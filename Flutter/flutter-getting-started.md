# Overview
## [Flutter FAQ](https://flutter.io/docs/resources/faq)
- Flutter use neither WebView nor the OEM widgets stat shipped with the device. Flutter uses its own high-performance engine to draw widgets
- IDE: AndroidStudio, IntelliJ IDEA, VS Code
- Flutter ships with a modern framework, inspired by React. Flutter's framework is designed to be layered and customizable. Developers can choose to use only parts of the framework, or a different framework.
- Flutter ships with a set of high quality Material Design and Cupertino(iOS-style) widget, layouts, and themes. You could create your own widgets, or customize the existing widgets.
- You could use flutter inside of your existing native app(but not fully optimized).
- No reflection/mirrors system in Flutter for now.

### what Flutter SDK provides?
- Heavily optimized, mobile-first 2D rendering engine with excellent support for text
- Modern react-style framework
- Rich set of widgets for Android and iOS
- APIs for unit and integration tests
- Interop and plugin APIs to connect to the system and 3rd-party SDKs
- Headless test runner for running tests on Windows, Linux, and Mac
- Command-line tools for creating, building, testing, and compiling your apps

### what technology is Flutter buit with?
Flutter use C, C++, Dart, and Skia(a 2D rendering engine).
Architecure Diagram: https://docs.google.com/presentation/d/1cw7A4HbvM_Abv320rVgPVGiUP2msVs7tfGbkgdrTy0I/edit#slide=id.p

### How does Flutter run my code on Android
- The engine’s C and C++ code are compiled with Android’s NDK.
- The Dart code (both the SDK’s and yours) are ahead-of-time (AOT) compiled into a native, ARM library.
- That library is included in a “runner” Android project, and the whole thing is built into an APK
- When launched, the app loads the Flutter library.
- Any rendering, input or event handling, and so on, are delegated to the compiled Flutter and app code
(This is similar to the way many game engines work)

### How does Flutter run my code on iOS
- The engine’s C and C++ code are compiled with LLVM
- The Dart code (both the SDK’s and yours) are ahead-of-time (AOT) compiled into a native, ARM library.
- That library is included in a “runner” iOS project, and the whole thing is built into an .ipa
- When launched, the app loads the Flutter library.
- Any rendering, input or event handling, and so on, are delegated to the compiled Flutter and app code.

### Does Flutter use my system's OEM widgets?
NO. If flutter reused OEM widgets, the quality and performance of Flutter apps would be limited by them.
Modern app design trends point towards designers and users wanting more motion-rich UIs and brand-first designs.
In order to achieve that level of customized, beautiful design, Flutter is architectured to drive pixels instead of the OEM widgets.

### Why Flutter choose Dart?
TL;DR
https://flutter.io/docs/resources/faq#why-did-flutter-choose-to-use-dart

### Hot reload is useful
Hot reload means the app state is retained after a reload.

### Can I access platform services and APIs like sensors and local storage?
Yes. Flutter encourage develpers to use Flutter's asynchronous message passing system to create your own integration with playtform and third-party APIs.

### [What programming paradigm does Flutter’s framework use?](https://flutter.io/docs/resources/faq#what-programming-paradigm-does-flutters-framework-use)
- Composition: using small objects with narrow scopes of behavior, composed together to obtain more complicated effects.
- Functional programming: For example, the Icon widget is essentially a function that maps its arguments (color, icon, size) into layout primitives. Additionally, heavy use is made of immutable data structures, including the entire Widget class hierarchy as well as numerous supporting classes such as Rect and TextStyle. On a smaller scale, Dart’s Iterable API, which makes heavy use of the functional style (map, reduce, where, etc), is frequently used to process lists of values in the framework
- Event-driven programming: User interactions are represented by event objects that are dispatched to callbacks registered with event handlers.The Listenable class, which is used as the basis of the animation system, formalizes a subscription model for events with multiple listeners
- Class-based object-oriented programming
- Prototype-based object-oriented programming:
- Imperative programming:
- Reactive programming:
- Declarative programming: The build methods of widgets are often a single expression with multiple levels of nested constructors, written using a strictly declarative subset of Dart.
- Generic programming: Types can be used to help developers catch programming errors early.
- Concurrent programming: Flutter makes heavy use of Futures and other asynchronous APIs.
- Constraint programming: The layout system in Flutter uses a weak form of constraint programming to determine the geometry of a scene.


## [Flutter Technical overview](https://flutter.io/docs/resources/technical-overview)
### Why Flutter?
- be highly productive
- create beautiful, highly-customized user experiences.

### Core principles

#### Everything is a Widget
Composition > inheritance
Container, a commonly-used widget, is made up of several widgets responsible for layout, painting, positioning, and sizing
https://flutter.io/docs/resources/technical-overview#composition--inheritance

#### Building widgets
You define the unique characteristics of a widget by implementing a build function that returns a tree (or hierarchy) of widgets.
A widget’s build function should be free of side effects.


#### Handling user interaction


# [Get Started](https://flutter.io/docs/get-started/)
This section would guide you to
- install Flutter SDK
- write a hello world app in AndroidStudio(or other IDE)
- Run app on both iOS and Android simulator & devices
Before all, get to know Dart please.

A widget’s main job is to provide a build() method that describes how to display the widget in terms of other, lower level widgets.

Stateless widgets are immutable, meaning that their properties can’t change—all values are final.

Stateful widgets maintain state that might change during the lifetime of the widget. Implementing a stateful widget requires at least two classes:
- a StatefulWidget class that creates an instance of
- a State class.

## [Flutter for Android devs](https://flutter.io/docs/get-started/flutter-for/android-devs)

### animation
https://flutter.io/docs/development/ui/animations/tutorial
https://flutter.io/docs/development/ui/animations

### Navigator and Route
A Route is an abstraction for a “screen” or “page” of an app, and a Navigator is a widget that manages routes.

Flutter use Navigator and Route to navigate between screens.

### Handle incoming intents from external apps
1. we first handle the shared text data on the Android native side (in our Activity
2. then wait until Flutter requests for the data to provide it using a MethodChannel


### runOnUiThread?
Dart has a single-threaded execution model, with support for Isolates (a way to run Dart code on another thread), an event loop, and asynchronous programming.
For Flutter, you could just use async/await to perform asynchronous work.

### background thread?
Since Flutter is single threaded and runs an event loop (like Node.js), you don’t have to worry about thread management or spawning background threads.
If you’re doing I/O-bound work, such as disk access or a network call, then you can safely use async/await and you’re all set.
If, on the other hand, you need to do computationally intensive work that keeps the CPU busy, you want to move it to an Isolate to avoid blocking the event loop.

Just use async/await or Isolate.

### show progress for a long-running task
use a ProgressIndicator widget

### the place you store image files
Assets are located in any arbitrary folder—Flutter has no predefined folder structure. You declare the assets (with location) in the pubspec.yaml file, and Flutter picks them up

### localization
https://pub.dartlang.org/packages/intl

### [lifecycle](https://flutter.io/docs/get-started/flutter-for/android-devs#how-do-i-listen-to-android-activity-lifecycle-events)
https://docs.flutter.io/flutter/dart-ui/AppLifecycleState-class.html
- inactive
- paused
- resumed
- suspending

### Gesture detection and touch event Handling
If the Widget doesn’t support event detection, wrap the widget in a GestureDetector and pass a function to the onTap parameter.
- onTapDown
- onTap
- ...
- onDoubleTap
- onLongPress
- onVerticalDragStart
- ...
- onHorizontalDragStart
- ...

### ListViews & Adapters
The recommended, efficient, and effective way to build a list uses a ListView.Builder.
This method is great when you have a dynamic List or a List with very large amounts of data.
This is essentially the equivalent of RecyclerView on Android, which automatically recycles list elements for you:

### Flutter plugins
- [geolocator](https://pub.dartlang.org/packages/geolocator) for access the GPS sensor
- [image_picker](https://pub.dartlang.org/packages/image_picker) for accessing camera

## [Flutter for iOS devs](https://flutter.io/docs/get-started/flutter-for/ios-devs)
TL;DR

### [Declarative UI](https://flutter.io/docs/get-started/flutter-for/declarative)
- Imperative Style used by many other UI frameworks:
you manually construct a full-functioned UI entity, such as a UIView or equivalent, and later mutate it using methods and setters when the UI changes

- Declarative Style used by Flutter:
In order to lighten the burden on developers from having to program how to transition between various UI states, Flutter, by contrast, lets the developer describe the current UI state and leaves the transitioning to the framework





# [Development](https://flutter.io/docs/development)

## User interfaces
### Hello World
```
import 'package:flutter/material.dart';

void main() {
  runApp(
    Center(
      child: Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```
runApp function taks a widget as argument.
Here, the widget tree consists of two widgets, Center and Text.

### Basic widgets
- Text
- Row, Column: let you create flexible layouts in both the horizontal (Row) and vertical (Column) directions
- Stack: lets you stack widgets on top of each other in paint order
- [Container](https://docs.flutter.io/flutter/widgets/Container-class.html): lets you create a rectangular visual element, A container can be decorated with a BoxDecoration
### Using Material Components
- [MaterialApp](https://docs.flutter.io/flutter/material/MaterialApp-class.html)


### Handling gestures
### Changing widgets in response to input
### Bringing it all together
### Responding to widget lifecycle events
### Keys
### Global Keys

## Data & backend

## Accessibility & internationalization

## Platform integration

## Packages & plugins

## Tools & optimization

# [Flutter Cookbook](https://flutter.io/docs/cookbook)
demonstrate how to solve common problems while writing Flutter apps.

# Flutter apps architecture
前書きGoogleのMVPサンプル：https://github.com/googlesamples/android-architecture/tree/todo-mvp/

## [Flutter architecture: implement MVP pattern](https://medium.com/flutterpub/flutter-architecture-implement-a-mvp-pattern-8ab78b75f2d4)
## [Flutter architecture samples](https://github.com/brianegan/flutter_architecture_samples)
## [Discussion on Architecure patterns for flutter](https://www.reddit.com/r/FlutterDev/comments/7niro1/architecture_patterns_for_flutter/)

# Testing & optimization
## [Debugging](https://flutter.io/docs/testing/debugging)
## [Using OEM debuggers](https://flutter.io/docs/testing/oem-debuggers)
## [Flutter's build modes](https://flutter.io/docs/testing/build-modes)
## [Testing](https://flutter.io/docs/testing)
## [Performance best practices](https://flutter.io/docs/testing/best-practices)
## [Performance profiling](https://flutter.io/docs/testing/ui-performance)


# Technical details
## [Inside Flutter](https://flutter.io/docs/resources/inside-flutter)
## [Why Flutter doesn't use OEM widgets](https://medium.com/flutter-io/why-flutter-doesnt-use-oem-widgets-94746e812510)


# Flutter Handbook
## [Flutter API reference](https://docs.flutter.io/)
## [Flutter widget index](https://flutter.io/docs/reference/widgets)
## [Flutter packages](https://pub.dartlang.org/flutter)

## Deployment
開発段階ではこちら無視しても良い
### [creating flavors for flutter](https://flutter.io/docs/deployment/flavors)
### [build and release for Android](https://flutter.io/docs/deployment/android)
### [build and release for iOS](https://flutter.io/docs/deployment/ios)
### [continuous deployment with fastlane](https://flutter.io/docs/deployment/fastlane-cd)

# Study Resources
## [Udacity online flutter training](https://www.udacity.com/course/build-native-mobile-apps-with-flutter--ud905)
## [Flutter codelabs](https://flutter.io/docs/codelabs)
## [Flutter samples on github](https://github.com/flutter/samples/blob/master/INDEX.md)


# 個人感想
## デメリット
If mobile OS updates and introduces new widgets(UI widgets) and you are using flutter, you have to wait the Flutter team to support the new widgets.
But if mobile OS updates and introduces new platform capabilities, you could use Flutter's interop and plugin system to access new mobile OS features and capabilities immediately.
