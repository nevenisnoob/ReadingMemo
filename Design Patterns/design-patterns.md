# 個人メモ
**1.7. How to select a design pattern** 何度も読むこと

# Guide to Readers
Design patterns is devided into three types: creational, structural, and behavioral.

We could start with the simplest and most common patterns:
- Abstract Factory
- Adapter
- Composite
- Decorator
- Factory Method
- Observer
- Strategy
- Template Method

# Chapter 1. Introduction
## 1.1 What Is a Design Pattern?
In general, a pattern has four essential elements:
1. The **pattern name** is a handle we can use to describe a design problem, its solutions, and consequences in a word or two.
2. The **problem** describes when to apply the pattern. It explains the problem and its context.
3. The **solution** describes the elements that make up the design, their relationships, responsibilities, and collaborations. Instead, the pattern provides an abstract description of a design problem and how a general arrangement of elements (classes and objects in our case) solves it.
4. The **consequences** are the results and trade-offs of applying the pattern. Though consequences are often unvoiced when we describe design decisions, they are critical for evaluating design alternatives and for understanding the costs and benefits of applying the pattern.

## 1.2 Design Patterns in Smalltalk MVC
MVC decouples views and models by establishing a subscribe/notify protocol between them. A view must ensure that its appearance reflects the state of the model. Whenever the model’s data changes, the model notifies views that depend on it. This more general design is described by the **Observer (page 293) design pattern**.

Another feature of MVC is that views can be nested. This more general design is described by the **Composite (163) design pattern**.

The View-Controller relationship is an example of the **Strategy (315) design pattern**. A Strategy is an object that represents an algorithm. It’s useful when you want to replace the algorithm either statically or dynamically, when you have a lot of variants of the algorithm, or when the algorithm has complex data structures that you want to encapsulate. MVC uses other design patterns, such as **Factory Method** (107) to specify the default controller class for a view and **Decorator (175)** to add scrolling to a view.

**The main relationships in MVC are given by the Observer, Composite, and Strategy design patterns**.

## 1.3 Describing design patterns
- Pattern name and Classification
- Intent
  * What does the design pattern do?
  * What is its rationale and intent?
  * What particular design issue or problem does it address?
- Also known as
Other well-known names for the pattern,
- Motivation
A scenario that illustrates a design problem and how the class and object structures in the pattern solve the problem.
- Applicability
  * What are the situations in which the design pattern can be applied?
  * What are examples of poor designs that the pattern can address?
  * How can you recognize these situations?
- Structure
A graphical representation of the classes in the pattern
- Participants
The classes and/or objects participating in the design pattern and their responsibilities.
- Collaborations
How the participants collaborate to carry out their responsibilities.
- Consequences
  * How does the pattern support its objectives?
  * What are the trade-offs and results of using the pattern?
  * What aspect of system structure does it let you vary independently?
- Implementation
What pitfalls, hints, or techniques should you be aware of when implementing the pattern?
- Sample Code
- Known Uses
Examples of the pattern found in real systems.
- Related Patterns
  * What design patterns are closely related to this one?
  * What are the important differences?
  * With which other patterns should this one be used?

## 1.4　&　1.5 The Catelog of Design Patterns/Organizing the catelog
### Creational
#### Class scope
- Factory Method (107) Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

#### Object scope
- Abstract Factory (87) Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
- Builder (97) Separate the construction of a complex object from its representation so that the same construction process can create different representations.
- Prototype (117) Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
- Singleton (127) Ensure a class only has one instance, and provide a global point of access to it.

### Structural
#### Class scope
- Adapter (139) Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.

#### Object scope
- Adapter (139) Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.
- Bridge (151) Decouple an abstraction from its implementation so that the two can vary independently.
- Composite (163) Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.
- Decorator (175) Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.
- Facade (185) Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.
- Flyweight (195) Use sharing to support large numbers of fine-grained objects efficiently.
- Proxy (207) Provide a surrogate or placeholder for another object to control access to it.

### Behavioral
#### Class scope
- Interpreter (243) Given a language, define a represention for its grammar along with an interpreter that uses the representation to interpret sentences in the language.
- Method (325) Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm’s structure.

#### Object scope
- Chain of Responsibility (223) Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.
- Command (233) Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.
- Iterator (257) Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
- Mediator (273) Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.
- Memento (283) Without violating encapsulation, capture and externalize an object’s internal state so that the object can be restored to this state later.
- Observer (293) Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
- State (305) Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.
- Strategy (315) Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
- Template
- Visitor (331) Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

## 1.6 How design patterns solve design problems
- Finding appropriate objects    
The hard part about object-oriented design is decomposing a system into objects. The task is difficult because many factors come into play: **encapsulation, granularity, dependency, flexibility, performance, evolution, reusability, and on and on**.

- Determining object granularity    
Objects can vary tremendously in size and number. They can represent everything down to the hardware or all the way up to entire applications. Design patterns tell  us the way to decide what should be an object

- Specifying object interfaces    
Every operation declared by an object specifies the operation’s name, the objects it takes as parameters, and the operation’s return value. This is known as the operation’s signature. The set of all signatures defined by an object’s operations is called the **interface** to the object.    
**Dynamic binding**.

- Specifying object implementations    
Class. The class specifies the object’s internal data and representation and defines the operations the object can perform.    
Objects are created by **instantiating** a class.    
The object is said to be an **instance** of the class.    
**Class inheritance**.
> Programming to an Interface, not an Implementation

- Putting reuse mechanisms to work
**Inheritance versus Composition**    
Delegation is a way of making composition as powerful for reuse as inheritance. In delegation, two objects are involved in handling a request: a receiving object delegates operations to its delegate.    
Another (not strictly object-oriented) technique for reusing functionality is through parameterized types, also known as templates(C++)

- Relating run-time and compile-time structures    
Consider the distinction between object **aggregation** and **acquaintance** and how differently they manifest themselves at compile- and run-times. Aggregation implies that one object owns or is responsible for another object. Generally we speak of an object having or being part of another object. Aggregation implies that an aggregate object and its owner have identical lifetimes. Acquaintance implies that an object merely knows of another object. Sometimes acquaintance is called “association” or the “using” relationship.

- **Designing for change**    
Here are some common causes of redesign:
  * Creating an object by specifying a class explicitly. Specifying a class name when you create an object commits you to a particular implementation instead of a particular interface. This commitment can complicate future changes. To avoid it, create objects indirectly.
    + Design patterns: Abstract Factory (87), Factory Method (107), Prototype (117).
  * Dependence on specific operations. When you specify a particular operation, you commit to one way of satisfying a request. By avoiding hard-coded requests, you make it easier to change the way a request gets satisfied both at compile-time and at run-time.
    + Design patterns: Chain of Responsibility (223), Command.
  * Dependence on hardware and software platform. External operating system interfaces and application programming interfaces (APIs) are different on different hardware and software platforms. Software that depends on a particular platform will be harder to port to other platforms. It may even be difficult to keep it up to date on its native platform. It’s important therefore to design your system to limit its platform dependencies.
    + Design patterns: Abstract Factory (87), Bridge (151).
  * Dependence on object representations or implementations. Clients that know how an object is represented, stored, located, or implemented might need to be changed when the object changes. Hiding this information from clients keeps changes from cascading.
    + Design patterns: Abstract Factory (87), Bridge (151), Memento (283), Proxy (207).
  * Algorithmic dependencies. Algorithms are often extended, optimized, and replaced during development and reuse. Objects that depend on an algorithm will have to change when the algorithm changes. Therefore algorithms that are likely to change should be isolated.
    + Design patterns: Builder (97), Iterator (257), Strategy (315), Template Method (325), Visitor (331).
  * Tight coupling. Classes that are tightly coupled are hard to reuse in isolation, since they depend on each other. Tight coupling leads to monolithic systems, where you can’t change or remove a class without understanding and changing many other classes. The system becomes a dense mass that’s hard to learn, port, and maintain. Loose coupling increases the probability that a class can be reused by itself and that a system can be learned, ported, modified, and extended more easily. Design patterns use techniques such as abstract coupling and layering to promote loosely coupled systems.
    + Design patterns: Abstract Factory (87), Bridge (151), Chain of Responsibility (223), Command (233), Facade (185), Mediator (273), Observer (293).
  * Extending functionality by subclassing. Customizing an object by subclassing often isn’t easy. Every new class has a fixed implementation overhead (initialization, finalization, etc.). Defining a subclass also requires an in-depth understanding of the parent class. For example, overriding one operation might require overriding another. An overridden operation might be required to call an inherited operation. And subclassing can lead to an explosion of classes, because you might have to introduce many new subclasses for even a simple extension.
    + Design patterns: Bridge (151), Chain of Responsibility (223), Composite (163), Decorator (175), Observer (293), Strategy (315).
  * Inability to alter classes conveniently. Sometimes you have to modify a class that can’t be modified conveniently. Perhaps you need the source code and don’t have it (as may be the case with a commercial class library). Or maybe any change would require modifying lots of existing subclasses. Design patterns offer ways to modify classes in such circumstances.
    + Design patterns: Adapter (139), Decorator (175), Visitor (331).

## 1.7 How to select a design pattern
- **Consider how design patterns solve design problems.**    
See 1.6.
- **Scan Intent sections.**    
See 1.4.
- **Study how patterns interrelate.**    
See Figure1.1 - Design pattern relationships.
- **Study patterns of like purpose.**    
See Chapter3,4,5.
- **Examine a cause of redesign.**    
See **Designing for change** in 1.6.
- **Consider what should be variable in your design.**    
See Table 1.2 - Design aspects that design patterns let you vary.

## 1.8 How to use a design pattern
- Read the pattern once through for an overview. Pay particular attention to the Applicability and Consequences sections to ensure the pattern is right for your problem.
- Go back and study the Structure, Participants, and Collaborations sections. Make sure you understand the classes and objects in the pattern and how they relate to one another.
- Look at the Sample Code section to see a concrete example of the pattern in code. Studying the code helps you learn how to implement the pattern.
- Choose names for pattern participants that are meaningful in the application context. The names for participants in design patterns are usually too abstract to appear directly in an application. Nevertheless, it’s useful to incorporate the participant name into the name that appears in the application. That helps make the pattern more explicit in the implementation. For example, if you use the Strategy pattern for a text compositing algorithm, then you might have classes SimpleLayoutStrategy or TeXLayoutStrategy.
- Define the classes. Declare their interfaces, establish their inheritance relationships, and define the instance variables that represent data and object references. Identify existing classes in your application that the pattern will affect, and modify them accordingly.
- Define application-specific names for operations in the pattern. Here again, the names generally depend on the application. Use the responsibilities and collaborations associated with each operation as a guide. Also, be consistent in your naming conventions. For example, you might use the “Create-” prefix consistently to denote a factory method.
- Implement the operations to carry out the responsibilities and collaborations in the pattern. The Implementation section offers hints to guide you in the implementation. The examples in the Sample Code section can help as well.


# Chapter 2. A Case Study: Designing a Document Editor

1. Composite (163) to represent the document’s physical structure.
2. Strategy (315) to allow different formatting algorithms.
3. Decorator (175) for embellishing the user interface.
4. Abstract Factory (87) for supporting multiple look-and-feel standards.
5. Bridge (151) to allow multiple windowing platforms.
6. Command (233) for undoable user operations.
7. Iterator (257) for accessing and traversing object structure.
8. Visitor (331) for allowing an open-ended number of analytical capabilities without complicating the document structure’s implementation.

# Chapter 3. Creational Patterns

## Abstract Factory
### Intent
Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
### Also Known As
Kit
### Motivation
Consider a user interface toolkit that supports multiple look-and-feel standards. Different look-and-feels define different appearances and behaviors for user interface “widgets” like scroll bars, windows, and buttons.

### Applicability
Use the Abstract Factory pattern when
- a system should be independent of how its products are created, composed, and represented.
- a system should be configured with one of multiple families of products.
- a family of related product objects is designed to be used together, and you need to enforce this constraint.
- you want to provide a class library of products, and you want to reveal just their interfaces, not their implementations.
### Structure
略
### Participants
- **AbstractFactory** (WidgetFactory)     
declares an interface for operations that create abstract product objects.
- **ConcreteFactory** (MotifWidgetFactory, PMWidgetFactory)    
implements the operations to create concrete product objects.
- **AbstractProduct** (Window, ScrollBar)    
declares an interface for a type of product object.
- **ConcreteProduct** (MotifWindow, MotifScrollBar)
  * defines a product object to be created by the corresponding concrete factory.
  * implements the AbstractProduct interface.
- **Client**    
uses only interfaces declared by AbstractFactory and AbstractProduct classes.

### Collaborations
- Normally a **single instance of a ConcreteFactory class is created at run-time**. This concrete factory creates product objects having a particular implementation. To create different product objects, clients should use a different concrete factory.
- AbstractFactory defers creation of product objects to its ConcreteFactory subclass.

### Consequences
Benefits and liabilities:
- It isolates concrete classes.
- It makes exchanging product families easy.
- It promotes consistency among products.
- Supporting new kinds of products is difficult.    
Extending abstract factories to produce new kinds of Products isn’t easy. That’s because the AbstractFactory interface fixes the set of products that can be created.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
AbstractFactory classes are often implemented with factory methods, but they can also be implemented using Prototype.    
A concrete factory is often a singleton.


## Builder
結構見られるので略

## Factory Method
略

## Singleton
略

## Prototype

### Intent
Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

### Motivation
We can use the Prototype pattern to reduce the number of classes even further.
### Applicability
Use the Prototype pattern when a system should be independent of how its products
are created, composed, and represented; and
- when the classes to instantiate are specified at run-time, for example, by dynamic loading; or
- to avoid building a class hierarchy of factories that parallels the class hierarchy of products; or
- when instances of a class can have one of only a few different combinations of state. It may be more convenient to install a corresponding number of prototypes and clone them rather than instantiating the class manually, each time with the appropriate state.

### Structure
略
### Participants
- Prototype (Graphic): declares an interface for cloning itself.
- ConcretePrototype (Staff, WholeNote, HalfNote): implements an operation for cloning itself.
- Client (GraphicTool): creates a new object by asking a prototype to clone itself.

### Collaborations
略
### Consequences
Benefits:
- Adding and removing products at run-time. Prototypes let you incorporate a new concrete product class into a system simply by registering a prototypical instance with the client. That’s a bit more flexible than other creational patterns, because a client can install and remove prototypes at run-time.
- Specifying new objects by varying values.
- Specifying new objects by varying structure.
- Reduced subclassing
- Configuring an application with classes dynamically.

Liability:     
each subclass of Prototype must implement the Clone operation, which may be difficult. For example, adding Clone is difficult when the classes under consideration already exist. Implementing Clone can be difficult when their internals include objects that don’t support copying or have circular references.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略


# Chapter 4. Structural Patterns
## Adapter
### Intent
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.

### Also Known As
Wrapper

### Motivation
略
### Applicability
Use the Adapter pattern when
- you want to use an existing class, and its interface does not match the one you need.
- you want to create a reusable class that cooperates with unrelated or unforeseen classes, that is, classes that don’t necessarily have compatible interfaces.
- (object adapter only) you need to use several existing subclasses, but it’s impractical to adapt their interface by subclassing every one. An object adapter can adapt the interface of its parent class.

### Structure
略
### Participants
- Target (Shape)    
defines the domain-specific interface that Client uses.
- Client (DrawingEditor)    
collaborates with objects conforming to the Target interface.
- Adaptee (TextView)    
defines an existing interface that needs adapting.
- Adapter (TextShape)    
adapts the interface of Adaptee to the Target interface.

### Collaborations
Clients call operations on an Adapter instance. In turn, the adapter calls Adaptee operations that carry out the request.

### Consequences
略
### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略


## Bridge
### Intent
Decouple an abstraction from its implementation so that the two can vary independently.
### Also Known As
Handle/Body

### Motivation
略
### Applicability
Use the Bridge pattern when
- you want to avoid a permanent binding between an abstraction and its implementation. This might be the case, for example, when the implementation must be selected or switched at run-time.
- both the abstractions and their implementations should be extensible by subclassing. In this case, the Bridge pattern lets you combine the different abstractions and implementations and extend them independently.
- changes in the implementation of an abstraction should have no impact on clients; that is, their code should not have to be recompiled.
- (C++) you want to hide the implementation of an abstraction completely from clients. In C++ the representation of a class is visible in the class interface.
- you have a proliferation of classes as shown earlier in the first Motivation diagram. Such a class hierarchy indicates the need for splitting an object into two parts. Rumbaugh uses the term “nested generalizations” [RBP+91] to refer to such class hierarchies.
- you want to share an implementation among multiple objects (perhaps using reference counting), and this fact should be hidden from the client. A simple example is Coplien’s String class, in which multiple objects can share the same string representation (StringRep).

### Structure
略
### Participants
- Abstraction (Window)    
defines the abstraction’s interface. – maintains a reference to an object of type Implementor. • RefmedAbstraction (IconWindow) – Extends the interface defined by Abstraction.
- Implementor (WindowImp)    
defines the interface for implementation classes. This interface doesn’t have to correspond exactly to Abstraction’s interface; in fact the two interfaces can be quite different. Typically the Implementor interface provides only primitive operations, and Abstraction defines higher-level operations based on these primitives.
- ConcreteImplementor (XWindowImp, PMWindowImp)    
implements the Implementor interface and defines its concrete implementation.

### Collaborations
Abstraction forwards client requests to its Implementor object.
### Consequences
- Decoupling interface and implementation.
- Improved extensibility. You can extend the Abstraction and Implementor hierarchies independently.
- Hiding implementation details from clients.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略


## Composite
### Intent
Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

### Also Known As
略
### Motivation
略
### Applicability
Use this pattern when
- you want to represent part-whole hierarchies of objects.
- you want clients to be able to ignore the difference between compositions of objects and individual objects. Clients will treat all objects in the composite structure uniformly.

### Structure
略
### Participants
- Component (Graphic)
  * declares the interface for objects in the composition.
  * implements default behavior for the interface common to all classes, as appropriate.
  * declares an interface for accessing and managing its child components.
  * (optional) defines an interface for accessing a component’s parent in the recursive structure, and implements it if that’s appropriate.
- Leaf (Rectangle, Line, Text, etc.)
  * represents leaf objects in the composition.
  * defines behavior for primitive objects in the composition.
- Composite (Picture)
  * defines behavior for components having children.
  * stores child components.
  * implements child-related operations in the Component interface.
- Client
  * manipulates objects in the composition through the Component interface.

### Collaborations
Clients use the Component class interface to interact with objects in the composite structure. If the recipient is a Leaf, then the request is handled directly. If the recipient is a Composite, then it usually forwards requests to its child components, possibly performing additional operations before and/or after forwarding.


### Consequences
- defines class hierarchies consisting of primitive objects and composite objects.
- makes the client simple.
- makes it easier to add new kinds of components.
- can make your design overly general.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略

## Decorator
略
## Facade
略
## Flyweight
略

## Proxy
### Intent
Provide a surrogate or placeholder for another object to control access to it.

### Also Known As
Surrogate

### Motivation
略
### Applicability
Proxy is applicable whenever there is a need for a more versatile or sophisticated reference to an object than a simple pointer. Here are several common situations in which the Proxy pattern is applicable:
- A remote proxy provides a local representative for an object in a different address space.
- A virtual proxy creates expensive objects on demand.
- A protection proxy controls access to the original object. Protection proxies are useful when objects should have different access rights.
- A smart reference is a replacement for a bare pointer that performs additional actions when an object is accessed. Typical uses include
  * counting the number of references to the real object so that it can be freed automatically when there are no more references (also called smart pointers).
  * loading a persistent object into memory when it’s first referenced.
  * checking that the real object is locked before it’s accessed to ensure that no other object can change it.

### Structure
略
### Participants
- Proxy (ImageProxy)
  * maintains a reference that lets the proxy access the real subject. Proxy may refer to a Subject if the RealSubject and Subject interfaces are the same.
  * provides an interface identical to Subject’s so that a proxy can by substituted for the real subject.
  * controls access to the real subject and may be responsible for creating and deleting it.
- Subject (Graphic)    
defines the common interface for RealSubject and Proxy so that a Proxy can be used anywhere a RealSubject is expected.
- RealSubject (Image)    
defines the real object that the proxy represents.

### Collaborations
Proxy forwards requests to RealSubject when appropriate, depending on the kind of proxy.

### Consequences
略
### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略

# Chapter 5. Behavioral Patterns
## Interpreter
略

## Method
略

## Chain of Responsibility
### Intent
Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

### Also Known As
略
### Motivation
略
### Applicability
Use Chain of Responsibility when
- more than one object may handle a request, and the handler isn’t known a priori. The handler should be ascertained automatically.
- you want to issue a request to one of several objects without specifying the receiver explicitly.
- the set of objects that can handle a request should be specified dynamically.

### Structure
略
### Participants
- Handler (HelpHandler)
  * defines an interface for handling requests.
  * (optional) implements the successor link.
- ConcreteHandler (PrintButton, PrintDialog)
  * handles requests it is responsible for.
  * can access its successor.
  * if the ConcreteHandler can handle the request, it does so; otherwise it forwards the request to its successor.
- Client
  * initiates the request to a ConcreteHandler object on the chain.


### Collaborations
When a client issues a request, the request propagates along the chain until a ConcreteHandler object takes responsibility for handling it.

### Consequences
- Reduced coupling.
- Added flexibility in assigning responsibilities to objects.
- Receipt isn’t guaranteed.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略

## Command
### Intent
Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

### Also Known As
Action, Transaction

### Motivation
略
### Applicability
Use the Command pattern when you want to
- parameterize objects by an action to perform, as Menultem objects did above.
- specify, queue, and execute requests at different times.
- support undo. The Command’s Execute operation can store state for reversing its effects in the command itself. The Command interface must have an added Unexecute operation that reverses the effects of a previous call to Execute. Executed commands are stored in a history list. Unlimited-level undo and redo is achieved by traversing this list backwards and forwards calling Unexecute and Execute, respectively.
- support logging changes so that they can be reapplied in case of a system crash.
- structure a system around high-level operations built on primitives operations.

### Structure
略
### Participants
- Command    
declares an interface for executing an operation.
- ConcreteCommand (PasteCommand, OpenCommand)
  * defines a binding between a Receiver object and an action.
  * implements Execute by invoking the corresponding operation(s) on Receiver.
- Client (Application)    
creates a ConcreteCommand object and sets its receiver.
- Invoker (Menultem)    
asks the command to carry out the request.
- Receiver (Document, Application)    
knows how to perform the operations associated with carrying out a request. Any class may serve as a Receiver.

### Collaborations
- The client creates a ConcreteCommand object and specifies its receiver.
- An Invoker object stores the ConcreteCommand object.
- The invoker issues a request by calling Execute on the command. When commands are undoable, ConcreteCommand stores state for undoing the command prior to invoking Execute.
- The ConcreteCommand object invokes operations on its receiver to carry out the request.

### Consequences
- Command decouples the object that invokes the operation from the one that knows how to perform it.
- Commands are first-class objects. They can be manipulated and extended like any other object.
- You can assemble commands into a composite command. An example is the MacroCommand class described earlier. In general, composite commands are an instance of the Composite (163) pattern.
- It’s easy to add new Commands, because you don’t have to change existing classes.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略

## Iterator
略

## Mediator
略

## Memento
略

## Observer
### Intent
Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

### Also Known As
Dependents, Publish-Subscribe

### Motivation
略
### Applicability
Use the Observer pattern in any of the following situations:
- When an abstraction has two aspects, one dependent on the other. Encapsulating these aspects in separate objects lets you vary and reuse them independently.
- When a change to one object requires changing others, and you don’t know how many objects need to be changed.
- When an object should be able to notify other objects without making assumptions about who these objects are. In other words, you don’t want these objects tightly coupled.

### Structure
略
### Participants
- Subject
  * knows its observers. Any number of Observer objects may observe a subject.
  * provides an interface for attaching and detaching Observer objects.
- Observer    
defines an updating interface for objects that should be notified of changes in a subject.
- ConcreteSubject
  * stores state of interest to ConcreteObserver objects.
  * sends a notification to its observers when its state changes.
- ConcreteObserver    
maintains a reference to a ConcreteSubject object.
  * stores state that should stay consistent with the subject’s.
  * implements the Observer updating interface to keep its state consistent with the subject’s.



### Collaborations
略
### Consequences
- Abstract coupling between Subject and Observer.
- Support for broadcast communication.
- Unexpected updates. Because observers have no knowledge of each other’s presence, they can be blind to the ultimate cost of changing the subject.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略

## State
### Intent
Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

### Also Known As
Objects for States

### Motivation
略
### Applicability
Use the State pattern in either of the following cases:
- An object’s behavior depends on its state, and it must change its behavior at run-time depending on that state.
- Operations have large, multipart conditional statements that depend on the object’s state. This state is usually represented by one or more enumerated constants. Often, several operations will contain this same conditional structure. The State pattern puts each branch of the conditional in a separate class. This lets you treat the object’s state as an object in its own right that can vary independently from other objects.


### Structure
略
### Participants
- Context (TCPConnection)
  * defines the interface of interest to clients.
  * maintains an instance of a ConcreteState subclass that defines the current state.
- State (TCPState)    
defines an interface for encapsulating the behavior associated with a particular state of the Context.
- ConcreteState subclasses (TCPEstablished, TCPListen, TCPClosed)    
each subclass implements a behavior associated with a state of the Context.


### Collaborations
- Context delegates state-specific requests to the current ConcreteState object.
- A context may pass itself as an argument to the State object handling the request. This lets the State object access the context if necessary.
- Context is the primary interface for clients. Clients can configure a context with State objects. Once a context is configured, its clients don’t have to deal with the State objects directly.
- Either Context or the ConcreteState subclasses can decide which state succeeds another and under what circumstances.

### Consequences
- It localizes state-specific behavior and partitions behavior for different states.
- It makes state transitions explicit.
- State objects can be shared.

### Implementation
略
### Sample Code
略
### Known Uses
略
### Related Patterns
略

## Strategy
### Intent
Define a family of algorithms, encapsulate each one, and make them interchangeable.　Strategy lets the algorithm vary independently from clients that use it.

### Also Known As
Policy

### Motivation
略
### Applicability
Use the Strategy pattern when
- many related classes differ only in their behavior. Strategies provide a way to configure a class with one of many behaviors.
- you need different variants of an algorithm. For example, you might define algorithms　reflecting different space/time trade-offs. Strategies can be used when these variants are implemented as a class hierarchy of algorithms [HO87].
- an algorithm uses data that clients shouldn’t know about. Use the Strategy pattern to avoid exposing complex, algorithm-specific data structures.
- a class defines many behaviors, and these appear as multiple conditional statements in its operations. Instead of many conditionals, move related conditional branches into their own Strategy class.


### Structure
略
### Participants
- Strategy (Compositor)    
declares an interface common to all supported algorithms. Context uses this interface to call the algorithm defined by a ConcreteStrategy.
- ConcreteStrategy (SimpleCompositor, TeXCompositor, ArrayCompositor)    
implements the algorithm using the Strategy interface.
- Context (Composition)
  * is configured with a ConcreteStrategy object.
  * maintains a reference to a Strategy object.
  * may define an interface that lets Strategy access its data.

### Collaborations
- Strategy and Context interact to implement the chosen algorithm. A context may pass all data required by the algorithm to the strategy when the algorithm is called. Alternatively, the context can pass itself as an argument to Strategy operations. That lets the strategy call back on the context as required.
- A context forwards requests from its clients to its strategy. Clients usually create and pass a ConcreteStrategy object to the context; thereafter, clients interact with the context exclusively. There is often a family of ConcreteStrategy classes for a client to choose from.


### Consequences
The Strategy pattern has the following benefits and drawbacks:
- Families of related algorithms. Hierarchies of Strategy classes define a family of algorithms or behaviors for contexts to reuse. Inheritance can help factor out common functionality of the algorithms.
- An alternative to subclassing.
- Strategies eliminate conditional statements.
- A choice of implementations. Strategies can provide different implementations of the same behavior. The client can choose among strategies with different time and space trade-offs.
- Clients must be aware of different Strategies. The pattern has a potential drawback in that a client must understand how Strategies differ before it can select the appropriate one. Clients might be exposed to implementation issues. Therefore you should use the Strategy pattern only when the variation in behavior is relevant to clients.
- Communication overhead between Strategy and Context.
- Increased number of objects.

### Implementation
略
### Sample Code
略
### Known Uses
略 
### Related Patterns
略

## Template Method
略

## Visitor
略

# Chapter 6. Conslusion
略

# その他
http://www.vincehuston.org/dp/

```

```
