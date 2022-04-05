# Use MVC, SOLID Principles, and Design Patterns in Java

## Discover Good Programming Practices with the SOLID Principles
Now comes a feature, which is a lot like the first one -but a bit different. 
How do you put in this new feature? Well, there's always copy/paste. 
Take the code that exists, copy and paste it in, then fix it up a little to do the new thing. 
Then repeat the process for subsequent features. In the long run, this code becomes difficult to maintain.

The problem is really twofold:
- First, the solution gradually gains complexity. Fewer people may understand how it works.
- Second is the mentality it brings with it. The team begins to accept less than quality work, for the sake of delivering a feature. 
So, it's more than just poor architecture; it's the view that poor architecture is OK and inevitable.

### Identify the SOLID Principles 
- **"S" is for Single responsibility**:
A class should do one thing, and do it well. It should only have one reason to change.

- **"O" is for Open/closed principle**:
A class should be open to extension, but closed to modification. 
Well, whenever you add a new concept to the system (an extension), you shouldn't have to go back and make a bunch of changes (modification) to support it.

- **"L" for Liskov substitutability**:
Adding a subtype through inheritance should not break the existing code. 
I call this the "no surprises" principle. That is, if the system is working and I add a new class that is derived from another, the system should still work.

- **"I" for Interface segregation**:
Essentially the single responsibility principle, applied to interfaces.

- **"D" is for Dependency inversion**:
High-level classes shouldn't have to change when a low-level class is modified. High-level classes should define an abstraction that the lower-level class conforms to.

<hr>

## Structure a SOLID Compliant Application With MVC Architecture
### What is MVC?
MVC is a software architecture approach. It divides the responsibilities of the system into three distinct parts:

- **Model**: The model holds the state information of the system. 

- **View**: The view presents the model information to the user. 

- **Controller**: The controller makes sure that user commands are executed correctly, modifying the appropriate model objects, and updating the view objects.

SOLID tells you to split out responsibilities, and model-view-controller (MVC) indicates where those splits should be. 
It is the basis of your system's architecture. Each class in the system falls into one of the three categories and therefore has a specific purpose.

### What Goes in the Model (M)?
**State information** is kept in model classes. These are the items being viewed and manipulated. 
Also, if you need to store anything long term, it will be the model objects.

If you were to program the restaurant example, a couple of model objects would be a customer's order,
or how many pounds of potatoes are in the pantry:
```java
class CustomerOrder {
    List<MenuItems> selectedItems;
    float baseCost;
    float tax;
};

class PantryItem {
    String name;
    float currentInventoryLevel;
    float reorderLevel;
};
```
if you consider our game, the state is all the information that tells the current "story." 
How many players are there? Which player holds which card? Which cards are still in the deck? 
All of those ideas added together make up the state of the game.

### What Goes in the View (V)?
The view is how the model is **presented and interacted** with by the user. It's the most likely thing to change. 
You want a clear distinction in the way this part interacts with the rest of the system. 

At the restaurant, this would be the menu, but also the greeter, and wait staff, and anyone else you would interact with directly. 
If you were building an application, this would be your user interface or UI. You might think of one of the views like this:
```java
class Greeter {
    public void askHowManyPeopleToSeat();
    public void reportEstimatedWaitTime();
    public void takeCustomersToTable();
}
```
### What Goes in the Controller (C)?
The controller is where the **flow of the application** is managed. All the **sequencing of interactions** between the user and the system is here. 
The user interacts with the view, which then interacts with the controller. 
The controller then makes the appropriate modifications to the model objects, makes new ones, or deletes no longer needed ones. 
In the restaurant example, the controller would be the set of rules, established by the owner or manager, on how to take care of a guest:
```java
class ProcessCustomer {
    public void customerGreeted();
    public void customerSeated();
    public void orderTaken();
    public void orderDelivered();
    public void patronSatisfactionChecked();
    public void billPresented();
    public void billPaid();
};
```
This would represent the workflow, or sequence of steps the customer would be led through.

<hr>

### Implement the Model for Your Application
- The model consists of the elements with which you interact. These contain the state information of the system.

- To find your model objects, review the list of requirements.

- In our application, we've defined that:

  - The model consists of player, hand, playing card, deck, rank, and suit.

  - A player has a hand. A hand holds a playing card. A deck holds playing cards.
  
### Implement the Controller and View for Your Application
- The controller is responsible for sequencing a use case and validates events sent by the view.

- The view is responsible for presenting the model and sequence information and gathering input from the user.

- The controller's responsibilities are determined by looking at the steps of the application. 
- The view's responsibilities are determined by what the controller needs to show to the user.

<hr>

## "S" for the Single Responsibility Principle
 > A class should do one thing, and do it well. Another way of saying this is a class should only have one reason to change.
 
### Why Use the Single Responsibility Principle?
keeping the responsibilities of a class to a minimum aids in this.
- one idea, one place
- unit tests are much easier to write


**Approach**
- Examine the requirements to determine what the code needs to do.

- Partition the code into MVC responsibilities.

- For each responsibility, ensure it is placed into the correct class. 

- If a class is doing too many different things, create new classes to separate out the responsibilities.

**Summary**
- Single responsibility means a class should only do one thing, or to put another way, only have one reason to change.

- It’s an easy principle to violate, as you add new features to the system. When adding in a new feature, think about:

  - What future changes might impact the class?

  - What could give the class more that one reason to change? 

- Remember, if a class mimics a real life concept, it should only implement the one responsibility that corresponds to the real life concept.

<hr>

## "O" for the Open/Closed Principle
> A class should be open to extension, but closed to modification.

In other words, new functionality did not require a rewrite of existing code. 

### Why Use the Open/Closed Principle? 
If you aren’t modifying the existing code, you know you aren’t breaking any of it. All the new functionality is contained in the newly added class(es).

Guidelines to help you recognize when open/closed may be applicable:
- When you have algorithms that perform a calculation (cost, tax, game score, etc.): it is likely that the algorithm will change over time. 
Create an interface first, and then provide specific implementations in classes, picking the class at run time.

- When you have data coming or or going from the system: the endpoint (file, database, another system) is likely to change. 
So is the actual format of the data. Again, come up with an interface first, and then a specific implementation for getting or saving the data as needed.

**Summary**
- The open/closed principle says that classes should be open to extension, but closed to modification.

- In existing systems, it might take some rework to get the code in a position to take advantage of open/closed.

<hr>

## "L" for the Liskov Substitution Principle
> Adding derived classes shouldn't break the functionality of an already existing system.

When adding a new class in the hierarchy, the existing system shouldn’t break when it uses the new class.

When looking to use inheritance, ask yourself:
- Does the derived class have a meaningful implementation for all overridden methods? 
  - If so, that's a good thing. ✅

- Would implementing an overridden method be out of the ordinary, possibly resulting in throwing an exception? 
  - If so, that's bad. ❌

- Would implementing an overridden method ignore the call, and do nothing? 
Usually that's a bad thing, but might be justifiable. You should keep an eye out if the derived class does this for:
  - A single method. ✅
  - Many of them. ❌
**Summary**
- Liskov substitution principle applies to inheritance hierarchies. 
It is violated when a derived class cannot take the place of a base class without the system breaking.

- To make sure you avoid violating this rule, try to first think of high-level abstractions/interfaces instead of low-level/concrete implementations.

<hr>

## "I" for the Interface Segregation Principle

If you are comfortable with the single responsibility principle, the interface segregation principle will make perfect sense.
It’s the same thing, only for interfaces: 

> An interface should describe one set of behaviors.

- Keeping interfaces small and to the point decreases coupling

- An interface that is well focused on what it should do is described as exhibiting high cohesion. 
Like single responsibility, high cohesion means that an interface describes one thing, very well.

**Summary**
- Interface segregation is the single responsibility principle for interfaces.

- It’s easy to violate the principle. The temptation is to add a new method to an existing interface, since it’s already doing something.

- When in doubt, it's better to have two interfaces with few methods to implement, rather than a single interface with many responsibilities.

<hr>

## "D" for the Dependency Inversion Principle
> High-level classes shouldn’t have to change because low-level classes change

- Dependency inversion says high-level concepts should communicate through high-level abstractions. 
In other words: high-level classes shouldn’t have to change because low-level classes change.

- Be aware of knowing too much about other classes’ implementation.

<hr>

## Avoid STUPID Practices in Programming
### What is S for? Singleton
- Singletons ensure that a single instance of a class is created, which seems to make sense.
- But the real problem is when this becomes your way of viewing most functionality. It becomes tempting to have a singleton for everything.
- Global state information is model information that ends up being shared across modules or portions of your application. 
Usually, having a system dependent on global state variables is a bad idea. The problem is that any part of the program can change the state.

Ask yourself if you really need a singleton. Why does this class needs to be accessed as if it were global data?
See if there isn’t a compelling reason for it not to be.

### What is T for? Tight Coupling
Real problem with a singleton; any class that uses one is tightly coupled to it. That class can’t be extracted and used elsewhere. It has to drag the singleton along.

You can reduce coupling by coding to an interface instead of an implementation.

### What is U for? Untestability
- There are many reasons why a class is difficult or impossible to test. But it usually boils down to tight coupling with some other component. 
- If you require many dependencies for a class to work correctly, that indicates it needs to be rewritten. 
- Testing a component can also be tricky when it violates single responsibility and does too many things.

### What is P for? Premature Optimization
Premature optimization refers to when an anticipated problem is dealt with before it is a problem.

For example, in our card game, we need to shuffle the deck. Shuffling can be a slow and repetitive process. 
We could design a lightning-fast algorithm that not everyone can understand, but cards don't get shuffled that often. 
So optimizing that algorithm really isn't worth the effort.

### What is I for? Indescriptive Naming
While this seems like something you can easily avoid, it appears quite often. It occurs because, at the time you are writing code, the problem and solution make sense. 

For example, Let's say you are dealing with a rectangle, so you name the upper-left corner variables x1 and y1. That makes sense.
Months later, when looking at the code, you (or someone else) see these variables. What is x1? You have to read the code to know. 
If you had named the variables upperLeftCornerX and upperLeftCornerY, you would know immediately.

### What is D for? Duplication
Copying and pasting are fine when you have to get something in place in a short time. But, you need to go back and find a better long-term solution. 

Ask yourself: 
- Why is there is so much commonality between these two pieces?

- Can the duplicated code be put into a common base class?

- Can I extract out an interface and put the slightly different pieces into different implementations?

**Let's Recap!**
- STUPID stands for:
  - Singleton

  - Tight coupling

  - Untestability

  - Premature optimization

  - Indescriptive naming

  - Duplication 

- STUPID approaches lead to difficult-to-maintain and hard-to-test code designs.

- It’s easy to fall into STUPID traps, so stay vigilant and ask yourself the right, SOLID questions.

<hr>

## Program Efficiently With Design Patterns
### What Is a Design Pattern?
A design pattern is a proven, reusable solution to a commonly occurring problem. 
It describes the static or dynamic nature of classes and objects that implement the solution. 
You are free to tailor the solution to fit your particular situation.

Patterns are usually described with four attributes:
- Name: allows you to describe the situation at a high level. It gives a universal language.

- Problem: indicates the situation where the pattern can be applied

- Solution: provides the arrangement of classes and objects that make the pattern work.

- Consequences: are what happens when you apply the pattern. Every pattern has at least one positive consequence. 
It solves the problem. But sometimes there may be negative consequences

Gang of Four (Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides) released the book Design Patterns: Elements of Reusable Object-Oriented Software

They categorized the patterns into three sections:

1. Creational patterns - patterns concerned with creating objects.

2. Structural patterns - aligning classes and objects.

3. Behavioral patterns - interactions between objects. 

### Why Use a Design Pattern?
- The biggest advantage of using a design pattern is that you know that the solution works. But there are other advantages as well.
- One is the understandability of the code.
- The level of communication between developers is elevated

### Let's Recap! 
- Patterns are proven, reusable solutions to commonly occurring problems.

- Patterns are described with four items:

  - Name

  - Problem

  - Solution

  - Consequences

- Using patterns lead to better understandability and maintainability.

- There are three types of patterns:

  - Creational

  - Structural 

  - Behavioral 

<hr>

## Create Objects With Creational Design Patterns
### Why Use Creational Patterns?
- You are making an object of type someClassName. Forever. Unless you go back in and change it. 
And as mentioned, going back in and changing existing code can lead to problems. So what can you do instead? 
Well, try to avoid using the word “new” as much as possible.
- There is an adage in software development that says you can solve any problem by adding yet one more level of indirection. 
If you apply that, you can defer the creation of the object to something else. That other thing is still called new, 
but you gain flexibility in your code through one extra level of indirection.

### What is the Factory Pattern?
 Let other objects make objects for you. The factory object is configured in some fashion and then asked to create the wanted object.
 ```java
 public class DeckFactory {
	public static Deck makeDeck(DeckType type) {
        switch (type) {
            case Normal: return new NormalDeck();
            case Small: return new SmallDeck();
            case Test: return new TestDeck();
        }
        
        // fallback
        return new NormalDeck();
	}
}
```
```java
Deck myDeck = DeckFactory.makeDeck(DeckType.Normal);
```
The factory method works when we want the flexibility to pick between specific implementations at run time. 
Just tell the factory what you want, and it makes that specific kind.

### What is the Prototype Pattern?
The prototype creational patterns make a new object by cloning an already existing one. 
Again, you preconfigure an object (or objects) the way you want. 
Then pick the one you want your new object to be like, and ask the prototype to return a clone of itself.

```java
SomeClass a = new SomeClass();
SomeClass b = a;

// this also changes a.someField
// since a and b refer to the same thing
b.someField = 5;
```

```java
SomeClass a = new SomeClass();
a.someField = 1202;

SomeClass b = a.clone();
// a.someField remains 1202
// since it is a different object
b.someField = 5;
```
Cloning is a handy pattern when you want an exact duplicate of an existing object, or at least very close. 
The alternative is to create an object in the normal way (call new), and then set all the values to match the item you want to copy. 
But that's a lot of code (and typing energy).

### What is the Builder Pattern?
You often build a single object out of constituent pieces. But how do you control what pieces go into the whole? The builder pattern. 
The builder follows an algorithm to determine what pieces to build. But the pieces can vary.

```java
public interface GameBuilder {
	Game getGame();
}

public class NormalHighCardGameBuilder implements GameBuilder {
	public Game getGame() {
		return new Game(DeckFactory.makeDeck(DeckType.Normal),
						EvaluatorFactory.makeEvaluator(EvaluatorType.High));
	}
}

public class SmallHighCardGameBuilder implements GameBuilder {
	public Game getGame() {
		return new Game(DeckFactory.makeDeck(DeckType.Small),
						EvaluatorFactory.makeEvaluator(EvaluatorType.High));
	}
}
```

### What are Singletons?
Singleton is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.
1. Ensure that a class has just a single instance
2. Provide a global access point to that instance.
```java
class SoundManager 
{ 
    // need to remember the one instance somewhere
    // so we'll keep a static variable
    private static SoundManager _instance = null; 

    // like any other class, attributes exist
    private int currentSoundLevel;

    // make the constructor private
    // so it can't be called by anything other than
    // methods defined in this class
    private SoundManager() { 
        currentSoundLevel = 11;
    } 
  
    // the method clients call to gain access to the singleton
    public static SoundManager getInstance() {
        // if we haven't made one before, make one now
        if (_instance == null) 
            _instance = new SoundManager(); 
  
        // return the one we made
        // either this time, or any time before
        return _instance; 
    }

    // nothing special about any other method
    public void setVolume(int value) {
        currentSoundLevel = value;
    }
} 
```
### Let's Recap! 
- Creational patterns add a level of indirection to object creation, adding flexibility to applications.

- The factory pattern has an object create another object. You can configure the factory to make an object just the way you want it.

- The prototype pattern creates a new object by cloning an existing object.

- The builder pattern creates a complex object by assembling various other objects into the single, complex item.

<hr>


## Organize Objects With Structural Design Patterns
### What Are Structural Design Patterns?
- When you are all done, you bring your items to the front of the store, checkout, and pay. You interact with the cashier. Pretty simple. It is an example of a structural pattern where a large amount of complexity is hidden behind an uncomplicated interface. 
- Structural patterns are ways of organizing classes or objects so that they are easy to use. There might be a lot happening behind the scenes, but as a user, you don’t need to know the complexities. 
- There are two types of structural patterns — those that organize classes and those that organize objects.


### What is the Adapter Pattern?
Adapter is a structural design pattern that allows objects with incompatible interfaces to collaborate.

The problem this pattern addresses is when you have code that expects one interface (set of methods), but the implementation provides another. 

Eg. In our card game, let's say we created a PlayableCard interface, and our PlayingCard implemented it:
```java
interface PlayableCard {
  void flip();
};

class PlayingCard implements PlayableCard {
   bool faceUp;
   
   void flip () {
      faceUp = !faceUp;
   }
};
```

But somewhere else in the company, someone has created a CoolCard class, that looks better than our implementation. We'd like to use that instead:
```java
class CoolCard {
   void turnOver() {
      // cool implementation here
    }
};
```
If we used this new card, every place that called our  flip()  operation would have to be changed to  turnOver(). 
Not that hard in our little game, but imagine working on a bigger project! So instead, let's introduce an adapter that looks like a PlayableCard, but acts like a CoolCard:
```java
class PlayingCardAdapter implements PlayableCard {
    CoolCard thisCard;
    void flip() {
        thisCard.turnOver();
    }
};
```
Now we don't have to change everywhere that we called the flip() operation! We do, however, have to create PlayingCardAdapter objects instead of PlayingCard objects. But we have a factory that makes all of that. So that's the only place in our code that needs to know about the new CoolCard concept that we added.

### What is the Composite Pattern?
There are times when you want to treat a bunch of objects and single objects the same.

The composite design pattern does this. Every item, whether it is a single entity or collection exposes the same interface. The collection’s implementation runs through all the objects it owns, asking each to perform the requested method.

```java
Shape shape = new Circle();
shape.draw();
```
```java
Shape shapes = new ComplicatedDiagramOfABunchOfShapes();
shapes.draw();
```

### What is the Decorator Pattern?
Decorator is similar to composite in that it allows a group of objects to behave as if it were just one. However, the difference is that the objects managed by decorators add new functionality that the original did not contain.

Decorator is a structural design pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

### Let's Recap! 
- Structural patterns are ways of organizing classes or objects so that they are easy to use. 

- The adapter pattern changes the interface of a class from non-compatible, to one that is expected.

- The composite pattern allows individual and collection objects to be treated the same.

- The decorator pattern allows for additional behavior to be added and removed at runtime.

<hr>

## Manage Objects With Behavioral Design Patterns
### What Are Behavioral Design Patterns?
There is one central place that is responsible for the coordination of all the other objects. Rather than pilots talking to each other, they talk to one central controller. The controller then sends out commands to all of the aircraft. In software, this central controller pattern is called a mediator.

Similarly, you often have complicated communication between objects. The behavioral patterns provide ways for objects to communicate in sensible and systematic ways.

### What is the Observer Pattern?
In many situations, you have an object that has state information in it, that other objects need to be aware of. When that state information changes, all those other objects need to be informed. 

Observer is a behavioral design pattern that lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.

