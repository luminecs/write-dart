---
title: Write Dart

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - dart

toc_footers:
  - <a href='#'>主页</a>

#includes:
#  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Write Dart
---

# 介绍

此页面用以记录 Dart 学习过程中的代码片段和概念。

> Dart 打印 `Hello world!`。

```dart
void main() {
  print('Hello world!');
}
```

<aside class="notice">
这是一个 <code>Notice</code> 示例。
</aside>

<aside class="success">
这是一个 <code>Success</code> 示例。
</aside>

<aside class="warning">
这是一个 <code>Warning</code> 示例。
</aside>

# Class Modifiers

## abstract class

```dart
abstract class Vehicle {
  void moveForward(int meters);
}

// Error: Cannot be constructed
Vehicle myVehicle = Vehicle();

// Can be extended
class Car extends Vehicle {
  int passengers = 4;

  @override
  void moveForward(int meters) {}
}

// Can be implemented
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {}
}
```


# Future

## long-chain

```dart
Future<String> one() => Future.value('from one');
Future<String> two() => Future.error('error from two');
Future<String> three() => Future.value('from three');
Future<String> four() => Future.value('from four');

void main() {
  one() // Future completes with "from one".
      .then((_) => two()) // Future completes with two()'s error.
      .then((_) => three()) // Future completes with two()'s error.
      .then((_) => four()) // Future completes with two()'s error.
      .then((value) => value.length) // Future completes with two()'s error.
      .catchError((e) {
    print('Got error: $e'); // Finally, callback fires.
    return 42; // Future completes with 42.
  }).then((value) {
    print('The value is $value');
  });
}

// Output of this program:
//   Got error: error from two
//   The value is 42

```

## then-catch

```dart
Future<Object> myFunc() => Future.value('42');

String processValue(dynamic value) {
  return 'value';
}

Future<String> handleError(dynamic error) {
  return Future.value('value');
}

void main() {
  myFunc().then(processValue).catchError(handleError);
}
```

## comprehensive-errors

```dart
Future<Object> myFunc() => Future.value('42');

String doSomethingWith(dynamic value) {
  return 'value';
}

Future<String> handleError(dynamic error) {
  return Future.value('value');
}

Never ellipsis<T>() => throw Exception('!');

void main() {
  myFunc().then((value) {
    doSomethingWith(value);
    ellipsis(); // 抛出异常
    // 下面代码不会被执行
    throw Exception('Some arbitrary error');
  }).catchError(handleError);
}
```

## throws-then-catch

```dart
Future<Object> asyncErrorFunction() async {
  throw Exception('Threw an exception');
}

Future<Object> anotherAsyncErrorFunction() {
  throw Exception('Also threw an exception');
}

Object successCallback(dynamic value) async {
  return '';
}

Future<String> handleError(dynamic error) {
  print(error);
  return Future.value('value');
}

void main() {
  asyncErrorFunction().then(successCallback, onError: (e) {
    handleError(e); // Original error. 显示捕获异常，不然后面的 catchError 不会再捕获
    anotherAsyncErrorFunction(); // Oops, new error.
  }).catchError(handleError); // Error from within then() handled.
}
// Exception: Threw an exception
// Exception: Also threw an exception
```

## connect-server

```dart
Future<Object> handleResponse() => Future.value('Response');

Future<String> handleError(dynamic error) {
  return Future.value('value');
}

void main() {
  dynamic connectToServer() {}
  const myUrl = 'https://dart.dev';

  final server = connectToServer();
  server
      .post(myUrl, fields: const {'name': 'Dash', 'profession': 'mascot'})
      .then(handleResponse)
      .catchError(handleError)
      .whenComplete(server.close);
}
```

## future-then & future-catch-error

```dart
abstract class FakeFuture<T> {
  Future<R> then<R>(FutureOr<R> Function(T value) onValue, {Function? onError});

  Future<T> catchError(Function onError, {bool Function(Object error)? test});
}
```

> test 返回值为 true，onError 才会执行：

```dart
void main() {
  Future.delayed(
    const Duration(seconds: 1),
    () => throw 401,
  ).then((value) {
    throw 'Unreachable';
  }).catchError((err) {
    print('Error: $err'); // Prints 401.
  }, test: (error) {
    return error is int && error >= 400;
  });
}
```

## 注意事项

以下代码会抛出异常 `ArgumentError`：`Invalid argument(s) (onError): The error handler of Future.catchError must return a value of the future's type`，因为编译器推断 `then()` 的返回值类型是 `Future<Never>` 或 `Future<Null>`，然而真正的返回类型并不如此。

修改方法：`then()` 添加返回类型 `void`，告诉编译器无返回值。

```dart
void main() {
  // error
  Future(() => 1).then((value) {
    throw Exception('1');
  }).catchError((error, stackTrace) {
    print('$error, $stackTrace');
  });
  // error
  File("foo.txt").readAsString().catchError((e) {
    print(e);
  });

  // ok
  Future(() => 1).then<void>((value) {
    throw Exception('1');
  }).catchError((error, stackTrace) {
    print('$error, $stackTrace');
  });
  // ok
  File("foo.txt").readAsString().then<void>((value) {}).catchError((e) {
    print(e);
  });
}
```

另外也可是使用 `try-catch`。

```dart
void main() {
  try {
    File("foo.txt").readAsString();
  } catch (e) {
    print(e);
  }
}
```

## auth-response

```dart
import 'dart:async';

Future<Object> handleAuthResponse(Map<String, dynamic> data) {
  return Future.value('Response');
}

void handleFormatException(Object exception) {}

void handleAuthorizationException(Object exception) {}

class AuthorizationException implements Exception {}

Never ellipsis<T>() => throw AuthorizationException();

void main() {
  handleAuthResponse(const {'username': 'dash', 'age': 3})
      .then<void>((_) => ellipsis())
      .catchError(handleFormatException, test: (e) => e is FormatException)
      .catchError(handleAuthorizationException, // go to this branch
          test: (e) => e is AuthorizationException);
}
```

## early error handler

以下代码，捕获异常比抛出异常推迟 500 ms，所以不能捕获异常。

```dart
void main() {
  Future<Object> asyncErrorFunction() => throw Exception('1');

  Future<Object> future = asyncErrorFunction(); // 已经抛出

  // BAD: Too late to handle asyncErrorFunction() exception.
  Future.delayed(const Duration(milliseconds: 500), () {
    future.then((_) {}).catchError((e) {
      print('e');
    });
  });
}
```

正确做法是，`Future().then().catchError()` 写在一起。

```dart
void main() {
  Future<Object> asyncErrorFunction() async {
    throw Exception('Threw an exception');
  }
  Future.delayed(const Duration(milliseconds: 500), () {
    asyncErrorFunction().then((_) {}).catchError((e) {
      print('e'); // ok
    });
  });
}
```

## when complete

### with-error

```dart
void main() {
  Future<Object> asyncErrorFunction() async {
    throw Exception('Threw an exception');
  }

  Future<String> handleError(dynamic error) {
    return Future.value('value');
  }

  asyncErrorFunction()
      // Future completes with an error:
      .then((_) => print("Won't reach here"))
      // Future completes with the same error:
      .whenComplete(() => print('Reaches here'))
      // Future completes with the same error:
      .then((_) => print("Won't reach here"))
      // Error is handled here:
      .catchError(handleError);
}
```

### with-object

```dart
Never ellipsis<T>() => throw Exception('!');
final Never someObject = ellipsis();

void main() {
  Future<Object> asyncErrorFunction() async {
    throw Exception('Threw an exception');
  }

  Future<String> handleError(dynamic error) {
    return Future.value('value');
  }

  void printErrorMessage() {}

  asyncErrorFunction()
      // Future completes with an error:
      .then((_) {})
      .catchError((e) {
    handleError(e);
    printErrorMessage();
    // Future completes with someObject
    return someObject;
  }).catchError((e) {
    print(e);
  }).whenComplete(() => print('Done!'));
  // Future completes with someObject
}
```

### when-complete-error

```dart
void main() {
  Future<Object> asyncErrorFunction() async {
    throw Exception('Threw an exception');
  }

  Future<String> handleError(dynamic error) {
    return Future.value('value');
  }

  asyncErrorFunction()
      // Future completes with a value:
      .catchError(handleError)
      // Future completes with an error:
      .whenComplete(() => throw Exception('New error'))
      // Error is handled:
      .catchError(handleError);
}
```

# Utils

## A simple logger

```dart
/// A simple logger
class Logger {
  final List<String> _log = [];

  List<String> get log => List.from(_log);
  void clear() => _log.clear();
  void print(Object o) => _log.add(o.toString());

  @override
  String toString() => _log.join('\n');
}
```


# async

## 以下三个函数有何区别？

```dart
String processValue(dynamic value) {
  return 'value';
}

Future<String> processValue1(dynamic value) async {
  return Future.value('value');
}

Future<String> processValue2(dynamic value) {
  return Future.value('value');
}
```

函数 `processValue` 和 `processValue2` 相同，它们都是同步操作，`Future` 可有可无。函数 `processValue1` 因为使用了 `async`，所以是异步操作，必须返回 `Future`。






# Questions

## Never 是什么？

Never 是 Dart 中的一个类型，表示没有值。它通常用于表示不可能返回的函数的返回类型。比如函数中途一定会抛出异常的函数。

```dart
Never ellipsis<T>() => throw Exception('!');
```

## Dart 中 dynamic 和 Object 有何区别？

在 Dart 中，`dynamic` 和 `Object` 都是类型。`dynamic` 类型是动态类型，这意味着它可以存储任何类型的值。`Object` 类型是静态类型，这意味着它只能存储 `Object` 及其子类的值。

`dynamic` 类型通常用于在编译时不知道值类型的场合。例如，以下代码将 `dynamic` 类型变量 `x` 初始化为一个字符串：

```
dynamic x = 'Hello World!';
```

`Object` 类型通常用于在编译时知道值类型的场合。例如，以下代码将 `Object` 类型变量 `y` 初始化为一个字符串：

```
Object y = 'Hello World!';
```

`dynamic` 类型比 `Object` 类型更灵活，但也更不安全。使用 `dynamic` 类型时，编译器无法检查类型错误，这可能会导致错误。使用 `Object` 类型时，编译器可以检查类型错误，这有助于确保程序的安全性。

一般来说，在 Dart 中使用 `Object` 类型而不是 `dynamic` 类型是更好的做法。但是，在编译时不知道值类型的场合，使用 `dynamic` 类型是有意义的。










