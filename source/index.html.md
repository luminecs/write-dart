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

# language_tour

## callable_objects

```dart
class WannabeFunction {
  String call(String a, String b, String c) => '$a $b $c!';
}

var wf = WannabeFunction();
var out = wf('Hi', 'there', 'gang');

void main() => print(out);
```

# built_in_types

## integer-literals

```dart
void main() {
  var x = 1;
  var hex = 0xDEADBEEF;
}
```

## double-literals

```dart
void main() {
  var y = 1.1;
  var exponents = 1.42e5;
}
```

## declare-num

```dart
void main() {
  num nx = 1; // nx can have both int and double values
  nx += 2.5;
  print(nx); // 3.5
}
```

## int-to-double

```dart
void main() {
  double z = 1; // Equivalent to double z = 1.0.
}
```

## const-num

```dart
void main() {
  const msPerSecond = 1000;
  const secondsUntilRetry = 5;
  const msUntilRetry = secondsUntilRetry * msPerSecond;
}
```

## quoting

```dart
void main() {
  var s1 = 'Single quotes work well for string literals.';
  var s2 = "Double quotes work just as well.";
  var s3 = 'It\'s easy to escape the string delimiter.';
  var s4 = "It's even easier to use the other delimiter.";
}
```

## raw-strings

```dart
void main() {
  var s = r'In a raw string, not even \n gets special treatment.';
  print(s);
  // In a raw string, not even \n gets special treatment.
}
```

## string-literals

```dart
void main() {
  // These work in a const string.
  const aConstNum = 0;
  const aConstBool = true;
  const aConstString = 'a constant string';

  // These do NOT work in a const string.
  var aNum = 0;
  var aBool = true;
  var aString = 'a string';
  const aConstList = [1, 2, 3];

  const validConstString = '$aConstNum $aConstBool $aConstString';
  // const invalidConstString = '$aNum $aBool $aString $aConstList';
  // Const variables must be initialized with a constant value.
}
```

## const-list

```dart
void main() {
  var constantList = const [1, 2, 3];
  constantList[1] = 1; // This line will cause an error.
}
```

## set-literal

```dart
void main() {
  var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};

  // set-vs-map
  var names = <String>{};
  Set<String> names1 = {}; // This works, too.
  var names2 = {}; // Creates a map, not a set.

  // set-add-items
  var elements = <String>{};
  elements.add('fluorine');
  elements.addAll(halogens);
}
```

## const-set

```dart
void main() {
  final constantSet = const {
    'fluorine',
    'chlorine',
    'bromine',
    'iodine',
    'astatine',
  };
  constantSet.add('helium'); // This line will cause an error.
}
```

## map-literal

```dart
void main() {
  var gifts = {
    // Key:    Value
    'first': 'partridge',
    'second': 'turtledoves',
    'fifth': 'golden rings'
  };

  var nobleGases = {
    2: 'helium',
    10: 'neon',
    18: 'argon',
  };
}
```

## map-constructor

```dart
void main() {
  var gifts = Map<String, String>();
  gifts['first'] = 'partridge';
  gifts['second'] = 'turtledoves';
  gifts['fifth'] = 'golden rings';

  var nobleGases = Map<int, String>();
  nobleGases[2] = 'helium';
  nobleGases[10] = 'neon';
  nobleGases[18] = 'argon';
}
```

## map-add-item

```dart
void main() {
  var gifts = {'first': 'partridge'};
  gifts['fourth'] = 'calling birds'; // Add a key-value pair
}
```

## const-map

```dart
void main() {
  final constantMap = const {
    2: 'helium',
    10: 'neon',
    18: 'argon',
  };

  constantMap[2] = 'Helium'; // This line will cause an error.
}
```

## triple-quotes

```dart
void main() {
  var s1 = '''
  You can create
multi-line strings like this one.
  ''';
  var s2 = """This is also a
  multi-line string.""";
  print(s1);
  //   You can create
  // multi-line strings like this one.
  print(s2);
  // This is also a
  //   multi-line string.
}
```

## symbols

```dart
void main() {
  var a1 = Function.apply(int.parse, ['11']);
  print(a1); // 11
  var a2 = Function.apply(int.parse, ['11'], {#radix: 16});
  print(a2); // 17
}
```


# Generics

## base_class

```dart
class SomeBaseClass {}

class Foo<T extends SomeBaseClass> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'"; // ignore: annotate_overrides
}

class Extender extends SomeBaseClass {}

void main() {
  var extenderFoo = Foo<Extender>();
  print(extenderFoo); // Instance of 'Foo<Extender>'

  var someBaseClassFoo = Foo<SomeBaseClass>();
  print(someBaseClassFoo); // Instance of 'Foo<SomeBaseClass>'

  var foo = Foo();
  print(foo); // Instance of 'Foo<SomeBaseClass>'
}
```

## cache

```dart
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}

abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}

abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

## misc

```dart
// collection-literals
var names = <String>['Seth', 'Kathy', 'Lars'];
var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};

// non-nullable
class Foo<T extends Object> {
  // Any type provided to Foo for T must be non-nullable.
}
```

## constructor

```dart
class View {}

void main() {
  var names = <String>[];
  names.addAll(['Seth', 'Kathy', 'Lars']);
  var nameSet = Set<String>.from(names);
  print(nameSet); // {Seth, Kathy, Lars}
  
  var views = Map<int, View>();
}
```

## is

```dart
void main() {
  var names = <String>[];
  names.addAll(['Seth', 'Kathy', 'Lars']);
  // ignore: unnecessary_type_check
  print(names is List<String>); // true
}
```

## method

```dart
T first<T>(List<T> ts) {
  // Do some initial work or error checking, then...
  T tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}

void main() {
  print('first: ${first<int>([1, 2, 3])}'); // 1
}
```

# Class

## factory_constructors

```dart
class Shape {
  Shape();

  factory Shape.fromTypeName(String typeName) {
    if (typeName == 'square') return Square();
    if (typeName == 'circle') return Circle();
    throw ArgumentError('Unrecognized $typeName');
  }
}

class Square extends Shape {}

class Circle extends Shape {}

void main() {
  print(Shape() is Shape); // true
  print(Shape.fromTypeName('square') is Square); // true
  print(Shape.fromTypeName('circle') is Circle); // true
  Shape.fromTypeName('trapezoid');
  // Unhandled exception:
  // Invalid argument(s): Unrecognized typeName
}
```

## getter_compute

```dart
class MyClass {
  final List<int> _values = [];

  void addValue(int value) {
    _values.add(value);
  }

  // A computed property.
  int get count {
    return _values.length;
  }
}

void main() {
  MyClass clazz = MyClass();
  clazz.addValue(5);
  print(clazz.count); // 1
  clazz.addValue(7);
  print(clazz.count); // 2
}
```

## getters_setters

```dart
class MyClass {
  int _aProperty = 0;

  int get aProperty => _aProperty;

  set aProperty(int value) {
    if (value >= 0) {
      _aProperty = value;
    }
  }
}

void main() {
  MyClass clazz = MyClass();
  clazz.aProperty = 5;
  print(clazz.aProperty); // 5
  clazz.aProperty = -10;
  print(clazz.aProperty); // 5
}
```

## initializer_lists

```dart
class NonNegativePoint {
  final int x;
  final int y;

  NonNegativePoint(this.x, this.y)
      : assert(x >= 0),
        assert(y >= 0) {
    print('I just made a NonNegativePoint: ($x, $y)');
  }
}

void main() {
  NonNegativePoint(100, 100);
  // I just made a NonNegativePoint: (100, 100)
  try {
    NonNegativePoint(-50, 100);
  } on AssertionError catch (e) {
    print(e);
    // Failed assertion: line 6 pos 16: 'x >= 0': is not true.
  }
  try {
    NonNegativePoint(100, -50);
  } on AssertionError catch (e) {
    print(e);
    // Failed assertion: line 7 pos 16: 'y >= 0': is not true.
  }
}
```

## named_constructor

```dart
class Point {
  double x, y;

  Point(this.x, this.y);

  Point.origin()
      : x = 0,
        y = 0;
}

void main() {
  final point = Point(1, 2);
  print('${point.x}, ${point.y}'); // 1.0, 2.0
  final p = Point.origin();
  print('${p.x}, ${p.y}'); // 0.0, 0.0
}
```

## named_parameters

```dart
void printName(String firstName, String lastName, {String? middleName}) {
  print('$firstName ${middleName ?? ''} $lastName');
}

void printNameWithDefault(String firstName, String lastName, {String middleName = ''}) {
  print('$firstName $middleName $lastName');
}

void main() {
  printName('Dash', 'Dartisan'); // Dash  Dartisan
  printName('John', 'Smith', middleName: 'Who'); // John Who Smith
  printName('John', middleName: 'Who', 'Smith'); // John Who Smith
  printNameWithDefault('Dash', 'Dartisan', middleName: 'Best');
  // Dash Best Dartisan
  printNameWithDefault('Dash', 'Dartisan');
  // Dash  Dartisan
}
```

## optional_positional_args

```dart
int sumUp(int a, int b, int c) {
  return a + b + c;
}

int sumUpToFive(int a, [int? b, int? c, int? d, int? e]) {
  int sum = a;
  if (b != null) sum += b;
  if (c != null) sum += c;
  if (d != null) sum += d;
  if (e != null) sum += e;
  return sum;
}

int sumUpToFive2(int a, [int b = 2, int c = 3, int d = 4, int e = 5]) {
  return a + b + c + d + e;
}

void main() {
  int total1 = sumUp(1, 2, 3);
  int total2 = sumUpToFive(1, 2);
  int total3 = sumUpToFive(1, 2, 3, 4, 5);
  print(total1); // 6
  print(total2); // 3
  print(total3); // 15

  int total4 = sumUpToFive2(1);
  print(total4); // 15
}
```

## redirecting-constructors

```dart
class Automobile {
  String make;
  String model;
  int mpg;

  // The main constructor for this class.
  Automobile(this.make, this.model, this.mpg);

  // Delegates to the main constructor.
  Automobile.hybrid(String make, String model) : this(make, model, 60);

  // Delegates to a named constructor
  Automobile.fancyHybrid() : this.hybrid('Futurecar', 'Mark 2');
}

void main() {
  final hybrid = Automobile.hybrid('Dash', 'Null Safety');
  final fancyHybrid = Automobile.fancyHybrid();
}
```

## const-constructors

```dart
class ImmutablePoint {
  final int x;
  final int y;

  const ImmutablePoint(this.x, this.y);

  static const ImmutablePoint origin = ImmutablePoint(0, 0);
}
```

## required-positional

```dart
class MyColor {
  int red;
  int green;
  int blue;

  MyColor(this.red, this.green, this.blue);
}

void main() {
  final color = MyColor(80, 80, 128);
}
```

## required-named

```dart
class MyColorRN {
  int red, green, blue;

  MyColorRN({
    required this.red,
    required this.green,
    required this.blue,
  });
}

void main() {
  final colorRN = MyColorRN(red: 80, green: 80, blue: 128);
}
```

## defaulted

```dart
class MyColor0 {
  int red, green, blue;

  MyColor0.positional([this.red = 0, this.green = 0, this.blue = 0]);

  MyColor0.name({this.red = 0, this.green = 0, this.blue = 0});
}

void main() {
  final color1 = MyColor0.positional();
  final color2 = MyColor0.positional(1, 2, 3);
  final color3 = MyColor0.name();
  final color4 = MyColor0.name(red: 4, green: 5, blue: 6);
}
```

## doer

```dart
abstract class Doer {
  // Define instance variables and methods...
  void doSomething(); // Define an abstract method.
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // Provide an implementation,
    // so the method is not abstract here...
  }
}
```

## employee

```dart

```


# spacecraft

```dart
class Spacecraft {
  String name;
  DateTime? launchDate;

  // Read-only non-final property
  int? get launchYear => launchDate?.year;

  // Constructor, with syntactic sugar for assignment to members.
  Spacecraft(this.name, this.launchDate) {
    // Initialization code goes here.
  }

  // Named constructor that forwards to the default one.
  Spacecraft.unlaunched(String name) : this(name, null);

  // Method.
  void describe() {
    print('Spacecraft: $name');
    // Type promotion doesn't work on getters.
    var launchDate = this.launchDate;
    if (launchDate != null) {
      int years = DateTime.now().difference(launchDate).inDays ~/ 365;
      print('Launched: $launchYear ($years years ago)');
    } else {
      print('Unlaunched');
    }
  }
}

// extends
class Orbiter extends Spacecraft {
  double altitude;

  // 添加 DateTime 除去父类的 DateTime?
  Orbiter(super.name, DateTime super.launchDate, this.altitude);
}

// mixin
mixin Piloted {
  int astronauts = 1;

  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}

// mixin-use
class PilotedCraft extends Spacecraft with Piloted {
  PilotedCraft(super.name, DateTime super.launchDate);
}

// implements
class MockSpaceship implements Spacecraft {
  MockSpaceship(this.name);

  @override
  DateTime? launchDate = DateTime(1969, 7, 16);

  @override
  String name;

  @override
  void describe() => print(name);

  @override
  int? get launchYear => launchDate?.year;
}

// abstract
abstract class Describable {
  void describe();

  void describeWithEmphasis() {
    print('=========');
    describe();
    print('=========');
  }
}

// simple-enum
enum PlanetType { terrestrial, gas, ice }

// enhanced-enum
/// Enum that enumerates the different planets
/// in our solar system and some of their properties.
enum Planet {
  mercury(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
  venus(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
  earth(planetType: PlanetType.terrestrial, moons: 1, hasRings: false),
  mars(planetType: PlanetType.terrestrial, moons: 2, hasRings: false),
  jupiter(planetType: PlanetType.gas, moons: 80, hasRings: true),
  saturn(planetType: PlanetType.gas, moons: 83, hasRings: true),
  uranus(planetType: PlanetType.ice, moons: 27, hasRings: true),
  neptune(planetType: PlanetType.ice, moons: 14, hasRings: true);

  /// A constant generating constructor
  const Planet({
    required this.planetType,
    required this.moons,
    required this.hasRings,
  });

  /// All instance variables are final
  final PlanetType planetType;
  final int moons;
  final bool hasRings;

  /// Enhanced enums support getters and other methods
  bool get isGiant =>
      planetType == PlanetType.gas || planetType == PlanetType.ice;
}

void main() async {
  var voyager = Spacecraft('Voyager I', DateTime(1977, 9, 5));
  voyager.describe();
  // Spacecraft: Voyager I
  // Launched: 1977 (45 years ago)

  var voyager3 = Spacecraft.unlaunched('Voyager III');
  voyager3.describe();
  // Spacecraft: Voyager III
  // Unlaunched

  final yourPlanet = Planet.earth;
  if (!yourPlanet.isGiant) {
    print('Your planet is not a "giant planet".');
  } // Your planet is not a "giant planet".

  final o = Orbiter('O', DateTime(1999), 42);
  final p = PilotedCraft('shuttle', DateTime(1999));
  print(p.astronauts); // 1

  final m = MockSpaceship('Enterprise');
  m.describe(); // Enterprise

  // async*
  var flybyObjects = ['Jupiter', 'Saturn', 'Uranus', 'Neptune'];
  // oneSecond is shown in the code excerpts as 1 second,
  // but we don't need to delay the actual test execution,
  // so we set the delay to 0.
  const oneSecond = Duration(seconds: 0);
  Stream<String> report(Spacecraft craft, Iterable<String> objects) async* {
    for (final object in objects) {
      await Future.delayed(oneSecond);
      yield '${craft.name} flies by $object';
    }
  }

  final messages = await report(voyager, flybyObjects).toList();
  print(messages);
  // [Voyager I flies by Jupiter,
  // Voyager I flies by Saturn,
  // Voyager I flies by Uranus,
  // Voyager I flies by Neptune]
}
```

# typedef

```dart
typedef IntList = List<int>;
IntList il = [1, 2, 3];

typedef ListMapper<X> = Map<X, List<X>>;
Map<String, List<String>> m1 = {}; // Verbose.
ListMapper<String> m2 = {};// Same thing but shorter and clearer.

typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  print(sort is Compare<int>); // true
}
```














# Metadata

```dart
class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}

@Todo('Dash', 'Implement this function')
void doSomething() {
  print('Do something');
}

class Television {
  /// Use [turnOn] to turn the power on instead.
  @Deprecated('Use turnOn instead')
  void activate() {
    turnOn();
  }

  /// Turns the TV's power on.
  void turnOn() {}

  set contrast(int value) {}
}

class SmartTelevision extends Television {
  @override
  set contrast(num value) {}
}
```

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

## base class

```dart
base class Vehicle {
  void moveForward(int meters) {}
}

// Can be constructed
Vehicle myVehicle = Vehicle();

// Can be extended
base class Car extends Vehicle {
  int passengers = 4;
}

// 没有报错
base class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {
  }
}

// ERROR: Cannot be implemented
base class MockVehicle2 implements Vehicle {
  @override
  void moveForward() {
    // ...
  }
}
```

## interface class

```dart
interface class Vehicle {
  void moveForward(int meters) {}
}

// Can be constructed
Vehicle myVehicle = Vehicle();

// ERROR: Cannot be inherited - 没有报错
class Car extends Vehicle {
  int passengers = 4;
}

// Can be implemented
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {}
}
```

## final class

```dart
final class Vehicle {
  void moveForward(int meters) {}
}

// Can be constructed
Vehicle myVehicle = Vehicle();

// ERROR: Cannot be inherited
class Car extends Vehicle {
  int passengers = 4;
}

class MockVehicle implements Vehicle {
  // ERROR: Cannot be implemented
  @override
  void moveForward(int meters) {}
}
```

## sealed class

```dart
sealed class Vehicle {}

class Car extends Vehicle {}

class Truck implements Vehicle {}

class Bicycle extends Vehicle {}

// ERROR: Cannot be instantiated
Vehicle myVehicle = Vehicle();

// Subclasses can be instantiated
Vehicle myCar = Car();

String getVehicleSound(Vehicle vehicle) {
  // ERROR: The switch is missing the
  // Bicycle subtype or a default case.
  return switch (vehicle) {
    Car() => 'vroom',
    Truck() => 'VROOOOMM',
  };
}
```

# Control Flow

## if-else

```dart
void main() {
  bool isRaining() => true;
  bool isSnowing() => true;
  dynamic car, you;
  if (isRaining()) {
    you.bringRainCoat();
  } else if (isSnowing()) {
    you.wearJacket();
  } else {
    car.putTopDown();
  }
}
```

## if-case

```dart
class Point {
  final int x;
  final int y;

  Point(this.x, this.y);
}

Point main() {
  var pair = [1, 2];
  if (pair case [int x, int y]) return Point(x, y);
  return Point(1, 1);
}
```

## if-case-else

```dart
void main() {
  var pair = [1, 2];
  if (pair case [int x, int y]) {
    print('Was coordinate array $x,$y');
  } else {
    throw FormatException('Invalid coordinates.');
  }
}
```

## switch

```dart
void executeClosed() {}
void executePending() {}
void executeApproved() {}
void executeDenied() {}
void executeOpen() {}
void executeUnknown() {}
void executeNowClosed() {}

void main() {
  var command = 'OPEN';
  switch (command) {
    case 'CLOSED':
      executeClosed();
    case 'PENDING':
      executePending();
    case 'APPROVED':
      executeApproved();
    case 'DENIED':
      executeDenied();
    case 'OPEN':
      executeOpen();
    default:
      executeUnknown();
  }
}
```

## switch-empty

```dart
void executeClosed() {}
void executeOpen() {}
void executeNowClosed() {}

void main() {
  var command = 'OPEN';
  switch (command) {
    case 'OPEN':
      executeOpen();
      continue newCase; // Continues executing at the newCase label.

    case 'DENIED': // Empty case falls through.
    case 'CLOSED':
      executeClosed(); // Runs for both DENIED and CLOSED,

    newCase:
    case 'PENDING':
      executeNowClosed(); // Runs for both OPEN and PENDING.
  }
}
```

## switch-stmt

```dart
dynamic charCode;
const slash = '/';
const star = '*';
const plus = '+';
const minus = '-';
const comma = ',';
const semicolon = ',';
const int digit0 = 0;
const int digit9 = 9;
Object? token;

dynamic operator(dynamic x) {}
dynamic punctuation(dynamic x) {}
dynamic number() {}

void main() {
  // Where slash, star, comma, semicolon, etc., are constant variables...
  switch (charCode) {
    case slash || star || plus || minus: // Logical-or pattern
      token = operator(charCode);
    case comma || semicolon: // Logical-or pattern
      token = punctuation(charCode);
    case >= digit0 && <= digit9: // Relational and logical-and patterns
      token = number();
    default:
      throw FormatException('Invalid');
  }
}
```

## switch-exp

```dart
dynamic charCode;
const slash = '/';
const star = '*';
const plus = '+';
const minus = '-';
const comma = ',';
const semicolon = ',';
const int digit0 = 0;
const int digit9 = 9;
Object? token;

dynamic operator(dynamic x) {}
dynamic punctuation(dynamic x) {}
dynamic number() {}

void main() {
  token = switch (charCode) {
    slash || star || plus || minus => operator(charCode),
    comma || semicolon => punctuation(charCode),
    >= digit0 && <= digit9 => number(),
    _ => throw FormatException('Invalid')
  };
}
```

## exh-bool

```dart
void main() {
  bool? nullableBool = false;
  // Non-exhaustive switch on bool?, missing case to match null possibility:
  switch (nullableBool) {
    case true:
      print('yes');
    case false:
      print('no');
  }
}
```

## guard

```dart
void main() {
  var pair = [1, 2];
  switch (pair) {
    case (int a, int b) when a > b:
      print('First element greater');
    case (int a, int b):
      print('First element not greater');
  }
}
```

## loop collection

```dart
final class Candidate {
  String name = '';
  int yearsExperience = 0;

  void interview() {}
}

final candidates = <Candidate>[];

void main() {
  for (final candidate in candidates) {
    candidate.interview();
  }
}
```

## loop collection-for-pattern

```dart
final class Candidate {
  String name = '';
  int yearsExperience = 0;

  void interview() {}
}

final candidates = <Candidate>[];

void main() {
  for (final Candidate(:name, :yearsExperience) in candidates) {
    print('$name has $yearsExperience of experience.');
  }
}
```

## while

```dart
void main() {
  bool isDone() => true;
  bool doSomething() => true;
  while (!isDone()) {
    doSomething();
  }
}
```

## do-while

```dart
void main() {
  bool atEndOfPage() => true;
  bool printLine() => true;
  do {
    printLine();
  } while (!atEndOfPage());
}
```

## while-break

```dart
void main() {
  bool shutDownRequested() => true;
  bool processIncomingRequests() => true;
  while (true) {
    if (shutDownRequested()) break;
    processIncomingRequests();
  }
}
```

## for-continue

```dart
final class Candidate {
  String name = '';
  int yearsExperience = 0;

  void interview() {}
}

void main() {
  final candidates = <Candidate>[];
  for (int i = 0; i < candidates.length; i++) {
    var candidate = candidates[i];
    if (candidate.yearsExperience < 5) {
      continue;
    }
    candidate.interview();
  }
}
```

## where

```dart
final class Candidate {
  String name = '';
  int yearsExperience = 0;

  void interview() {}
}

void main() {
  final candidates = <Candidate>[];
  candidates
      .where((c) => c.yearsExperience >= 5)
      .forEach((c) => c.interview());
}
```

## for-and-closures

```dart
void main() {
  var callbacks = [];
  for (var i = 0; i < 2; i++) {
    callbacks.add(() => print(i));
  }
  for (final callback in callbacks) {
    callback();
  }
}
```

## for-each

```dart
void main() {
  var collection = [1, 2, 3];
  collection.forEach(print);
}
```


# Patterns

## algebraic_datatypes

```dart
import 'dart:math' as math;

sealed class Shape {}

class Square implements Shape {
  final double length;
  Square(this.length);
}

class Circle implements Shape {
  final double radius;
  Circle(this.radius);
}

double calculateArea(Shape shape) => switch (shape) {
  Square(length: var l) => l * l,
  Circle(radius: var r) => math.pi * r * r
};
```

## destructuring list-pattern

```dart
void main() {
  var numList = [1, 2, 3];
  // List pattern [a, b, c] destructures the three elements from numList...
  var [a, b, c] = numList;
  // ...and assigns them to new variables.
  print(a + b + c); // 6
}
```

## destructuring nested-pattern

```dart
void main() {
  var list = ['b', 'c'];
  switch (list) {
    case ['a' || 'b', var c]:
      print(c);
  }
}
```

## destructuring variable-declaration

```dart
void main() {
  // Declares new variables a, b, and c.
  var (a, [b, c]) = ('str', [1, 2]);
}
```

## destructuring variable-assignment

```dart
void main() {
  var (a, b) = ('left', 'right');
  (b, a) = (a, b); // Swap.
  print('$a $b'); // Prints "right left".
}
```

## destructure-multiple-returns

```dart
(String, int) userInfo(Map<String, dynamic> json) {
  return ('doug', 25);
}

var json = <String, dynamic>{};

void main() {
  var info = userInfo(json);
  var name = info.$1;
  var age = info.$2;
  var (name1, age1) = userInfo(json);
}
```

## destructure-class-instances

```dart
class Foo {
  final String one;
  final int two;

  Foo({required this.one, required this.two});
}

void main() {
  final Foo myFoo = Foo(one: 'one', two: 2);
  var Foo(:one,:two) = myFoo;
  print('one $one, two $two');
}
```

## for-in-pattern & for-in-pattern

```dart
Map<String, int> hist = {'a': 23, 'b': 100};

void main() {
  for (var MapEntry(key: key, value: count) in hist.entries) {
    print('$key occurred $count times');
  }

  for (var MapEntry(:key, value: count) in hist.entries) {
    print('$key occurred $count times');
  }
}
```

## json

```dart
void main() {
  var json = {
    'user': ['Lily', 13]
  };
  var {'user': [name, age]} = json;

  if (json is Map<String, Object?> &&
      json.length == 1 &&
      json.containsKey('user')) {
    var user = json['user'];
    if (user is List<Object> &&
        user.length == 2 &&
        user[0] is String &&
        user[1] is int) {
      var name = user[0] as String;
      var age = user[1] as int;
      print('User $name is $age years old.');
    }
  }

  if (json case {'user': [String name, int age]}) {
    print('User $name is $age years old.');
  }
}
```

## record-syntax

```dart
void main() {
  var record = ('first', a: 2, b: true, 'last');
  // record-getters
  print(record.$1); // first
  print(record.$2); // last
  print(record.a); // 2
  print(record.b); // true
}
```

## record-type-annotation

```dart
void main() {
  (int, int) swap((int, int) record) {
    var (a, b) = record;
    return (b, a);
  }

  print(swap((1, 2))); // (2, 1)
}
```

## record-type-declaration

```dart
void main() {
  // Record type annotation in a variable declaration:
  (String, int) record;
  // Initialize it with a record expression:
  record = ('A string', 123);
}
```

## record-type-named-declaration

```dart
void main() {
  // Record type annotation in a variable declaration:
  ({int a, bool b}) record;
  // Initialize it with a record expression:
  record = (a: 123, b: true);
}
```

## record-type-mismatched-names

```dart
void main() {
  ({int a, int b}) recordAB = (a: 1, b: 2);
  ({int x, int y}) recordXY = (x: 3, y: 4);
  // Compile error! These records don't have the same type.
  // recordAB = recordXY;
  recordAB;
  recordXY;
}
```

## record-type-matched-names

```dart
void main() {
  (int a, int b) recordAB = (1, 2);
  (int x, int y) recordXY = (3, 4);
  recordAB = recordXY; // OK.
  recordAB;
  recordXY;
}
```

## record-getters-two

```dart
void main() {
  (num, Object) pair = (42, 'a');
  // Static type `num`, runtime type `int`.
  var first = pair.$1;
  // Static type `Object`, runtime type `String`.
  var second = pair.$2;
  first;
  second;
}
```

## record-shape

```dart
void main() {
  (int x, int y, int z) point = (1,2,3);
  (int r, int g, int b) color = (1,2,3);
  print(point == color); // true
}
```

## record-shape-mismatch

```dart
void main() {
  ({int x, int y, int z}) point = (x: 1, y: 2, z: 3);
  ({int r, int g, int b}) color = (r: 1, g: 2, b: 3);
  // Prints 'false'. Lint: Equals on unrelated types.
  print(point == color);
}
```

## record-multiple-returns

```dart
void main() {
  (String, int) userInfo(Map<String, dynamic> json) {
    return (json['name'] as String, json['age'] as int);
  }

  final json = <String, dynamic>{
    'name': 'Dash',
    'age': 10,
    'color': 'blue',
  };
  // Destructures using a record pattern:
  var (name, age) = userInfo(json);
  /* Equivalent to:
    var info = userInfo(json);
    var name = info.$1;
    var age  = info.$2;
  */
  print(name); // Dash
  print(age); // 10
}
```




## pattern_types cast

```dart
void main() {
  (num, Object) record = (1, 's');
  var (i as int, s as String) = record;
}
```

## pattern_types constant

```dart
void main() {
  var number = 1;
  switch (number) {
    // Matches if 1 == number.
    case 1: // ...
  }
}
```

## pattern_types complex-constant

```dart
void main() {
  const a = 1;
  const b = 2;
  switch ([1, 2]) {
    // List or map pattern:
    case [a, b]: // ...

    // List or map literal:
    case const [a, b]: // ...
  }
}
```

## pattern_types match-context

```dart
void main() {
  const c = 1;
  switch (2) {
    case c:
      print('match $c');
    default:
      print('no match'); // Prints "no match".
  }
}
```

## pattern_types rest

```dart
void main() {
  var [a, b, ..., c, d] = [1, 2, 3, 4, 5, 6, 7];
  print('$a $b $c $d'); // Prints "1 2 6 7".
}
```

## pattern_types rest-sub

```dart
void main() {
  var [a, b, ...rest, c, d] = [1, 2, 3, 4, 5, 6, 7];
  print('$a $b $rest $c $d'); // Prints "1 2 [3, 4, 5] 6 7".
}
```

## pattern_types logical-and

```dart
void main() {
  switch ((1, 2)) {
    // Error, both subpatterns attempt to bind 'b'.
    case (var a, var b) && (var b, var c): // ...
  }
}
```

## pattern_types logical-or

```dart
class Color {
  static const red = true;
  static const yellow = false;
  static const blue = true;
}

void main() {
  var color = Color.red;
  var isPrimary = switch (color) {
    Color.red || Color.yellow || Color.blue => true,
    _ => false
  };
  print('$isPrimary'); // true
}
```

## pattern_types share-guard

```dart
sealed class Shape {}

class Square implements Shape {
  final double size;
  Square(this.size);
}

class Circle implements Shape {
  final double size;
  Circle(this.size);
}

void main() {
  var shape = Square(10);
  switch (shape) {
    case Square(size: var s) || Circle(size: var s) when s > 0:
      print('Non-empty symmetric shape');
  }
}
```

## pattern_types null-assert-match

```dart
void main() {
  List<String?> row = ['user', null];
  switch (row) {
    case ['user', var name!]:
    // 'name' is a non-nullable string here.
  }
}
```

## pattern_types null-assert-dec

```dart
void main() {
  (int?, int?) position = (2, 3);
  var (x!, y!) = position;
}
```

## pattern_types null-check

```dart
void main() {
  String? maybeString = 'nullable with base type String';
  switch (maybeString) {
    case var s?:
    // 's' has type non-nullable String here.
  }
}
```

## pattern_types object

```dart
sealed class Shape {}

class Square implements Shape {
  final double size;
  Square(this.size);
}

class Circle implements Shape {
  final double size;
  Circle(this.size);
}

class Rect {
  final int width;
  final int height;
  Rect({required this.width, required this.height});
}

void main() {
  var shape = Square(10);
  switch (shape) {
    // Matches if shape is of type Rect,
    // and then against the properties of Rect.
    case Rect(width: var w, height: var h): // ...
  }
}
```

## pattern_types object-getter

```dart
class Point {
  final int? x;
  final int? y;
  Point(this.x, this.y);
}

void main() {
  // Binds new variables x and y to the
  // values of Point's x and y properties.
  var Point(:x, :y) = Point(1, 2);
}
```

## pattern_types record

```dart
void main() {
  var (myString: foo, myNumber: bar) = (myString: 'string', myNumber: 1);
}
```

## pattern_types record-getter

```dart
void main() {
  var record = (untyped: '1', typed: 2);
  // Record pattern with variable subpatterns:
  var (untyped: untyped, typed: int typed) = record;
  var (:untyped1, :int typed1) = (untyped1: '1', typed1: 2);

  switch (record) {
    case (untyped: var untyped, typed: int typed): // ...
    case (:var untyped, :int typed): // ...
  }

  // Record pattern with null-check and null-assert subpatterns:
  switch (record) {
    case (checked: var checked?, asserted: var asserted!): // ...
    case (:var checked?, :var asserted!): // ...
  }

  // Record pattern wih cast subpattern:
  var (untyped: untyped2 as int, typed: typed2 as String) = (untyped: '1', typed: 2);
  var (:untyped3 as int, :typed3 as String) = (untyped3: '1', typed3: 2);
}
```

## pattern_types relational

```dart
void main() {
  String asciiCharType(int char) {
    const space = 32;
    const zero = 48;
    const nine = 57;

    return switch (char) {
      < space => 'control',
      == space => 'space',
      > space && < zero => 'punctuation',
      >= zero && <= nine => 'digit',
      _ => ''
    };
  }
  assert(asciiCharType(32) == 'space');
}
```

## pattern_types variable

```dart
void main() {
  switch ((1, 2)) {
    // 'var a' and 'var b' are variable patterns
    // that bind to 1 and 2, respectively.
    case (var a, var b):
    // 'a' and 'b' are in scope in the case body.
  }
}
```

## pattern_types variable-typed

```dart
void main() {
  switch ((1, 2)) {
    // Does not match.
    case (int a, String b): // ...
  }
}
```

## pattern_types wildcard

```dart
void main() {
  var list = [1, 2, 3];
  var [_, two, _] = list;
}
```

## pattern_types wildcard-typed

```dart
void main() {
  var record = (1, 'one');
  switch (record) {
    case (int _, String _):
      print('First field is int and second is String.');
  }
}
```

## pattern_types parens

```dart
void main() {
  const x = true;
  const y = true;
  const z = false;
  var result = true;
  var token = switch (result) {
    // ...
    x || y && z => 'matches true',
    (x || y) && z => 'matches false',
    // ...
    _ => throw FormatException('Invalid')
  };
}
```

## switch constant-pattern

```dart
void main() {
  var number = 1;
  switch (number) {
    // Constant pattern matches if 1 == number.
    case 1:
      print('one');
  }
}
```

## switch list-pattern

```dart
void main() {
  var obj = ['a', 'b'];
  const a = 'a';
  const b = 'b';
  switch (obj) {
    // List pattern [a, b] matches obj first if obj is a list with two fields,
    // then if its fields match the constant subpatterns 'a' and 'b'.
    case [a, b]:
      print('$a, $b'); // a, b
  }
}
```

## switch-statement

```dart
void main() {
  var obj = 0;
  const first = 0;
  const last = 10;
  switch (obj) {
    // Matches if 1 == obj.
    case 1:
      print('one');

    // Matches if the value of obj is between the constant values of 'first' and 'last'.
    case >= first && <= last:
      print('in range');

    // Matches if obj is a record with two fields, then assigns the fields to 'a' and 'b'.
    case (var a, var b):
      print('a = $a, b = $b');

    default:
  }
}
```

# Concurrency

## sync read json file

```dart
import 'dart:convert';
import 'dart:io';

// {"a": "foo", "b": "bar", "c": "baz"}
const String filename = 'with_keys.json';

String _readFileSync() {
  final file = File(filename);
  final contents = file.readAsStringSync();
  return contents.trim();
}

void main() async {
  // Read some data.
  final fileData = _readFileSync();
  final jsonData = jsonDecode(fileData);
  // Use that data.
  print('Number of JSON keys: ${jsonData.length}');
}
```

## async read json file

```dart
import 'dart:convert';
import 'dart:io';

// {"a": "foo", "b": "bar", "c": "baz"}
const String filename = 'with_keys.json';

Future<String> _readFileAsync() async {
  final file = File(filename);
  final contents = await file.readAsString();
  return contents.trim();
}

void main() async {
  // Read some data.
  final fileData = await _readFileAsync();
  final jsonData = jsonDecode(fileData);
  // Use that data.
  print('Number of JSON keys: ${jsonData.length}');
}
```

## simple_isolate_closure

```dart
import 'dart:convert';
import 'dart:io';
import 'dart:isolate';

// {"a": "foo", "b": "bar", "c": "baz"}
const String filename = 'with_keys.json';

void main() async {
  // Read some data.
  final jsonData = await Isolate.run(() async {
    final fileData = await File(filename).readAsString();
    final jsonData = jsonDecode(fileData) as Map<String, dynamic>;
    return jsonData;
  });
  // Use that data.
  print('Number of JSON keys: ${jsonData.length}');
}
```

## simple_worker_isolate

```dart
import 'dart:convert';
import 'dart:io';
import 'dart:isolate';

// {"a": "foo", "b": "bar", "c": "baz"}
const String filename = 'with_keys.json';
// spawned
Future<Map<String, dynamic>> _readAndParseJson() async {
  final fileData = await File(filename).readAsString();
  final jsonData = jsonDecode(fileData) as Map<String, dynamic>;
  return jsonData;
}

void main() async {
  // Read some data.
  final jsonData = await Isolate.run(_readAndParseJson);
  // Use that data.
  print('Number of JSON keys: ${jsonData.length}');
}
```

# Extension Methods

## extension list

```dart
extension MyFancyList<T> on List<T> {
  int get doubleLength => length * 2;
  List<T> operator -() => reversed.toList();
  List<List<T>> split(int at) => [sublist(0, at), sublist(at)];
}

extension MyIntList on List<int> {
  int get tripleLength => length * 3;
}

void main() {
  final list1 = ['a', 'b', 'c'];
  print(list1.doubleLength); // 6
  print(-list1); // [c, b, a]
  print(list1.split(1)); // [[a], [b, c]]

  final list2 = [1, 2, 3];
  print(list2.tripleLength); // 9
}
```

## extension String & import-as-hide

> string_apis.dart

```dart
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }

  double parseDouble() {
    return double.parse(this);
  }
}
```

> string_apis_2.dart

```dart
extension NumberParsing2 on String {
  int parseInt() {
    return int.parse(this);
  }
}

extension HexParsing on String {
  int parseHexInt() {
    return int.parse(this, radix: 16);
  }
}
```

> string_apis_3.dart

```dart
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this, radix: 16);
  }

  num parseNum() {
    return num.parse(this);
  }
}
```

> string_apis_unnamed.dart

```dart
extension on String {
  bool get isBlank => trim().isEmpty;
}

bool isBlank(String string) => string.isBlank;

void main() {
  assert(isBlank('not-blank') == false);
  assert(isBlank(' not-blank ') == false);
  assert(isBlank('') == true);
  assert(isBlank(' ') == true);
}
```

> usage_explicit.dart

```dart
// Both libraries define extensions on String that contain parseInt(),
// and the extensions have different names.
import 'string_apis.dart'; // Contains NumberParsing extension.
import 'string_apis_2.dart'; // Contains NumberParsing2 extension.

void main() {
  // print('42'.parseInt()); // Doesn't work.
  print(NumberParsing('42').parseInt());
  print(NumberParsing2('42').parseInt());
  print('42'.parseDouble());
}
```

> usage_import.dart

```dart
// Defines the String extension method parseInt().
import 'string_apis.dart';

// Also defines parseInt(), but hiding NumberParsing2
// hides that extension method.
import 'string_apis_2.dart' hide NumberParsing2;

void main() {
  // Uses the parseInt() defined in 'string_apis.dart'.
  print('42'.parseInt());
  // Uses parseHexInt(), defined in 'string_apis_2.dart'.
  print('42'.parseHexInt());
  // Uses the parseDouble() defined in 'string_apis.dart'.
  print('42'.parseDouble());
}
```

> usage_prefix.dart

```dart
// Both libraries define extensions named NumberParsing
// that contain the extension method parseInt().
// One NumberParsing extension (in 'string_apis_3.dart')
// also defines parseNum().
import 'string_apis.dart';
import 'string_apis_3.dart' as rad;

void main() {
  // print('42'.parseInt()); // Doesn't work.
  // Use the ParseNumbers extension from string_apis.dart.
  print(NumberParsing('42').parseInt());
  // Use the ParseNumbers extension from string_apis_3.dart.
  print(rad.NumberParsing('42').parseInt());
  // Only string_apis_3.dart has parseNum().
  print('42'.parseNum());
}
```

> usage_simple_extension.dart

```dart
// Import a library that contains an extension on String.
import 'string_apis.dart';

void main() {
  // WithOUT extension methods.
  print(int.parse('42'));
  print(double.parse('42'));

  // WITH extension methods.
  print('42'.padLeft(5)); // Use a String method.
  print('42'.parseInt()); // Use an extension method.
  print('42'.parseDouble());

  // var vs. dynamic.
  var v = '2';
  print(v.parseInt()); // Output: 2

  dynamic d = '2';

  if (true) {
    // Runtime exception: NoSuchMethodError
    print(d.parseInt());
  }
  print(d); // Avoid unused_local_variable hint.
}
```

# Null safety

## non_nullable_types

```dart
void main() {
  int a;
  a = 145;
  // A value of type 'Null' can't be assigned to a variable of type 'int'.
  // a = null;
  print('a is $a.');
}
```

## nullable_types

```dart
void main() {
  int? a;
  a = null;
  print('a is $a.');
}
```

## more_nullable_types

```dart
void main() {
  List<String> aListOfStrings = ['one', 'two', 'three'];
  List<String>? aNullableListOfStrings;
  List<String?> aListOfNullableStrings = ['one', null, 'three'];

  print('$aListOfStrings.'); // [one, two, three]
  print('$aNullableListOfStrings.'); // null
  print('$aListOfNullableStrings.'); // [one, null, three]
}
```

## late_keyword

```dart
class Meal {
  late String _description;

  set description(String desc) {
    _description = 'Meal description: $desc';
  }

  String get description => _description;
}

void main() {
  final myMeal = Meal();
  // Unhandled exception:
  // LateInitializationError: Field '_description@18009629' has not been initialized.
  print(myMeal.description);
  myMeal.description = 'Feijoada!';
  print(myMeal.description);
}
```

## late_lazy

```dart
int _computeValue() {
  print('In _computeValue...');
  return 3;
}

class CachedValueProvider {
  final _cache = _computeValue();
  int get value => _cache;
}

void main() {
  print('Calling constructor...');
  var provider = CachedValueProvider();
  print('Getting value...');
  print('The value is ${provider.value}!');
}

// Calling constructor...
// In _computeValue...
// Getting value...
// The value is 3!
```

## late_circular_references

```dart
class Team {
  late final Coach coach;
}

class Coach {
  late final Team team;
}

void main() {
  final myTeam = Team();
  final myCoach = Coach();
  myTeam.coach = myCoach;
  myCoach.team = myTeam;

  print('All done!');
}
```

## promotion_exceptions

```dart
int getLength(String? str) {
  // Try throwing an exception here if `str` is null.
  if (str == null) {
    throw Exception('String is null');
  }
  return str.length;
}

void main() {
  print(getLength(null));
}
```

## type_promotion

```dart
int getLength(String? str) {
  // Add null check here
  if (str == null) {
    return 0;
  }
  return str.length;
}

void main() {
  print(getLength('This is a string!'));
}
```

## assertion_operator

```dart
int? couldReturnNullButDoesnt() => -3;

void main() {
  int? couldBeNullButIsnt = 1;
  List<int?> listThatCouldHoldNulls = [2, null, 4];
  int a = couldBeNullButIsnt;
  int b = listThatCouldHoldNulls.first!; // first item in the list
  int c = couldReturnNullButDoesnt()!.abs(); // absolute value
  print('a is $a.'); // 1
  print('b is $b.'); // 2
  print('c is $c.'); // 3
}
```

## null_aware_operators

```dart
class TestObject {
  void action() {}
}

TestObject? nullableObjectGenerate() => TestObject();

String? nullableStringGenerate() => null;

void other() {
  final nullableObject = nullableObjectGenerate();
  // The following calls the 'action' method
  // only if nullableObject is not null
  nullableObject?.action();

  var nullableString = nullableStringGenerate();
  // Both of the following print out 'alternate' if nullableString is null
  print(nullableString ?? 'alternate');
  print(nullableString != null ? nullableString : 'alternate');

  // Both of the following set nullableString to 'alternate' if it is null
  nullableString ??= 'alternate';
  nullableString = nullableString != null ? nullableString : 'alternate';
}
```

# Non promotion

## property_bang

```dart
class C1 {
  int? i;

  void f() {
    if (i == null) return;
    print(i!.isEven);
  }
}
```

## property_copy

```dart
class C {
  int? i;
  void f() {
    final i = this.i;
    if (i == null) return; // return
    print(i.isEven);
  }
}
```

## write_combine_ifs

```dart
void f(bool b, int? i, int? j) {
  if (i == null) return;
  if (b) {
    i = j;
  } else {
    print(i.isEven);
  }
}
```

## write_change_type

```dart
void f(bool b, int? i, int j) {
  if (i == null) return;
  if (b) {
    i = j;
  }
  if (!b) {
    print(i.isEven);
  }
}
```

## loop

```dart
class Link {
  final value = 0;
  late Link next;
}

void f(Link? p) {
  while (p != null) {
    print(p.value);
    p = p.next;
  }
}
```

## switch-loop

```dart
void f(int i, int? j, int? k) {
  switch (i) {
    label:
    case 0:
      if (j == null) return;
      print(j.isEven);
      j = k;
      continue label;
  }
}
```

## catch-null-check

```dart
void f(int? i, int? j) {
  if (i == null) return;
  try {
    i = j; // (1)
    // ... Additional code ...
    if (i == null) return; // (2)
    // ... Additional code ...
  } catch (e) {
    if (i != null) {
      print(i.isEven); // (3) OK due to the null check in the line above.
    } else {
      // Handle the case where i is null.
    }
  }
}
```

## catch-bang

```dart
void f(int? i, int? j) {
  if (i == null) return;
  try {
    i = j; // (1)
    // ... Additional code ...
    if (i == null) return; // (2)
    // ... Additional code ...
  } catch (e) {
    print(i!.isEven); // (3) OK because of the `!`.
  }
}
```

## subtype-variable

```dart
void f(Object o) {
  if (o is Comparable /* (1) */) {
    Object o2 = o;
    if (o2 is Pattern /* (2) */) {
      print(o2.matchAsPrefix('foo')); // (3) OK; o2 was promoted to `Pattern`.
    }
  }
}
```

## subtype-redundant

```dart
void f(Object o) {
  if (o is Comparable /* (1) */) {
    if (o is Pattern /* (2) */) {
      print((o as Pattern).matchAsPrefix('foo')); // (3) OK
    }
  }
}
```

## subtype-String

```dart
void f(Object o) {
  if (o is Comparable /* (1) */) {
    if (o is String /* (2) */) {
      print(o.matchAsPrefix('foo')); // (3) OK
    }
  }
}
```

## local-write-capture-reorder

```dart
void f(int? i, int? j) {
  if (i == null) return; // (1)
  // ... Additional code ...
  print(i.isEven); // (2) OK
  var foo = () {
    i = j;
  };
  // ... Use foo ...
}
```

## local-write-capture-copy

```dart
void f(int? i, int? j) {
  var foo = () {
    i = j;
  };
  // ... Use foo ...
  var i2 = i;
  if (i2 == null) return; // (1)
  // ... Additional code ...
  print(i2.isEven); // (2) OK because `i2` isn't write captured.
}
```

## local-write-capture-bang

```dart
void f(int? i, int? j) {
  var foo = () {
    i = j;
  };
  // ... Use foo ...
  if (i == null) return; // (1)
  // ... Additional code ...
  print(i!.isEven); // (2) OK due to `!` check.
}
```

## closure-new-var

```dart
void f(int? i, int? j) {
  if (i == null) return;
  var i2 = i;
  var foo = () {
    print(i2.isEven); // (1) OK because `i2` isn't changed later.
  };
  i = j; // (2)
}
```

## closure-new-var2

```dart
void f(int? i) {
  var j = i ?? 0;
  var foo = () {
    print(j.isEven); // OK
  };
}
```

## closure-write-capture

```dart
void f(int? i, int? j) {
  var foo = () {
    var i2 = i;
    if (i2 == null) return;
    print(i2.isEven); // OK because i2 is local to this closure.
  };
  var bar = () {
    i = j;
  };
}
```

# Type System

## animal type

```dart
Never ellipsis<T>() => throw Exception('!');

class Animal {
  void chase(Animal a) {}
  Animal get parent => ellipsis();
}

class HoneyBadger extends Animal {
  @override
  void chase(Animal a) {}

  @override
  HoneyBadger get parent => ellipsis();
}

class HoneyBadger1 extends Animal {
  @override
  void chase(Object a) {}

  @override
  Animal get parent => ellipsis();
}

class Alligator extends Animal {}
class Cat extends Animal {}
class Dog extends Animal {}
class MaineCoon extends Cat {}

void main() {
  Animal c1 = Cat(); // ok
  MaineCoon c2 = Cat(); // error
  Cat c3 = Cat(); // ok
  Cat c4 = MaineCoon(); // ok
  // generic-type-assignment
  List<MaineCoon> myMaineCoons = ellipsis();
  List<Cat> myCats = myMaineCoons;

  List<Animal> myAnimals = ellipsis();
  List<Cat> myCats = myAnimals; // error

  // generic-type-assignment-implied-cast
  List<Animal> myAnimals1 = ellipsis();
  List<Cat> myCats1 = myAnimals1 as List<Cat>;
}
```

## runtime-checks

```dart
// Unhandled exception:
// type 'List<Animal>' is not a subtype of type 'List<Cat>' in type cast
void main() {
  List<Animal> animals = [Dog()];
  List<Cat> cats = animals as List<Cat>;
}
```

## covariant

```dart
class Animal {
  void chase(Animal x) {}
}

class Mouse extends Animal {}

class Cat extends Animal {
  @override
  void chase(covariant Mouse x) {}
}
```

## bounded

```dart
class C<T extends Iterable> {
  final T collection;
  C(this.collection);
}

void cannotRunThis() {
  // undefined_method
  var c = C(Iterable.empty()).collection;
  // c.add(2); //!analysis-issue
}

void main() {
  // add-type-arg
  var c = C<List>([]).collection;
  c.add(2);
  print(c); // [2]
}
```

## strong_analysis dart-2-note-unused-but-necessary

```dart
void main() {
  var i = 1;
  // i is dynamic in Dart 1.x
  // i is inferred as int in Dart 2
  dynamic x = 1;
  x = 'Hello';
}
```

## strong_analysis opening-example

```dart
void printInts(List<int> a) => print(a);

void main() {
  final list = []; // List<dynamic> list
  list.add(1);
  list.add('2');
  // The argument type 'List<dynamic>' can't
  // be assigned to the parameter type 'List<int>'.
  printInts(list); //!analysis-issue
}
```

## strong_analysis static-analysis-enabled

```dart
// static-analysis-enabled
void main() {
  // ignore: stable, beta, dev, invalid_assignment
  bool b = [0][0];
}
```

## strong_analysis type-inference-orig

```dart
// type-inference-orig
void main() {
  Map<String, dynamic> arguments = {'argA': 'hello', 'argB': 42};
  // ignore: stable, beta, dev, argument_type_not_assignable
  arguments[1] = null;

  Map<String, dynamic> message = {
    'method': 'someMethod',
    'args': <Map<String, dynamic>>[arguments],
  };
}
```

## strong_analysis type-inference

```dart
void main() {
  Map<String, List<dynamic>> foo = {};
  // List<dynamic>? arguments
  var arguments = foo['args'];
}
```

## strong_analysis local-var-type-inference-error

```dart
void main() {
  // x is inferred as an int.
  var x = 3;
  // ignore: stable, beta, dev, stable, dev, invalid_assignment
  x = 4.0; //!analysis-issue
}
```

## strong_analysis local-var-type-inference-ok

```dart
void main() {
  // A num can be double or int.
  num y = 3;
  y = 4.0;
}
```

## strong_analysis type-arg-inference

```dart
void main() {
  // Inferred as if you wrote <int>[].
  List<int> listOfInt = [];
  // Inferred as if you wrote <double>[3.0].
  var listOfDouble = [3.0];
  // Inferred as Iterable<int>.
  var ints = listOfDouble.map((x) => x.toInt());
  // ignore: stable, beta, dev, invalid_assignment
  listOfDouble[0] = '';
}
```

## common_fixes_analysis canvas-undefined

```dart
import 'dart:html';

void main() {
  final double x = 0;
  final double y = 0;
  
  var canvas = querySelector('canvas')!;
  // ignore: stable, beta, dev, undefined_getter
  canvas.context2D.lineTo(x, y); //!analysis-issue
}
```

## common_fixes_analysis canvas-as

```dart
import 'dart:html';

void main() {
  final double x = 0;
  final double y = 0;
  
  var canvas = querySelector('canvas') as CanvasElement;
  canvas.context2D.lineTo(x, y);
}
```

## common_fixes_analysis canvas-dynamic

```dart
import 'dart:html';

void main() {
  dynamic canvasOrImg = querySelector('canvas, img');
  var width = canvasOrImg.width; // dynamic width
}
```

## common_fixes_analysis inferred-collection-types

```dart
void main() {
  // Inferred as Map<String, int>
  var map = {'a': 1, 'b': 2, 'c': 3};
  // ignore: stable, beta, dev, invalid_assignment
  map['d'] = 1.5; //!analysis-issue
  
  // ok
  var m = <String, num>{'a': 1, 'b': 2, 'c': 3};
  m['d'] = 1.5;
}
```

## common_fixes_analysis invalid-method-override

```dart
abstract class NumberAdder {
  num add(num a, num b);
}

// invalid-method-override
class MyAdder extends NumberAdder {
  @override
  // ignore: stable, beta, dev, invalid_override
  num add(int a, int b) => a + b; // error
}

// runtime-failure
void main() {
  NumberAdder adder = MyAdder();
  adder.add(1.2, 3.4);
}
```

## common_fixes_analysis type-arguments

```dart
class Superclass<T> {
  void method(T param) {}
}

class Subclass extends Superclass {
  @override
  // ignore: stable, beta, dev, invalid_override
  void method(int param) {}
}
```

## common_fixes_analysis super-goes-last

```dart
class Eats {}

abstract class Animal {
  Animal(Eats food);
}

class _HoneyBadger extends Animal {
  final String _name;

  // super-goes-last
  _HoneyBadger(Eats food, String name)
      // ignore: stable, beta, dev, super_invocation_not_last
      : super(food),
        _name = name {}
}

class HoneyBadger extends Animal {
  final String _name;

  // super-goes-last-ok
  HoneyBadger(Eats food, String name)
      : _name = name,
        super(food) {}
}
```

## common_fixes_analysis func-fail

```dart
void funcFail() {
  void filterValues(bool Function(dynamic) filter) {}
  // ignore: stable, beta, dev, argument_type_not_assignable
  filterValues((String x) => x.contains('hello')); // error
}

void funcT() {
  void filterValues<T>(bool Function(T) filter) {}
  filterValues((String x) => x.contains('hello')); // ok
  filterValues<String>((x) => x.contains('hello')); // ok
}

void funcCast() {
  void filterValues(bool Function(dynamic) filter) {}
  filterValues((x) => (x as String).contains('hello'));
}
```

## common_fixes_analysis type-inf-null

```dart
void infNull() {
  var ints = [1, 2, 3];
  // ignore: non_bool_operand, undefined_operator, return_of_invalid_type_from_closure
  var maximumOrNull = ints.fold(null, (a, b) => a == null || a < b ? b : a);
}

void infFix() {
  var ints = [1, 2, 3];
  var maximumOrNull =
      ints.fold<int?>(null, (a, b) => a == null || a < b ? b : a);
}
```

## instantiate-to-bound sanity

```dart
class B<S extends int, T> {
  String get typeOfS => '$S';
  String get typeOfT => '$T';
}

void main() {
  final b = B();
  print(b.typeOfS); // int
  print(b.typeOfT); // dynamic
}
```

# Html

## querySelector

```dart
import 'dart:html';

void main() {
  // Find an element by id (an-id).
  Element idElement = querySelector('#an-id')!;
  // Find an element by class (a-class).
  Element classElement = querySelector('.a-class')!;
  // Find all elements by tag (<div>).
  List<Element> divElements = querySelectorAll('div');
  // Find all text inputs.
  List<Element> textInputElements = querySelectorAll(
    'input[type="text"]',
  );
  // Find all elements with the CSS class 'class'
  // inside of a <p> that is inside an element with
  // the ID 'id'.
  List<Element> specialParagraphElements = querySelectorAll(
    '#id p.class',
  );
}
```

## attributes

```dart
import 'dart:html';

void main() {
  Element elem = querySelector('#an-id')!;
  elem.attributes['someAttribute'] = 'someValue';
}
```

## creating-elements

```dart
import 'dart:html';

void main() {
  var elem = ParagraphElement();
  elem.text = 'Creating is easy!';
}
```

## html

```dart
import 'dart:html';

void main() {
  // creating-elements
  var elem = ParagraphElement();
  elem.text = 'Creating is easy!';
  // creating-from-html
  var elem2 = Element.html(
    '<p>Creating <em>is</em> easy!</p>',
  );
  // body-children-add
  document.body!.children.add(elem2);
  // nodes-add
  querySelector('#inputs')!.nodes.add(elem);
  // replaceWith
  querySelector('#status')!.replaceWith(elem);
  // remove
  // Find a node by ID, and remove it
  // from the DOM if it is found.
  querySelector('#expendable')?.remove();
}
```

## classes-add

```dart
import 'dart:html';

void main() {
  var elem = querySelector('#message')!;
  elem.classes.add('warning');
}
```

## set-id

```dart
import 'dart:html';

void main() {
  var message = DivElement();
  message.id = 'message2';
  message.text = 'Please subscribe to the Dart mailing list.';
}
```

## elem-set-cascade

```dart
void main() {
  var message = DivElement()
    ..id = 'message2'
    ..text = 'Please subscribe to the Dart mailing list.';
  // set-style
  message.style
    ..fontWeight = 'bold'
    ..fontSize = '3em';
}
```

## onClick

```dart
import 'dart:html';

void main() {
  void submitData() {}
  // Find a button by ID and add an event handler.
  querySelector('#submitInfo')!.onClick.listen((event) {
    // When the button is clicked, it runs this code.
    submitData();
  });
}
```

## target

```dart
import 'dart:html';

void main() {
  document.body!.onClick.listen((event) {
    final clickedElem = event.target;
  });
}
```

## try-getString

```dart
import 'dart:html';

Future<void> tryGetString() async {
  String jsonUri = 'data.json';
  final url = 'https://httpbin.org';
  try {
    await HttpRequest.getString(jsonUri);
    String pageHtml = await HttpRequest.getString(url);
    // Process data...
  } catch (e) {
    // Handle exception...
  }
}
```

## new-HttpRequest

```dart
import 'dart:html';

void main() {
  var encodedData = 'encoded data';
  var url = 'random-url';

  void requestComplete(HttpRequest req) {}
  var request = HttpRequest();
  request
    ..open('POST', url)
    ..onLoadEnd.listen((event) {
      requestComplete(request);
    })
    ..send(encodedData);
}
```

## href

```dart
import 'dart:html';

void main() {
  final html = '<a id="example" href="/another/example">link text</a>';
  document.body!.appendHtml(html);
  var anchor = querySelector('#example') as AnchorElement;
  print(anchor.href); // endsWith('/another/example')
  anchor.href = 'https://dart.dev';
}
```

## os-html

```dart
import 'dart:html';

void main() {
  const html = '''<!-- In HTML: -->
    <p>
      <span class="linux">Words for Linux</span>
      <span class="macos">Words for Mac</span>
      <span class="windows">Words for Windows</span>
    </p>''';
  document.body!.appendHtml(html);
  String determineUserOs() => 'linux';
  const osList = ['macos', 'windows', 'linux'];
  final userOs = determineUserOs();
  // For each possible OS...
  for (final os in osList) {
    // Matches user OS?
    bool shouldShow = (os == userOs);
    // Find all elements with class=os. For example, if
    // os == 'windows', call querySelectorAll('.windows')
    // to find all elements with the class "windows".
    // Note that '.$os' uses string interpolation.
    for (final elem in querySelectorAll('.$os')) {
      elem.hidden = !shouldShow; // Show or hide.
    }
  }
}
```

## request

```dart
import 'dart:html';

void main() {
  final url = 'https://httpbin.org/headers';
  Future<void> request() async {
    HttpRequest req = await HttpRequest.request(
      url,
      method: 'HEAD',
    );
    if (req.status == 200) {
      // Successful URL access...
    }
  }
  request();
}
```

## POST

```dart
import 'dart:html';

void main() {
  const url = 'https://httpbin.org/post';
  String encodeMap(Map<String, String> data) {
    return data.entries
        .map((e) =>
            '${Uri.encodeComponent(e.key)}=${Uri.encodeComponent(e.value)}')
        .join('&');
  }

  void test() async {
    const data = {'dart': 'fun', 'angular': 'productive'};
    var request = HttpRequest();
    request
      ..open('POST', url)
      ..setRequestHeader(
        'Content-type',
        'application/x-www-form-urlencoded',
      )
      ..send(encodeMap(data));
    await request.onLoadEnd.first;
    if (request.status == 200) {
      // Successful URL access...
    }
  }
}
```

## WebSocket

```dart
import 'dart:async';
import 'dart:html';

class Logger {
  final List<String> _log = [];

  List<String> get log => List.from(_log);
  void clear() => _log.clear();
  void print(Object o) => _log.add(o.toString());

  @override
  String toString() => _log.join('\n');
}

void main() {
  final logger = Logger();
  final print = logger.print; // shadow global print
  final wsStream = StreamController<String>();

  var ws = WebSocket('ws://echo.websocket.org');

  void initWebSocket([int retrySeconds = 1]) {
    var reconnectScheduled = false;
    print('Connecting to websocket');

    void scheduleReconnect() {
      if (!reconnectScheduled) {
        Timer(Duration(seconds: retrySeconds),
                () => initWebSocket(retrySeconds * 2));
      }
      reconnectScheduled = true;
    }

    ws.onOpen.listen((e) {
      print('Connected');
      ws.send('Hello from Dart!');
    });
    ws.onClose.listen((e) {
      print('Websocket closed, retrying in $retrySeconds seconds');
      scheduleReconnect();
    });
    ws.onError.listen((e) {
      print('Error connecting to ws');
      scheduleReconnect();
    });
    ws.onMessage.listen((MessageEvent e) {
      print('Received message: ${e.data}');
      wsStream.add(('Received message'));
    });
  }

  final t = wsStream.stream.timeout(
    const Duration(seconds: 5),
    onTimeout: (s) => s.add('Timeout!'),
  );

  // Under heavy loads we don't get a response,
  // so let's accept the possibility of a timeout.
  try {
    initWebSocket();
    t.first; // 'Received message' || 'Timeout'
  } catch (e) {
    print(e);
  } finally {
    wsStream.close();
  }
}
```

# Create Libraries

```
lib
 ├── hw_mp.dart
 └── src
     ├── hw_html.dart
     ├── hw_io.dart
     └── hw_none.dart
```

> lib/hw_mp.dart

```dart
/// A multi-platform Hello World library.
library hw_mp;

// #docregion export
export 'src/hw_none.dart' // Stub implementation
    if (dart.library.io) 'src/hw_io.dart' // dart:io implementation
    if (dart.library.html) 'src/hw_html.dart'; // dart:html implementation
```

> lib/src/hw_html.dart

```dart
import 'dart:html';

void alarm([String? text]) {
  window.alert(text ?? message);
}

String get message => 'Hello World from JavaScript!';
```

> lib/src/hw_io.dart

```dart
import 'dart:io';

void alarm([String? text]) {
  stderr.writeln(text ?? message);
}

String get message => 'Hello World from the VM!';
```

```dart
void alarm([String? text]) => throw UnsupportedError('hw_none alarm');

String get message => throw UnsupportedError('hw_none message');
```

# Iterables

## any

```dart
void any(Iterable<String> items, Function(String) print) {
  if (items.any((item) => item.contains('Z'))) {
    print('At least one item contains "Z"');
  } else {
    print('No item contains "Z"');
  }
}

void main() {
  var items = ['Zoo', 'Home'];
  any(items, (s) => print(s));
}
```

## every

```dart
bool bad(Iterable<String> items) {
  for (final item in items) {
    if (item.length < 5) {
      return false;
    }
  }
  return true;
}

bool good(Iterable<String> items) {
  return items.every((item) => item.length >= 5);
}

void main() {
  print(good(['12345'])); // true
}
```

## any-every

```dart
void main() {
  const items = ['Salad', 'Popcorn', 'Toast'];

  if (items.any((item) => item.contains('a'))) {
    print('At least one item contains "a"');
  }

  if (items.every((item) => item.length >= 5)) {
    print('All items have length >= 5');
  }
}
```

## firstWhere

```dart
void main() {
  const iterable = ['a', '123456', 'abcdef'];
  String element = iterable.firstWhere((element) => element.length > 5);
  print(element); // 123456
}
```

## first-where-long

```dart
bool predicate(String item) {
  return item.length > 5;
}

void main() {
  const items = ['Salad', 'Popcorn', 'Toast', 'Lasagne'];
  // You can find with a simple expression:
  var foundItem1 = items.firstWhere((item) => item.length > 5);
  print(foundItem1); // Popcorn

  // Or try using a function block:
  var foundItem2 = items.firstWhere((item) {
    return item.length > 5;
  });
  print(foundItem2); // Popcorn

  // Or even pass in a function reference:
  var foundItem3 = items.firstWhere(predicate);
  print(foundItem3); // Popcorn

  // You can also use an `orElse` function in case no value is found!
  var foundItem4 = items.firstWhere(
    (item) => item.length > 10,
    orElse: () => 'None!',
  );
  print(foundItem4); // None!
}
```

## elementAt

```dart
void main() {
  Iterable<int> iterable = [1, 2, 3];
  int value = iterable.elementAt(1);
  print(value); // 2
}
```

## map-int

```dart
void main() {
  final numbers = [1, 2, 3];
  Iterable<int> output = numbers.map((e) => e * 10);
  print(output); // (10, 20, 30)
}
```

## map-string

```dart
void main() {
  final numbers = [1, 2, 3];
  Iterable<String> output = numbers.map((e) => e.toString());
  print(output); // (1, 2, 3)
}
```

## take-while

```dart
void main() {
  const numbers = [1, 2, 3, -1, 4, 5];
  var numbersUntilNegative = numbers.takeWhile((e) => !e.isNegative);
  print(numbersUntilNegative); // (1, 2, 3)
}
```

## take-while-long skipWhile

```dart
void main() {
  const numbers = [1, 3, -2, 0, 4, 5];
  var numbersUntilZero = numbers.takeWhile((number) => number != 0);
  print('Numbers until 0: $numbersUntilZero'); // (1, 3, -2)

  var numbersStartingAtZero = numbers.skipWhile((number) => number!=0);
  print('Numbers starting at 0: $numbersStartingAtZero'); // (0, 4, 5)
}
```

## where

```dart
void main() {
  final numbers = [1, 2, 3, 4];
  var evenNumbers = numbers.where((number) => number.isEven);
  for (final number in evenNumbers) {
    print('$number is even');
  }
}
```

## for-in

```dart
void main() {
  const iterable = ['Salad', 'Popcorn', 'Toast'];
  for (final element in iterable) {
    print(element);
  }
}
```

## first-last

```dart
void main() {
  Iterable<String> iterable = const ['Salad', 'Popcorn', 'Toast'];
  print('The first element is ${iterable.first}');
  print('The last element is ${iterable.last}');
}
```

## numbers-where

```dart
void main() {
  var evenNumbers = const [1, -2, 3, 42].where((number) => number.isEven);
  for (final number in evenNumbers) {
    print('$number is even.');
  }
  if (evenNumbers.any((number) => number.isNegative)) {
    print('evenNumbers contains negative numbers.');
  }
  // If no element satisfies the predicate, the output is empty.
  var largeNumbers = evenNumbers.where((number) => number > 1000);
  if (largeNumbers.isEmpty) {
    print('largeNumbers is empty!');
  }
}
```














































































# Function

## pass function

```dart
import 'package:flutter/material.dart';

typedef Hello<T> = void Function(T value);

class PassFunction extends StatelessWidget {
  const PassFunction({super.key, required this.onTest, required this.hello});

  final Function(int) onTest;
  final Hello<String> hello;

  @override
  Widget build(BuildContext context) {
    return OutlinedButton(
      onPressed: () {
        onTest(512);
        hello('你好');
      },
      child: const Text('click'),
    );
  }
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: PassFunction(
          onTest: (i) {
            print(i); // 512
          },
          hello: (String text) {
            print(text); // 你好
          },
        ),
      ),
    );
  }
}

void main() => runApp(const App());
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

## sync

```dart
import 'dart:io';

String obtainFilename(Map<String, dynamic> data) => 'file name';

int parseFileData(String contents) => 42;

Future<int> parseAndRead(Map<String, dynamic> data) {
  final filename = obtainFilename(data); // Could throw.
  final file = File(filename);
  return file.readAsString().then((contents) {
    return parseFileData(contents); // Could throw.
  });
}

Future<int> parseAndRead1(Map<String, dynamic> data) {
  return Future.sync(() {
    final filename = obtainFilename(data); // Could throw.
    final file = File(filename);
    return file.readAsString().then((contents) {
      return parseFileData(contents); // Could throw.
    });
  });
}

void main() {
  final Map<String, dynamic> data = {};
  parseAndRead(data).catchError((e) {
    print('Inside catchError');
    print(e);
    return -1;
  });
  // Inside catchError
  // PathNotFoundException: Cannot open file,
  // path = 'file name' (OS Error: No such file
  // or directory, errno = 2)
}

Never ellipsis<T>() => throw Exception('!');
int someFunc() => 42;

Function fragileFunc() {
  return Future.sync(() {
    final x = someFunc(); // Unexpectedly throws in some rare cases.
    var y = 10 / x; // x should not equal 0.
    ellipsis();
  });
}
```

## delayed

```dart
void main() async {
  print(1);
  await Future.delayed(Duration(milliseconds: 1000));
  print(2);
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


## async_example

```dart
Future<String> fetchUserOrder() {
  // Imagine that this function is more complex and slow.
  return Future.delayed(Duration(seconds: 4), () => 'Large Latte');
}

Future<void> printOrderMessage() async {
  print('Awaiting user order...');
  var order = await fetchUserOrder();
  print('Your order is: $order');
}

// You can ignore this function -
// it's here to visualize delay time in this example.
void countSeconds(int s) {
  for (var i = 1; i <= s; i++) {
    Future.delayed(Duration(seconds: i), () => print(i));
  }
}

void main() async {
  countSeconds(4);
  await printOrderMessage();
  // Awaiting user order...
  // 1
  // 2
  // 3
  // 4
  // Your order is: Large Latte
}
```

## async

```dart
// sync
String lookUpVersionSync() => '1.0.0';

Future<String> lookUpVersion() async => '1.0.0';

Future<void> checkVersion() async {
  var version = await lookUpVersion();
}

Future<void> tryCatch() async {
  String version;
  try {
    version = await lookUpVersion();
  } catch (e) {
    // React to inability to look up the version
  }
}

Future<void> repeatedAwait() async {
  Future<dynamic> findEntryPoint() async => Never;
  Future<dynamic> flushThenExit(_) async => Never;
  Future<dynamic> runExecutable(_, dynamic) async => Never;
  dynamic args;
  var entrypoint = await findEntryPoint();
  var exitCode = await runExecutable(entrypoint, args);
  await flushThenExit(exitCode);
}

Future<void> check() async {}

void main() async {
  check();
  print('In main: version is ${await lookUpVersion()}');
}

Stream<dynamic> requestServer = Stream.empty();
Future<dynamic> handleRequest(_) async => Never;

void numberThinker() async {
  // ...
  await for (final request in requestServer) {
    handleRequest(request);
  }
  // ...
}

Future<void> awaitFor() async {
  <varOrType>(Stream<varOrType> expression) async {
    // ignore: prefer_final_in_for_each
    await for (varOrType identifier in expression) {
      // Executes each time the stream emits a value.
    }
  };
}
```

## futures_intro

```dart
Future<void> fetchUserOrder() {
  // Imagine that this function is fetching
  // user info from another service or database.
  return Future.delayed(Duration(seconds: 2), () => print('Large Latte'));
}

Future<void> fetchUserOrderError() {
  // Imagine that this function is fetching
  // user info but encounters a bug
  return Future.delayed(Duration(seconds: 2),
          () => throw Exception('Logout failed: user ID is invalid'));
}

void process() {
  fetchUserOrder();
  print('Fetching user order...');
  // Fetching user order...
  // Large Latte
}

void main() {
  Future.wait([
    Future.delayed(Duration(seconds: 4)),
    Future.sync(process),
  ]);
}
```

## try_catch

```dart
Future<String> fetchUserOrder() {
  // Imagine that this function is more complex.
  var str = Future.delayed(
      const Duration(seconds: 4),
      // ignore: only_throw_errors
      () => throw 'Cannot locate user order');
  return str;
}

Future<void> printOrderMessage() async {
  try {
    print('Awaiting user order...');
    var order = await fetchUserOrder();
    print(order);
  } catch (err) {
    print('Caught error: $err');
  }
}

void main() async {
  await printOrderMessage();
  // Awaiting user order...
  // Caught error: Cannot locate user order
}
```

# Package http

## buildUris

```dart
void main() {
  // Parse the entire URI, including the scheme
  Uri.parse('https://dart.dev/f/packages/http.json');
  // Specifically create a URI with the https scheme
  Uri.https('dart.dev', '/f/packages/http.json');
}
```

## read

```dart
import 'package:http/http.dart' as http;

void main() async {
  final httpPackageUrl = Uri.https('dart.dev', '/f/packages/http.json');
  final httpPackageInfo = await http.read(httpPackageUrl);
  print(httpPackageInfo);
}
// {
//   "name": "http",
//   "latestVersion": "0.13.5",
//   "description": "A composable, multi-platform, Future-based API for HTTP requests.",
//   "publisher": "dart.dev",
//   "repository": "https://github.com/dart-lang/http"
// }
```

## get

```dart
import 'package:http/http.dart' as http;

void main() async {
  final httpPackageUrl = Uri.https('dart.dev', '/f/packages/http.json');
  final httpPackageResponse = await http.get(httpPackageUrl);
  if (httpPackageResponse.statusCode != 200) {
    print('Failed to retrieve the http package!');
    return;
  }
  print(httpPackageResponse.body);
}
// {
//   "name": "http",
//   "latestVersion": "0.13.5",
//   "description": "A composable, multi-platform, Future-based API for HTTP requests.",
//   "publisher": "dart.dev",
//   "repository": "https://github.com/dart-lang/http"
// }
```

## headers

```dart
import 'package:http/http.dart' as http;

void headers() async {
  await http.get(
    Uri.https('dart.dev', '/f/packages/http.json'),
    headers: {'User-Agent': '<product name>/<product-version>'},
  );
}
```

## json-decode

```dart
import 'dart:convert';

import 'package:http/http.dart' as http;

void main() async {
  final httpPackageUrl = Uri.https('dart.dev', '/f/packages/http.json');
  final httpPackageInfo = await http.read(httpPackageUrl);
  final httpPackageJson = json.decode(httpPackageInfo) as Map<String, dynamic>;
  print(httpPackageJson);
}
// {name: http, latestVersion: 0.13.5, 
// description: A composable, multi-platform, 
// Future-based API for HTTP requests., 
// publisher: dart.dev, 
// repository: https://github.com/dart-lang/http}
```

## http-client

```dart
import 'package:http/http.dart' as http;

void main() async {
  final httpPackageUrl = Uri.https('dart.dev', '/f/packages/http.json');
  final client = http.Client();
  try {
    final httpPackageInfo = await client.read(httpPackageUrl);
    print(httpPackageInfo);
  } finally {
    client.close();
  }
}
// {
//   "name": "http",
//   "latestVersion": "0.13.5",
//   "description": "A composable, multi-platform, Future-based API for HTTP requests.",
//   "publisher": "dart.dev",
//   "repository": "https://github.com/dart-lang/http"
// }
```

## http-retry

```dart
import 'package:http/http.dart' as http;
import 'package:http/retry.dart';

void main() async {
  final httpPackageUrl = Uri.https('dart.dev', '/f/packages/http.json');
  final client = RetryClient(http.Client());
  try {
    final httpPackageInfo = await client.read(httpPackageUrl);
    print(httpPackageInfo);
  } finally {
    client.close();
  }
}
// {
//   "name": "http",
//   "latestVersion": "0.13.5",
//   "description": "A composable, multi-platform, Future-based API for HTTP requests.",
//   "publisher": "dart.dev",
//   "repository": "https://github.com/dart-lang/http"
// }
```

## fetch_http_package

```dart
import 'dart:convert';

import 'package:http/http.dart' as http;

void main() async {
  await printPackageInformation('http');
  print('');
  await printPackageInformation('path');
}
// Information about the http package:
// Latest version: 0.13.5
// Description: A composable, multi-platform, Future-based API for HTTP requests.
// Publisher: dart.dev
// Repository: https://github.com/dart-lang/http
//
// Information about the path package:
// Latest version: 1.8.3
// Description: A string-based path manipulation library with cross-platform support.
// Publisher: dart.dev
// Repository: https://github.com/dart-lang/path

Future<void> printPackageInformation(String packageName) async {
  final PackageInfo packageInfo;

  try {
    packageInfo = await getPackage(packageName);
  } on PackageRetrievalException catch (e) {
    print(e);
    return;
  }

  print('Information about the $packageName package:');
  print('Latest version: ${packageInfo.latestVersion}');
  print('Description: ${packageInfo.description}');
  print('Publisher: ${packageInfo.publisher}');

  final repository = packageInfo.repository;
  if (repository != null) {
    print('Repository: $repository');
  }
}

Future<PackageInfo> getPackage(String packageName) async {
  final packageUrl = Uri.https('dart.dev', '/f/packages/$packageName.json');
  final packageResponse = await http.get(packageUrl);

  // If the request didn't succeed, throw an exception
  if (packageResponse.statusCode != 200) {
    throw PackageRetrievalException(
      packageName: packageName,
      statusCode: packageResponse.statusCode,
    );
  }

  final packageJson = json.decode(packageResponse.body) as Map<String, dynamic>;

  return PackageInfo.fromJson(packageJson);
}

class PackageInfo {
  final String name;
  final String latestVersion;
  final String description;
  final String publisher;
  final Uri? repository;

  PackageInfo({
    required this.name,
    required this.latestVersion,
    required this.description,
    required this.publisher,
    this.repository,
  });

  factory PackageInfo.fromJson(Map<String, dynamic> json) {
    final repository = json['repository'] as String?;

    return PackageInfo(
      name: json['name'] as String,
      latestVersion: json['latestVersion'] as String,
      description: json['description'] as String,
      publisher: json['publisher'] as String,
      repository: repository != null ? Uri.tryParse(repository) : null,
    );
  }
}

class PackageRetrievalException implements Exception {
  final String packageName;
  final int? statusCode;

  PackageRetrievalException({required this.packageName, this.statusCode});

  @override
  String toString() {
    final buf = StringBuffer();
    buf.write('Failed to retrieve package:$packageName information');

    if (statusCode != null) {
      buf.write(' with a status code of $statusCode');
    }

    buf.write('!');
    return buf.toString();
  }
}
```
















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










