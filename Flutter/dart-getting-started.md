# Overview
try Dart here:
https://dartpad.dartlang.org/

Dart looks like the combination of Java and JavaScript


# [Sample Code](https://www.dartlang.org/samples)
Go though the Dart code and maybe you would have a straight image about Dart.

Here we don't go deep.
## Hello World
```
main() {
  print('Hello, World!');
}
```

## Variables
Type inference makes us don't need explicit types

Just like JavaScript.

```
var name = 'hello world';
var year = 1234;
var doubleNum = 3.7;
var stringArray = ['Jan', 'Feb', 'Mar'];
var image = {
  'tag': ['haha', 'xixi'],
  'url': 'http://sample.com'
}
```

## Control flow statements
Same as most of Programming languages.
```
for (var object in stringArray) {
  print(object);
}
```

## Function
old-fashion way:
```
int fibonacci(int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```
Though Dart has type inference, google still recommend that specifying the type of each function's arguments and return value.

we could use => for functions that contain a single statement, very useful when passing anonymous functions as arguments
```
flybyObjects.where((name) => name.contains('turn')).forEach(print);
```
- anonymous function
- use a function 'print' as a argument to forEach

## Imports
To access APIs defined in other libraries, use import.
```
To access APIs defined in other libraries, use import.

// Importing core libraries
import 'dart:math';

// Importing libraries from external packages
import 'package:test/test.dart';

// Importing files
import 'path/to/my_other_file.dart';
```

## Class
Named constructor is interesting, but no idea which situation need this.

Still, it's better for us to specify the member variables type.
```
class Spacecraft {
  String name;
  DateTime launchDate;

  // Constructor, with syntactic sugar for assignment to members.
  Spacecraft(name, launchDate) {
    this.name = name;
    this.launchDate = launchDate;
    // Initialization code goes here.
  }

  // Named constructor
  Spacecraft.unlaunched(String name) {
    this.name = name;
  }
  Spacecraft.unlaunched2(String name) : this(name, null);


  int get launchYear => launchDate?.year; // read-only non-final property
}
```
Single inheritance. just like Java.

## Mixins
a way of reusing code in multiple class hierarchies. a class could act as a mixin
```
class Piloted {
  int astronauts = 1;
  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}

class PilotedCraft extends Spacecraft with Piloted {
  // ···
}
```

## Interfaces and abstract classes
Dart has no interface keyword, but all classes implicitly define an interface.
```
class MockSpaceship implements Spacecraft {
  // ···
}

abstract class Describable {
  void describe();

  void describeWithEmphasis() {
    print('=========');
    describe();
    print('=========');
  }
}
```

## Async
avoid callback hell, make your code much more readable by using async and await.
```
const oneSecond = Duration(seconds: 1);
// with async and await
Future<void> printWithDelay(String message) async {
  await Future.delayed(oneSecond);
  print(message);
}

// without
Future<void> printWithDelay(String message) {
  return Future.delayed(oneSecond).then((_) {
    print(message);
  });
}
```

need to learn more about Future, Stream, await for, aysnc*

## Exceptions
just use 'throw' as Java.
keyword: try-on-catch-finally

# [Details of Dart](https://www.dartlang.org/guides/language/language-tour)

## [From Java to Dart](https://codelabs.developers.google.com/codelabs/from-java-to-dart/#0)
TL;DR


## A basic Dart program
```
// Define a function.
printInteger(int aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
main() {
  var number = 42; // Declare and initialize a variable.
  printInteger(number); // Call a function.
}
```
string could be '...' or "..."

$variableName or ${expression}

## [Important concepts](https://www.dartlang.org/guides/language/language-tour#important-concepts)
- Everything you can place in a variable is an object, and every object is an instance of a class. Even numbers, functions, and null are objects. All objects inherit from the Object class
- Although Dart is strongly typed, type annotations are optional because Dart can infer types
- Dart supports top-level functions (such as main()), as well as functions tied to a class or object (static and instance methods, respectively)
  * Comparing with java, you have to define a function in a class.
- Unlike Java, Dart doesn’t have the keywords public, protected, and private. If an identifier starts with an underscore ( _ ), it’s private to its library.

## Keywords
cheat sheet is here:
https://www.dartlang.org/guides/language/language-tour#keywords

## [Variables](https://www.dartlang.org/guides/language/language-tour#variables)
For local variables, you could use var directly rather than type annotations.
If an object isn’t restricted to a single type, specify the Object or dynamic type
```
dynamic name = 'Bob';
Object name = 'Bob';
```
### Default value
Uninitialized variables hava an initial value of *null*.
```
int lineCount;
assert(lineCount == null);
```
even numeric types are initially null, since numbers are also Object in Dart.
### Final and const
A final variable can be set only once, it is initialized the first time it’s used.;

A const variable is a compile-time constant. (Const variables are implicitly final.)

> Instance variables can be final but not const. Final instance variables must be initialized before the constructor body starts — at the variable declaration, by a constructor parameter, or in the constructor’s initializer list.

Notice that Dart has initializer list, which like C++.

If the const variable is at the `class level`, mark it `static const`.

## [Built-in types](https://www.dartlang.org/guides/language/language-tour#built-in-types)
### Numbers
int, double.

```
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```
### Strings
both "" and '' could be used.

put value into string by using ${expression}, for identifier, you could skip {}

create a multi-line String by triple quote
```
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```

raw String by 'r'
```
var s = r'In a raw string, not even \n gets special treatment.';
```

Literal string are compile-time constants.
```
// These work in a const string.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// These do NOT work in a const string.
var aNum = 0;
var aBool = true;
var aString = 'a string';
const aConstList = [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString'; // OK
// const invalidConstString = '$aNum $aBool $aString $aConstList'; // NO
```
### Booleans
type: bool.

### Lists
In Dart, arrays are list.
```
var list = [1, 2, 3];  // type inference
List<int> list2 = [1, 2, 3];
```

To create a list that's a compile-time constant, add const before the list literal:
```
var constantList = const [1, 2, 3];
// constantList[1] = 1; // Uncommenting this causes an error.
// or
const List<int> list1 = [1, 2, 3];

```
### Maps
```
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair

const Map<int, String> constantMap = {
  2: 'helium',
  10: 'neon',
  18: 'argon'
  };

var constMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon'
};

```

### Runes
In Dart, runes are the UTF-32 code points of a string.

Dart string is a sequence of UTF-16 code units.

The usual way to express a Unicode code point is \uXXXX, where XXXX is a 4-digit hexadecimal(8-digit) value
```
Runes input = new Runes(
    '\u2665  \u{1f605}  \u{1f60e}  \u{1f47b}  \u{1f596}  \u{1f44d}');
print(new String.fromCharCodes(input));
```
### Symbols
to get the symbol ofr an identifier, use '#'
```
#radix
#bar
```
Symbol literals are compile-time constants.for APIs that refer to identifiers by name.

You might never need to use it, but it is invaluable

## [Functions](https://www.dartlang.org/guides/language/language-tour#functions)
Even functions are objects and have a type which is [Function](https://api.dartlang.org/stable/dart-core/Function-class.html)
This means that functions can be assigned to variables or passed as arguments to other functions.
```
// Though you could skip the return type and arguments type here, but Dart recommend you do add the type when you define a method.
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}

bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
// The => expr syntax is a shorthand for { return expr; }

```
A funciton can have two types of parameters: required and optional.

### Optional parameters
IMPORTANT!!!!

Optional parameters can be either positional parameters or named parameters. but not both.

optional named parameters: {param1, param2, ...}
```
// use {param1, param2, ...} to specify named parameters.
void enableFlags({bool bold, bool hidden}) {...}

enableFlags(bold: true, hidden: false);

// by add @required to a named parameters to indicate it is a required parameter.
Scrollbar({Key key, @required Widget child})
```
Flutter's widget constructor use named parameters exclusively.

optional positional parameters:
```
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

and also, you could set default parameter values:
```
// optional named parameters
void enableFlags({bool bold = false, bool hidden = false}) {...}

// optional positional parameters
String say(String from, String msg, [String device = 'carrier pigeon', String mood])

void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list:  $list');
  print('gifts: $gifts');
}
```

### The main() function
every app must have a top-level main() function.

### Functions as first-class objects
pass function as a parameter to another function:
```
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
```

### Anonymous functions
```
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';

String methodName(msg) => '!!! ${msg.toUpperCase()} !!!';
var loudify = methodName;

// Code block:
([[Type] param1[, …]]) {
  codeBlock;
};
```

### Lexical scope
skip.
### Lexical closures
skip.
### Testing functions for equality
skip.
### Return values
All functions return a value. if no return value is specified, the statement `return null;` is implicitly to the function body.

## [Operators](https://www.dartlang.org/guides/language/language-tour#operators)
if null: ??

If the boolean expression tests for null, consider using ??.
```
String playerName(String name) => name ?? 'Guest';
// if name is null, return 'Guest', otherwise return name.
```

type test: as, is, is!

### Arithmetic operators
~/: divide, returning an integer result (ignore the float part.)

### Equality and relational operators
skip.

### Type test operators
```
if (emp is Person) {
  // Type check
  emp.firstName = 'Bob';
}

(emp as Person).firstName = 'Bob';
```
Use the as operator to cast an object to a particular type. In general, you should use it as a shorthand for an is test on an object following by an expression using that object.

if emp is not a Person, code1 would do nothing, code2 would throws an exception.

### Assignment operators
To assign only if the assigned-to variable is null, use the ??= operator.
```
b ??= value;
```

### Logical operators
skip.
### Bitwise and shift operators
skip.
### Conditional expressions
> condition ? expr1 : expr2

skip.

> expr1 ?? expr2

If expr1 is non-null, returns its value; otherwise, evaluates and returns the value of expr2.

### Cascade notation (..)
Cascades (..) allow you to make a sequence of operations on the same object.
```
querySelector('#confirm') // Get an object.
  ..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
```

### Other operators
`?.` : foo?.bar selects property bar from expression foo unless foo is null

## Control flow statements
### If and else
just same as Java.
### For loops
Using forEach() is a good option if you don’t need to know the current iteration counter:

Iterable classes such as List and Set also support the for-in form of iteration:
```
var collection = [0, 1, 2];
for (var x in collection) {
  print(x); // 0 1 2
}
```

### While and do-while
skip.
### Break and continue
skip.
### Switch and case
skip.
### Assert
Assert statements have no effect in production code, they are for development only.

## Exceptions
In contrast to Java, all Dart exceptions are unchecked exceptions(which means can not be checked when compile).
### Throw
Production-quality code usually throws types that implement `Error` or `Exception`.

### Catch
Catching, or capturing, an exception stops the exception from propagating
```
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) { // catch(e, s): s means Stack trace.
  // No specified type, handles all
  print('Something really unknown: $e');
}
```
rethrow.

### Finally
```
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```

## Classes
### Using class members
Use ?. instead of . to avoid an exception when the leftmost operand is null:

### Using constructors
Constructor names can be either ClassName or ClassName.identifier.
```
var p1 = Point(2, 2);
var p2 = Point.fromJson({'x': 1, 'y': 2});

//same as
var p1 = new Point(2, 2);
var p2 = new Point.fromJson({'x': 1, 'y': 2});
```
The new keyword became optional in Dart 2.

[constant constructors](https://www.dartlang.org/guides/language/language-tour#constant-constructors):
To create a compile-time constant using a constant constructor, put the const keyword before the constructor name:
```
var p = const ImmutablePoint(2, 2);

// Lots of const keywords here.
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};

// Only one const, which establishes the constant context.
// The const keyword became optional within a constant context in Dart 2.
const pointAndLine = {
  'point': [ImmutablePoint(0, 0)],
  'line': [ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
```

If a constant constructor is outside of a constant context and is invoked without const, it creates a non-constant object:
```
var a = const ImmutablePoint(1, 1); // Creates a constant
var b = ImmutablePoint(1, 1); // Does NOT create a constant

assert(!identical(a, b)); // NOT the same instance!
```



### Getting an object’s type
you can use Object’s runtimeType property
```
print('The type of a is ${a.runtimeType}');
```

### Instance variables
All uninitialized instance variables have the value null.

All instance variables generate an implicit getter method. Non-final instance variables also generate an implicit setter method.

If you initialize an instance variable where it is declared (instead of in a constructor or method), the value is set when the instance is created, which is before the constructor and its initializer list execute.

### [Constructors](https://www.dartlang.org/guides/language/language-tour#constructors)
Use `this` only when there is a name conflict

Syntactic sugar:
```
class Point {
  num x, y;

  // Syntactic sugar for setting x and y
  // before the constructor body runs.
  Point(this.x, this.y);
}
```

You can't create two or more constructors with same names but different arguments.

Dart takes these same name constructors as one default constructor.
```
class Person {
  String name;
  bool male;
  Person.make(String name) {
    this.name = name;
    this.male = true;
  }

  //Error here because 'The constructor with name make is already defined.'
  Person.make(String name, bool male) {
    this.name = name;
    this.male = male;
  }

  Person(String name, bool male) {
    this.name = name;
    this.male = male;
  }

  // Error here because the default constructor is already defined.
  Person():name = "Default", male = true {}
}
```

#### Constructors aren't inherited
Subclasses don’t inherit constructors from their superclass.

A subclass that declares no constructors has only the default (no argument, no name) constructor.
If you declare any constructor, then the default constructor won't be generated.

#### Named constructors
```
class Point {
  num x, y;

  Point(this.x, this.y);

  // Named constructor
  Point.origin() {
    x = 0;
    y = 0;
  }
}
```
Remember that constructors are not inherited, which means that a superclass’s named constructor is not inherited by a subclass. If you want a subclass to be created with a named constructor defined in the superclass, you must implement that constructor in the subclass.

#### Invoking a non-default superclass constructor
By default, a constructor in a subclass calls the superclass’s unnamed, no-argument constructor.
In summary, the order of execution is as follows:
- initializer list
- superclass’s no-arg constructor
- main class’s no-arg constructor

If the superclass doesn’t have an unnamed, no-argument constructor, then you must manually call one of the constructors in the superclass.Specify the superclass constructor after a colon (:), just before the constructor body (if any)
```
class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

class Employee extends Person {
  Employee() : super.fromJson(getDefaultData());
  // ···
}
```

#### Initializer list
Besides invoking a superclass constructor, you can also initialize instance variables before the constructor body runs. Separate initializers with commas.
```
class Student extends Person {
  int age;
  // use Initializer list to init instance variables, and call super method.
  Student(String name, bool male, int age): age = age, super(name, male){
  }
}
```

#### Redirecting constructors
```
class Point {
  num x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  // Delegates to the main constructor.
  Point.alongXAxis(num x) : this(x, 0);
}
```

#### Constant constructors
If your class produces objects that never change, you can make these objects compile-time constants.

To do this, define a const constructor and make sure that all instance variables are final.

```
//Constant constructors
class ImmutablePoint {
  static final ImmutablePoint origin =
      const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
```

#### Factory constructors
use the `factory` keyword  when implementing a constructor that doesn't always create a new instance of its class.

For example, a factory constructor might return an instance from a cache, or it might return an instance of a subtype.
```
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache =
      <String, Logger>{};

  factory Logger(String name) {
    if (_cache.containsKey(name)) {
      return _cache[name];
    } else {
      final logger = Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```
with 'factory', your constructor could return values.

for an easy understanding, you could take the factory constructor as an ordinary function witch returns the Class instance.
```
factory Logger(String name)
//maybe equals to
Logger getLogger(String name)
```

### Methods
Getters and setters: using the get and set keywords:
```
class Rectangle {
  num left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
  num get right => left + width;
  set right(num value) => left = value - width;
  num get bottom => top + height;
  set bottom(num value) => top = value - height;
}
```

Abstract methods can only exist in abstract classes.

### Abstract classes
Abstract classes are useful for defining interfaces, often with some implementation.

If you want your abstract class to appear to be instantiable, define a factory constructor.

### Implicit interfaces
If you want to create a class A that supports class B’s API without inheriting B’s implementation, class A should implement the B interface
```
class Point implements Comparable, Location {...}
```


### Extending a class
```
class SmartTelevision extends Television {
  void turnOn() {
    // use super to refer to the superclass
    super.turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }

  // use @override annotation to indicate that you are intentionally overriding a member.
  @override
  void turnOff() {...}
  // ···
}
```

To detect or react whenever code attempts to use a non-existent method or instance variable, you can override noSuchMethod():


### Enumerated types
略
### Adding features to a class: mixins
Mixins are a way of reusing a class’s code in multiple class hierarchies.

To implement a mixin, create a class that extends Object and declares no constructors.

Unless you want your mixin to be usable as a regular class, use the mixin keyword instead of class.

More information here:https://github.com/dart-lang/language/blob/master/accepted/2.1/super-mixins/feature-specification.md#dart-2-mixin-declarations

TL,DR;

### Class variables and methods

Static variables aren’t initialized until they’re used.

## [Generics](https://www.dartlang.org/guides/language/language-tour#generics)
List<E>. The <…> notation marks List as a generic (or parameterized) type.

Seems not too difficult to understand. We take a overview here.


### Why use generics?

Generics are often required for type safety.

Generic types can save you the trouble of creating all these interfaces. Instead, you can create a single interface that takes a type parameter:
```
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

### Using collection literals
List and map literals can be parameterized.
```
var names = <String>['Seth', 'Kathy', 'Lars'];
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
```
### Using parameterized types with constructors
```
var views = Map<int, View>();

var names = List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
var nameSet = Set<String>.from(names);
```

### Generic collections and the types they contain

### Restricting the parameterized type
use extends
```
class Foo<T extends SomeBaseClass> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'";
}

class Extender extends SomeBaseClass {...}
```
### Using generic methods
```
T first<T>(List<T> ts) {
  // Do some initial work or error checking, then...
  T tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}
```
you could use the type argument T in several places:
- in the function's return type(T)
- in the type of an argument(List<T>)
- in the type of a local variable(T tmp)

## Libraries and visibility
The `import` and `library` directives can help you create a modular and shareable code base.

Libraries not only provide APIs, but are a unit of privacy: identifiers that start with an underscore ( _ ) are visible only inside the library.

Every Dart app is a library, even if it doesn’t use a library directive.

### Using libraries
```
import 'dart:html';
import 'package:test/test.dart';
```
The only required argument to `import` is a URI specifying the library.
- for built-in libraries, the URI has the special `dart:` scheme.
- for other libraries, you can use a file system path or the `package:` scheme.

> URI stands for uniform resource identifier. URLs (uniform resource locators) are a common kind of URI.

#### Specifying a library prefix
If you import two libraries that have conflicting identifiers, then you can specify a prefix for one or both libraries. For example, if library1 and library2 both have an Element class, then you might have code like this:
```
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

#### Importing only part of a library
```
// Import only foo.
import 'package:lib1/lib1.dart' show foo;

// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;
```

#### Lazily loading a library
Deferred loading (also called lazy loading) allows an application to load a library on demand, if and when it’s needed. You may need deferred loading when:
- to reduce an app's initial startup time
- to perform A/B testing - trying out alternative implementations of an algorithm.
- to load rarely used functionality, such as optional screens and dialogs.

To lazily load a library, you must first import it using `deferred as`.
```
import 'package:greetings/hello.dart' deferred as hello;
```

When you need the library, invoke loadLibrary() using the library’s identifier.
```
Future greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```

You can invoke loadLibrary() multiple times on a library without problems. The library is loaded only once.

Keep in mind when you use deffered loading:
- A deferred library’s constants aren’t constants in the importing file. Remember, these constants don’t exist until the deferred library is loaded.
- You can’t use types from a deferred library in the importing file. Instead, consider moving interface types to a library imported by both the deferred library and the importing file.
- Dart implicitly inserts loadLibrary() into the namespace that you define using deferred as namespace. The loadLibrary() function returns a Future.

### [Implementing libraries](https://www.dartlang.org/guides/libraries/create-library-packages)
Read this part carefully if you need to implement your own libraries.

## [Asynchrony support](https://www.dartlang.org/guides/language/language-tour#asynchrony-support)
Asynchronous programming often uses callback functions, but Dart provides alternatives:
- [Future](https://api.dartlang.org/stable/2.1.0/dart-async/Future-class.html) objects
- [Stream](https://api.dartlang.org/stable/2.1.0/dart-async/Stream-class.html) objects.

The `async` and `await` keywords support asynchronous programming.

### Handling Futures
To use await, code must be in an async function:
```
Future checkVersion() async {
  var version = await lookUpVersion();
  // Do something with version
}
```

You can use await multiple times in an async function.

In await expression, the value of expression is usually a Future;
if it isn’t, then the value is automatically wrapped in a Future.
This Future object indicates a promise to return an object.
The value of await expression is that returned object.
The await expression makes execution pause until that object is available.

```
// findEntrypoint() returns a Future
// await findEntrypoint() return the real object.
var entrypoint = await findEntrypoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

**If you get a compile-time error when using await, make sure await is in an async function**
```
Future main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
```

### Declaring async functions
An async function is a function whose body is marked with the async modifier.
```
String lookUpVersion() => '1.0.0';

Future<String> lookUpVersion() async => '1.0.0';
```

If your function doesn’t return a useful value, make its return type Future<void>.


### [Handling Streams](https://www.dartlang.org/guides/libraries/library-tour#stream)

When you need to get values from a Stream, you have two options:
- Use async and an asynchronous for loop (await for).
- Use the Stream API, as described in the library tour.
  * https://www.dartlang.org/guides/libraries/library-tour#stream

**Before using await for, be sure that it makes the code clearer and that you really do want to wait for all of the stream’s results.
For example, you usually should not use await for for UI event listeners, because UI frameworks send endless streams of events.**

```
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```
The value of expression must have type Stream. Execution proceeds as follows:
1. Wait until the stream emits a value.
2. Execute the body of the for loop, with the variable set to that emitted value.
3. Repeat 1 and 2 until the stream is closed.

```
Future main() async {
  // ...
  await for (var request in requestServer) {
    handleRequest(request);
  }
  // ...
}
```
**If you get a compile-time error when implementing an asynchronous for loop, make sure the await for is in an async function.**

## Generators
When you need to lazily produce a sequence of values, consider using a generator function.
- Synchronous generator: Returns an `Iterable` object.
- Asynchronous generator: Returns a `Stream` object.

To implement a synchronous generator function, mark the function body as sync*, and use yield statements to deliver values:
```
Iterable<int> naturalsTo(int n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
```

To implement an asynchronous generator function, mark the function body as async*, and use yield statements to deliver values:
```
Stream<int> asynchronousNaturalsTo(int n) async* {
  int k = 0;
  while (k < n) yield k++;
}
```

Actually it is difficult to understand this part, especially the sync*, async* and yield.
take a look at the article below if having time: https://www.dartlang.org/articles/language/beyond-async

## [Callable classes](https://www.dartlang.org/guides/language/language-tour#callable-classes)
you could treat class as a function, just by implement the call() method.

## [Isolates](https://api.dartlang.org/stable/2.1.1/dart-isolate/dart-isolate-library.html)
Instead of threads, all Dart code runs inside of isolates. Each isolate has its own memory heap, ensuring that no isolate’s state is accessible from any other isolate.

## [Typedefs](https://www.dartlang.org/guides/language/language-tour#typedefs)
This would be changed in the future, so skip it for now.

## [Metadata](https://www.dartlang.org/guides/language/language-tour#metadata)
Use metadata to give additional information about your code. A metadata annotation begins with the character `@`.

Two annotations are available to all Dart code: @deprecated and @override.

you can define your own metadata annotations.

## [Comments](https://www.dartlang.org/guides/language/language-tour#comments)
- Single-line comments
- Multi-line comments
- Documentation comments    
Begin with `///` or `/**`


here is the tips shows you how to structure your comments:
https://www.dartlang.org/guides/language/effective-dart/documentation

## Summary
TBA...

# asynchronous programming
## use then() for Future
```
HttpRequest.getString(url).then((String result) {
  print(result);
});
```

## use listen() for Stream

# [Asynchronous Programming: Futures](https://www.dartlang.org/tutorials/language/futures)

# [Asynchronous Programming: Streams](https://www.dartlang.org/tutorials/language/streams)

# [Dart Language Asynchrony Support: Phase1](https://www.dartlang.org/articles/language/await-async)
Async and await, two language features that support asynchronous programming,

# [Dart Language Asynchrony Support: Phase2](https://www.dartlang.org/articles/language/beyond-async)
Async*, sync*, yield, and yield*.

use Generators to generate a Iterable object for sync, and generate a Stream object for async.
## Synchronous generateors: sync*
```
Iterable naturalsTo(n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
```
when the function get called,
- naturalsTo immediately returns an iterable, you could extract an iterator from the iterable.
- The body of the function won’t start running until one calls moveNext on that iterator.
- It will run until it hits the yield statement the first time. The yield statement contains an expression, which it evaluates.
- Then, the function suspends, and moveNext returns true to its caller.
- The function will resume execution the next time moveNext is called.
- When the loop ends, the method implicitly executes a return, which causes it to terminate. At that point, moveNext returns false to its caller

## Asynchronous generators: async*
```
Stream asynchronousNaturalsTo(n) async* {
  int k = 0;
  while (k < n) yield k++;
}
```
- Invoking this function immediately returns a stream
- Once you listen to the stream, execution of the body begins.
- When the yield statement executes, it adds the result of evaluating its expression to the stream.
- In any event, whatever function is listening on the stream will get called with each new value at some point.

```
Stream get naturals async* {
  int k = 0; while (true) { yield await k++; }
}

await for (int i in naturals) { print(‘event loop $i’); }

```

## [Creating Streams in Dart](https://www.dartlang.org/articles/libraries/creating-streams)
Three ways:
- transforming existing streams
- creating a stream from scratch by using an async* function
- creating a stream by using a StreamController

## [Stream API](https://api.dartlang.org/stable/2.2.0/dart-async/Stream-class.html)
A Stream provides a way to receive a sequence of events.

A stream will emit its event, which something similar to a Publisher;
and you could listen on a stream to make it start generating events, and to set up listeners that receive the events.
When you listen, you receive a StreamSubscription object.

There are two kind of streams:
- single-subscription steam: allow only a single listener during the whole lifetime of the stream.
  * generally used for streaming chunks of larger contiguous data like file I/O
- broadcast stream: A broadcast stream allows any number of listeners, and it fires its events when they are ready, whether there are listeners or not.
  * Broadcast streams are used for independent events/observers


# [Effective Dart](https://www.dartlang.org/guides/language/effective-dart)

# [A Tour of the Dart Libraries](https://www.dartlang.org/guides/libraries/library-tour)

# [Commonly Used Libraries](https://www.dartlang.org/guides/libraries/useful-libraries)

# [Create Library Packges](https://www.dartlang.org/guides/libraries/create-library-packages)

# [Dart Details](https://www.dartlang.org/articles)

# [Tools for Dart](https://www.dartlang.org/tools)

# [Community and Support](https://www.dartlang.org/community)
