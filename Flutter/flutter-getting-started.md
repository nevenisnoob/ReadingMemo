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

Stateful Widget Lifecycle:
```
createState()
mounted == true
initState()
didChangeDependencies()
build()
didUpdateWidget()
setState()
deactivate()
dispose()
mounted == false
```

API reference:https://docs.flutter.io/flutter/widgets/widgets-library.html

## [User interfaces](https://flutter.io/docs/development/ui)
### Introduction to widgets
#### Hello World
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

#### Basic widgets
- Text
- Row, Column: let you create flexible layouts in both the horizontal (Row) and vertical (Column) directions
- Stack: lets you stack widgets on top of each other in paint order
- [Container](https://docs.flutter.io/flutter/widgets/Container-class.html): lets you create a rectangular visual element, A container can be decorated with a BoxDecoration

#### Using Material Components
- [MaterialApp](https://docs.flutter.io/flutter/material/MaterialApp-class.html)

#### Handling gestures
```
class MyButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        print('MyButton was tapped!');
      },
      child: Container(
        height: 36.0,
        padding: const EdgeInsets.all(8.0),
        margin: const EdgeInsets.symmetric(horizontal: 8.0),
        decoration: BoxDecoration(
          borderRadius: BorderRadius.circular(5.0),
          color: Colors.lightGreen[500],
        ),
        child: Center(
          child: Text('Engage'),
        ),
      ),
    );
  }
}
```
GestureDetector widget doesn't have a visual representation, but it could monitor all gestures which happened on its child.

more information here: https://flutter.io/docs/development/ui/advanced/gestures
- [GestureDetector](https://docs.flutter.io/flutter/widgets/GestureDetector-class.html)
- [AppBar](https://docs.flutter.io/flutter/material/AppBar-class.html)
- [Container](https://docs.flutter.io/flutter/widgets/Container-class.html)
  * tl;dr: Container tries, in order: to honor alignment, to size itself to the child, to honor the width, height, and constraints, to expand to fit the parent, to be as small as possible.
- [Center](https://docs.flutter.io/flutter/widgets/Center-class.html)
- [RaisedButton](https://docs.flutter.io/flutter/material/RaisedButton-class.html)


#### Changing widgets in response to input
you need a StatefulWidget and a State class.

You might wonder why StatefulWidget and State are separate objects. In Flutter, these two types of objects have different life cycles. Widgets are temporary objects, used to construct a presentation of the application in its current state. State objects on the other hand are persistent between calls to build(), allowing them to remember information.

Pay attention to build() method and setState() method in State class.
- if setState is called, the State class would return the build method so that the display can reflect the updated values.
- build() method in State class would be called every time setState is called.

- [StatefulWidget](https://docs.flutter.io/flutter/widgets/StatefulWidget-class.html)
- [State](https://docs.flutter.io/flutter/widgets/State-class.html)


#### [Bringing it all together](https://flutter.io/docs/development/ui/widgets-intro#bringing-it-all-together)
read this again!

try to re-implement it by using StatefulWidget
- [StatefulWidget](https://docs.flutter.io/flutter/widgets/StatefulWidget-class.html)
  * For compositions that depend only on the configuration information in the object itself and the BuildContext in which the widget is inflated, consider using StatelessWidget.
  * two types of StatefulWidget:
    + allocates resources in State.initState() and disposes of them in State.dispose(). they are built once then never update.
    + use State.setState() or depend on InheritedWidget. they would be rebuilt many times.

- [StatelessWidget](https://docs.flutter.io/flutter/widgets/StatelessWidget-class.html)
  * Stateless widget are useful when the part of the user interface you are describing does not depend on anything other than the configuration information in the object itself and the BuildContext in which the widget is inflated.


#### Responding to widget lifecycle events
- createState() is called
- flutter inserts the new state object into the tree and calls initState()
  * you could configure animations or subscribe platform services.
- when a state object is no longer needed, flutter calls state object's dispose() method.
  * you could do some cleanup work here.: cancel timers, unsubscribe platform services etc.

#### Keys
```
class ShoppingList extends StatefulWidget {
  ShoppingList({Key key, this.products}) : super(key: key);

  final List<Product> products;

  // The framework calls createState the first time a widget appears at a given
  // location in the tree. If the parent rebuilds and uses the same type of
  // widget (with the same key), the framework re-uses the State object
  // instead of creating a new State object.

  @override
  _ShoppingListState createState() => _ShoppingListState();
}
```
Keys are most useful in widgets that build many instances of the same type of widget.

A key is an identifier for Widgets.

#### Global Keys
You can use global keys to uniquely identify child widgets.

### Building layouts
#### [Layout widgets](https://flutter.io/docs/development/ui/widgets/layout)
- single-child layout widgets
  * Container: https://flutter.io/docs/development/ui/layout#container
  * Padding:
  * Center
  * Align
  * ...
- multi-child layout widgets
  * Row
  * Column
  * Stack: https://flutter.io/docs/development/ui/layout#stack
  * GridView: https://flutter.io/docs/development/ui/layout#gridview
  * ListView: https://flutter.io/docs/development/ui/layout#listview


aligning widgets by using Row/Column's MainAxisAlignment & CrossAxisAlignment
- https://docs.flutter.io/flutter/rendering/MainAxisAlignment-class.html
- https://docs.flutter.io/flutter/rendering/CrossAxisAlignment-class.html

use Expanded to re-size the Widget.
```
Row(
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    Expanded(
      child: Image.asset('images/pic1.jpg'),
    ),
    Expanded(
      flex: 2,
      child: Image.asset('images/pic2.jpg'),
    ),
    Expanded(
      child: Image.asset('images/pic3.jpg'),
    ),
  ],
);
```

use MainAxisSize.min to packing widgets.

Learn the tutorial carefully! You'll know how flutter's layout mechanism works.
https://flutter.io/docs/development/ui/layout/tutorial
1. create the app base code
2. diagram the layout
3. implement the smallest widget
4. then implement the outter/layout widget

Expanded class: A widget that expands a child of a Row, Column, or Flex.
If multiple children are expanded, the available space is divided among them according to the 'flex' factor.
Using an Expanded widget makes a child of a Row, Column, or Flex expand to fill the available space in the main axis(horizontal for a row, vertical for a Column)

Using an Flexible widget gives a child of a Row, Column, or Flex the flexibility to expand to fill the available space in the main axis.
unlike Expanded, Flexible does not require the child to fill the available space.


#### [Box constraints](https://flutter.io/docs/development/ui/layout/box-constraints)
Generally, there are three kinds of render boxes
- Those that try to be as big as possible. For example, the boxes used by Center, ListView, Container
- Those that try to be the same size as their children. For example, the boxes used by Transform and Opacity.
- Those that try to be a particular size. For example, the boxes used by Image and Text.

### Adding interactivity
A stateless widget never changes. Such as Icon, IconButton, and Text etc.

A stateful widget is dynamic: for example, it can change its appearance in response to events triggered by user interactions or when it receives data. Such as Checkbox, Radio, Slider, InkWell, Form, and TextField, etc.

Members or classes that start with an underscore ( _ ) are private.

#### [Managing state](https://flutter.io/docs/development/ui/interactive#managing-state)
There are three ways to managing the states:
- the widget manage its own state
  * If the state is aesthetic, for example an animation
- the parent manages the widget's state
  * If the state is user data, for example the checked or unchecked mode of a checkbox, or the position of a slider, managing state by parent.
- a mix-and-match approach


### [Assets and images](https://flutter.io/docs/development/ui/assets-and-images)
Common types of assets include static data(json file), configuration files, icons, and images.

you could specifying assets in your pubspec.yaml file
```
flutter:
  assets:
    - assets/my_icon.png
    - assets/background.png

```

Loading assets by obtaining the AssetBundle for the current BuildContext using DefaultAssetBundle.

Outside of a Widget context, or when a handle to an AssetBundle is not available, you can use rootBundle.


### [Navigation & routing](https://flutter.io/docs/development/ui/navigation)
In Flutter, screens and pages are called `routes`.
A route equals:
- for Android, route == activity
- for iOS, route == ViewController

A route is just a widget. Use Navigator to navigate to a new route.

https://docs.flutter.io/flutter/widgets/Navigator-class.html


#### [Navigate to a new screen and back](https://flutter.io/docs/cookbook/navigation/navigation-basics)
1. Create two routes
2. Navigate to the second route using Navigator.push()
3. Return to the first route using Navigator.pop()
```
class FirstRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('First Route'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Open route'),
          onPressed: () {
            // Navigate to second route when tapped.
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondRoute()),
            );
          },
        ),
      ),
    );
  }
}
```
- Navigator.push: https://docs.flutter.io/flutter/widgets/Navigator/push.html
- MaterialPageRoute: https://docs.flutter.io/flutter/material/MaterialPageRoute-class.html
  * A modal route that replaces the entire screen with a platform-adaptive transition

#### [Send data to a new screen](https://flutter.io/docs/cookbook/navigation/passing-data)
A Todo list sample, which meets the needs of news app.

```
ListView.builder(
  itemCount: todos.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(todos[index].title),
      // When a user taps on the ListTile, navigate to the DetailScreen.
      // Notice that we're not only creating a DetailScreen, we're
      // also passing the current todo to it!
      onTap: () {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => DetailScreen(todo: todos[index]),
          ),
        );
      },
    );
  },
);
```

#### [Return data from a screen](https://flutter.io/docs/cookbook/navigation/returning-data)
Navigator.pop accepts an optional second argument called result. If we provide a result, it will be returned to the Future in our SelectionButton!

```
// A method that launches the SelectionScreen and awaits the result from
// Navigator.pop!
_navigateAndDisplaySelection(BuildContext context) async {
  // Navigator.push returns a Future that will complete after we call
  // Navigator.pop on the Selection Screen!
  final result = await Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => SelectionScreen()),
  );

  // After the Selection Screen returns a result, hide any previous snackbars
  // and show the new result!
  Scaffold.of(context)
    ..removeCurrentSnackBar()
    ..showSnackBar(SnackBar(content: Text("$result")));
}

//blablabla...
RaisedButton(
  onPressed: () {
    // Our Nope button will return "Nope!" as the result
    Navigator.pop(context, 'Nope!');
  },
  child: Text('Nope!'),
);
```
Notice that we use the async/await to receive result.

#### [Navigate with named routes](https://flutter.io/docs/cookbook/navigation/named-routes)
```
class FirstScreen extends StatelessWidget {...}

class SecondScreen extends StatelessWidget {...}

MaterialApp(
  // Start the app with the "/" named route. In our case, the app will start
  // on the FirstScreen Widget
  initialRoute: '/',
  routes: {
    // When we navigate to the "/" route, build the FirstScreen Widget
    '/': (context) => FirstScreen(),
    // When we navigate to the "/second" route, build the SecondScreen Widget
    '/second': (context) => SecondScreen(),
  },
);

// Within the `FirstScreen` Widget
onPressed: () {
  // Navigate to the second screen using a named route
  Navigator.pushNamed(context, '/second');
}


```
- The initialRoute property defines which route our app should start with.
- The routes property defines the available named routes and the Widgets that should be built when we navigate to those routes



#### [Animating a widget across screens](https://flutter.io/docs/cookbook/navigation/hero-animations)
Hero widget allows us to animate a widget from on screen to the next.
https://docs.flutter.io/flutter/widgets/Hero-class.html

1. create two screens showing the same image
2. add a Hero widget to the first screen
3. add a Hero widget to the second screen

the Hero.tag must be same.
```
Hero(
  tag: 'imageHero',
  child: Image.network(
    'https://picsum.photos/250?image=9',
  ),
);
```
That's it.

### Animations
```
├── Animatable
│   └── Tween
├── Listenable
│   └── Animation
│       ├── AnimationController
│       └── CurvedAnimation
└── TickerProvider
```

Animationをさせたい場合、注意しなければならないのは
- 最初のUIデザイン時点で、画面構成をちゃんと考えなければならない
  * AppBar付きの画面は、Flutterが提供しているScaffold widgetを使うのはめっちゃ便利ですが、後からAnimationを追加することになると、描画領域の制限がかかられ、やりづらくなる
- Animation付きのWidgetは、基本的に StatefulWidgetとして作成されます。
  * Animationさせる際の、座標、幅などもStateですので
  * この際のState管理は、親Widgetではなく、自分で管理することになる
- 重要なクラス
  * Animation
  * AnimationController
  * Tween
  * TickerProvider
- WidgetにAnimationをつける手順
  * 画面のどのWidgetに、どんなAnimationをつけるのかを頭の中にイメージする
  * そのようなAnimationさせるには、どうやって分解する？
    + x軸、y軸、透明度、横幅、縦幅...
  * AnimationControllerで、Animationの続く時間、Animation Stateを管理する
    + 在AnimationController的Listener里调用setState来进行重绘
  * 分解されたそれぞれのwidget propertyに、Animationを作り、AnimationControllerと関連をつける
  * Tweenを使って、さらにAnimationを生成する
  * AnimationControllerを使ってAnimationをさせる
- その他
  * GobalKeyを使って、別のWidgetからあるWidgetを呼び出せる

AnimatedWidget/AnimatedBuilderを使えば、Animationの実装が楽になれる



#### [Animation and motion widgets](https://flutter.dev/docs/development/ui/widgets/animation)

#### [Study Resources]
- https://blog.csdn.net/hekaiyou/article/details/72259392
  * 一共七篇，由浅入深，值得一看。


### Advanced UI
#### pixel
https://docs.flutter.io/flutter/dart-ui/Window/devicePixelRatio.html
The Flutter framework operates in logical pixels.

By definition, there are roughly 38 logical pixels per centimeter, or about 96 logical pixels per inch, of the physical display.

#### Slivers

#### Gestures

### Widget catalog

## Data & backend
### [State management](https://flutter.dev/docs/development/data-and-backend/state-mgmt/intro)

Ephemeral state(UI State or local State):
- current page in a PageView
- current progress of a complex animation
- current selected tab in a BottomNavigationBar

for this kind of local state, there is no need to use state management techniques(ScopedModel, Redux, etc.)

App State:
- User preferences
- Login info
- Notifications in a social networking app
- The shopping cart in an e-commerce app
- Read/unread state of articles in a news app

ScopedModel is the widget that provides an instance of Model to its descendants.



### [Json and serialization](https://flutter.dev/docs/development/data-and-backend/json)
In Flutter, encoding and serialization are the same thing—turning a data structure into a string. Decoding and deserialization are the opposite process—turning a string into a data structure.


## Accessibility & internationalization

## Platform integration

関連情報
- [Add flutter to existing apps](https://github.com/flutter/flutter/wiki/Add-Flutter-to-existing-apps)

- Use MethodChannel for Flutter -> Native direction.
- Use EventChannel for Native -> Flutter direction.
  * [iOS Native主动和Flutter通信](https://juejin.im/post/5c133919e51d4524851c67e3)
  * [google sample](https://github.com/flutter/flutter/tree/master/examples/platform_channel)


## Packages & plugins

## Tools & optimization

# [Flutter Cookbook](https://flutter.io/docs/cookbook)
demonstrate how to solve common problems while writing Flutter apps.

# Flutter apps architecture
前書きGoogleのMVPサンプル：https://github.com/googlesamples/android-architecture/tree/todo-mvp/

## [Flutter architecture: implement MVP pattern](https://medium.com/flutterpub/flutter-architecture-implement-a-mvp-pattern-8ab78b75f2d4)
## [Flutter architecture samples](https://github.com/brianegan/flutter_architecture_samples)
## [Discussion on Architecure patterns for flutter](https://www.reddit.com/r/FlutterDev/comments/7niro1/architecture_patterns_for_flutter/)
## [Flutter + MVC at Last](https://medium.com/flutter-community/flutter-mvc-at-last-275a0dc1e730)
## [Flutter redux app framework](https://github.com/alibaba/fish-redux)
https://juejin.im/entry/5c7f6516518825408f707ae7

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
## [Dart GC](https://juejin.im/post/5c7e0c255188250a432388d8)
## [How Flutter use Widgets, Elements, and RenderObjects to create delicious eye-candy at 120fps](https://medium.com/flutter-community/the-layer-cake-widgets-elements-renderobjects-7644c3142401)
- 中文翻译: https://www.jianshu.com/p/8e714a204898

- Widget Tree
- Element Tree
- RenderObject Tree

每一个Element中都有着相对应的Widget和RenderObject的引用.

RenderObject中包含了所有用来渲染实例Widget的逻辑。它负责layout、painting和hit-testing。它的生成十分耗费性能，所以我们应该尽可能的缓存它

Element是存在于可变Widget树和不可变RenderObject树之间的桥梁。Element擅长比较两个Object，在Flutter里面就是Widget和RenderObject。它的作用是配置好Widget在树中的位置，并且保持对于相对应的RenderObject和Widget的引用。

当Widget树改变的时候，Flutter使用Element树来比较新的Widget树和原来的RenderObject树。如果某一个位置的Widget和RenderObject类型不一致，才需要重新创建RenderObject。如果其他位置的Widget和RenderObject类型一致，则只需要修改RenderObject的配置，不用进行耗费性能的RenderObject的实例化工作了。因为Widget是非常轻量级的，实例化耗费的性能很少，所以它是描述APP的状态（也就是configuration）的最好工具。

因为Widget是不可变的，当某个Widget的配置改变的时候，整个Widget树都需要被重建。例如当我们改变一个Container的颜色为红色的时候，框架就会触发一个重建整个Widget树的动作。然后在Element的帮助下，Flutter比较新的Widget树中的第一个Widget类型和RenderObject树中第一个RenderObject的类型。接下来比较Widget树中第二个Widget和RenderObject树中第二个RenderObject的类型，以此类推，直到Widget树和RendObject树比较完成。

Flutter遵循一个最基本的原则：判断新的Widget和老的Widget是否是同一个类型。
如果不是同一个类型，那就把Widget、Element、RenderObject分别从它们的树（包括它们的子树）上移除，然后创建新的对象。
如果是一个类型，那就仅仅修改RenderObject中的配置，然后继续向下遍历。
这个过程是非常快的，因为Flutter非常擅长创建那些轻量级的Widgets。



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

# その他開発し始まる前に見といたほうが良さそうな情報
- [Style guide for Flutter repo](https://github.com/flutter/flutter/wiki/Style-guide-for-Flutter-repo)


# 個人感想
If mobile OS updates and introduces new widgets(UI widgets) and you are using flutter, you have to wait the Flutter team to support the new widgets.
But if mobile OS updates and introduces new platform capabilities, you could use Flutter's interop and plugin system to access new mobile OS features and capabilities immediately.

- When to use StatefulWidget or StatelessWidget?
  * for StatefulWidget, it could generate data by itself?
  * for StatelessWidget, data need to be passed to it？

- Widget render tree???

- when you see a widget tree, you should be able to draw the UI.
  * https://flutter.io/docs/development/ui/layout#nesting-rows-and-columns
    + for you to practice

- How to manage state???
  * https://flutter.io/docs/development/ui/interactive#managing-state

- the difference of Expanded and Flexible
  * https://stackoverflow.com/a/52904214/7701713

- [Flutter Layout Cheat Sheet](https://medium.com/flutter-community/flutter-layout-cheat-sheet-5363348d037e)

- [The Power of WebViews in Flutter](https://medium.com/flutter-io/the-power-of-webviews-in-flutter-a56234b57df2)

- Figure out State's lifecycle is VERY important!!!!!!!!!!!!!!
  * https://docs.flutter.io/flutter/widgets/State-class.html
