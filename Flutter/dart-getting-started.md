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

constant constructors: To create a compile-time constant using a constant constructor, put the const keyword before the constructor name:
```
var p = const ImmutablePoint(2, 2);

// Lots of const keywords here.
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};

// Only one const, which establishes the constant context.
const pointAndLine = {
  'point': [ImmutablePoint(0, 0)],
  'line': [ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
```

### Getting an object’s type
you can use Object’s runtimeType property

### Instance variables
All uninitialized instance variables have the value null.

All instance variables generate an implicit getter method. Non-final instance variables also generate an implicit setter method.

If you initialize an instance variable where it is declared (instead of in a constructor or method), the value is set when the instance is created, which is before the constructor and its initializer list execute.

### [Constructors](https://www.dartlang.org/guides/language/language-tour#constructors)
Use `this` only when there is a name conflict

Subclasses don’t inherit constructors from their superclass

Remember that constructors are not inherited, which means that a superclass’s named constructor is not inherited by a subclass. If you want a subclass to be created with a named constructor defined in the superclass, you must implement that constructor in the subclass.

By default, a constructor in a subclass calls the superclass’s unnamed, no-argument constructor.
In summary, the order of execution is as follows:
- initializer list
- superclass’s no-arg constructor
- main class’s no-arg constructor

If the superclass doesn’t have an unnamed, no-argument constructor, then you must manually call one of the constructors in the superclass.Specify the superclass constructor after a colon (:), just before the constructor body (if any)

Initializer list
Besides invoking a superclass constructor, you can also initialize instance variables before the constructor body runs. Separate initializers with commas.

- Default constructor
  * The default constructor has no arguments and invokes the no-argument constructor in the superclass.
- Named constructor
- Initializer list
- Redirecting constructors
- Constant constructors
  * If your class produces objects that never change, you can make these objects compile-time constants.
  * To do this, define a const constructor and make sure that all instance variables are final.
- Factory constructors


```
class Point {
  num x, y;

  // Syntactic sugar for setting x and y
  // before the constructor body runs.
  Point(this.x, this.y);

  // Named constructor
  Point.origin() {
    x = 0;
    y = 0;
  }
}

// Initializer list sets instance variables before
// the constructor body runs.
Point.fromJson(Map<String, num> json)
    : x = json['x'],
      y = json['y'] {
  print('In Point.fromJson(): ($x, $y)');
}

class Point {
  num x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  //Redirecting constructors, body is empty
  // Delegates to the main constructor.
  Point.alongXAxis(num x) : this(x, 0);
}

class Person {
  String firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

//Constant constructors
class ImmutablePoint {
  static final ImmutablePoint origin =
      const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
```

### Methods
### Abstract classes
### Implicit interfaces
### Extending a class
### Enumerated types
### Adding features to a class: mixins
### Class variables and methods

## Generics
### Why use generics?
### Using collection literals
### Using parameterized types with constructors
### Generic collections and the types they contain
### Restricting the parameterized type
### Using generic methods

## Libraries and visibility
### Using libraries
### Implementing libraries

## Asynchrony support
### Handling Futures
### Declaring async functions
### Handling Streams

## Generators

## Callable classes

## Isolates

## Typedefs

## Metadata

## Comments
### Single-line comments
### Multi-line comments
### Documentation comments

## Summary


# [Asynchronous Programming: Futures](https://www.dartlang.org/tutorials/language/futures)

# [Asynchronous Programming: Streams](https://www.dartlang.org/tutorials/language/streams)

# [Effective Dart](https://www.dartlang.org/guides/language/effective-dart)

# [A Tour of the Dart Libraries](https://www.dartlang.org/guides/libraries/library-tour)

# [Commonly Used Libraries](https://www.dartlang.org/guides/libraries/useful-libraries)

# [Create Library Packges](https://www.dartlang.org/guides/libraries/create-library-packages)

# [Dart Details](https://www.dartlang.org/articles)

# [Tools for Dart](https://www.dartlang.org/tools)

# [Community and Support](https://www.dartlang.org/community)
