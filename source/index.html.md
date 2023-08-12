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



# Future

## Long chain

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

> 以下三个函数有何区别？

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

























