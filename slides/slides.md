% Genetic algorithms
% Quentin de Laroussilhe - Guillaume Sanchez

# The need for programming paradigms

## The rise of complexity in our code

### Source code length comparison

(Assuming C language)

* "Hello world" : 10 lines
* EPITA malloc : 180 lines
* myhttpd : 1,200 lines
* dlmalloc : 4,000 lines
* linux kernel : 6,000,000 lines
* debian 5.0 : 324,000,000 lines

### The problem

As software grows bigger, the complexity becomes too huge for a human brain to
handle. Nopony can remember all the details of a modern program.

We need a way to manage this complexity explosion.

### The solution : abstraction

* Abstraction is the act of "naming and manipulating compound elements as
units"[1].

* Those units behave as black boxes by "naming semantically meaningful
  syntactic classes"[2]

* I don't care how the "DrawSquare" procedure works, but I trust that it draws
  a square.

* We can pile up these units in abstraction layers.


[1] Abelson and Sussman, "Structure and Interpretation of Computer Programs"
(1984)
[2] David A. Schmidt, "The Structure of typed programming languages" (1994)

## What is a paradigm?

### Formal definition

"[paradigms are] universally recognized scientific achievements that, for a
time, provide model problems and solutions for a community of researchers."

-- Thomas Kuhn, "The Structure of Scientific Revolutions" (1962)

### In the programming world

"A paradigm is a set of formal abstraction methodologies for modeling and
developing software."

-- Me, OOP conference (today)

## General guidelines

### There is no perfect paradigm

* I'll stop quoting Kuhn for now.
* There is no silver bullet
* Don't try to shoehorn a single paradigm for every problem you encounter
  (*cough*java*cough*)

### Paradigms are not mutually exclusive

* Think of paradigms as pairs of looking glasses
* The more glasses you have, the more ways you have to view your problem
* Multiple interpretations makes you richer

# How to use OOP?

## A few considerations before we dive in

### There is no unique definition of OOP

* Since its inception in the 60s by `Simula 67`, many languages have created
  their own flavor of OOP
* Static, dynamic, class based, prototype based...
* I can't possibly talk about every flavor out there
* We will focus on static, class based OOP (the one used in C++, Java, C#...)

### Some words have different meanings in a OOP context

* type
* subtyping
* polymorphism (we'll get back on that)
* message

## The basics

### Working on a real life exemple

* I want to create a video game!
* My game will have characters I can control, monsters I can pwn, items to
  equip...
* All these entities are placed on a map, and there will be obstacles!
* IT'S GONNA BE FUCKING AWESOME
* ...How do I modelize that?

### Everything is an object!

* All the entities in our system are thingamajigs called "objects"
* These objects all have an internal state
* They also can communicate with other objects in the system

### The blueprint of an object : the class

* In class blased OOP, Sartre never happened.
* Before creating an object, one must beforehand define the blueprint of this object
* In this blueprint, we detail the data the object will posess and how it will
  communicate with other objects

### A bit of terminology

* A object is the *instance* of a class
* Data inside an object are the object's *attributes*
* Operation on these datas (and therefore, communication of these datas) is
  done by the object's *methods*

## In practice...

### Defining a class

* All code samples will be done in an imaginary language.

~~~
class Character(hp, strength):
    hp = hp;
    strength = strength;

    void attack(Character other):
        other.receive_damage(strength)

    void receive_damage(int amount):
        hp = hp - amount
~~~

### Creating an object, accessing attributes, calling methods

~~~
hubert = new Character(100, 20)
bernard = new Character(250, 42)

if (hubert.strength < bernard.strength):
    print "Bernard is the strongest."

hubert.attack(bernard)
~~~

### Public and private fields

* Remember that objects exists to build abstraction!
* Some attributes and methods are internal details that should not be visible
* Some languages advocate making all attributes visible
* The privateness is classwide, not objectwide!

## Relationships between classes

### Aggregation relationship

* Aggregation is a "as a" relationship
* This relationship is present when when an object's attribute is another
  object
* Exemple: a character can equip an item.

### Composition relationship

* Special case of the aggregation relationship
* The posessed object only lives while its holder does.
* Destruction of the container implies destruction of the contained objects
* Exemple: a map is composed of tiles

### Inheritance relationship

* Inheritance is a "is a" relationship
* Some classes are *specialization* of a more general concept
* They share a lot of common ground, but differ in specific ways
* Exemple: a warrior is a special character, so is a mage.
* Inheritance is a way of achieving `polymorphism`

## Expanding on the inheritance relationship

### Classes are types

* Defining a new class means defining a new type
* As such, a derived class is a *subtype*
* Most type theory applies

### A word on polymorphism

* Cardelli and Wegner (1985) define four kinds of polymorphism


In OOP, we usually imply "inclusion polymorphism"

### the Liskov substitution principle

* If S is a subtype of T, then objects of type T maybe be replaced with objects
  of type S
* This principle is enforced by both the compiler and you
* By the compiler: it will allow using S wherever T is needed
* By you: you must enforce the *semantic* coherence of this relationship

## Our exemple : modelized

### UML diagram


### Beware of UML!

* I used the awesome [yuml.me](yuml.me) website to create this UML in 2 min
* UML is cool when it allows you to quickly formalize your thoughts
* UML is not cool when you spend a week on a diagram that will inevitably
  change in the middle of development
* "Un intellectuel assis va moins loin qu'un con qui marche" -- Michel Audiard

# Advanced concepts

## A few common idioms

### Composition over inheritance

* Inheritance is a very strong and very rigid relationship
* It should only be used when you want to expose the complete interface of a
  class (think LSP)
* If you only want part of a class, you should rather extract that part in a
  new class and make it a member.

### SOLID

* SOLID is an acronymception by Micheal Feathers.

* SRP (Single Responsibility principle):
    an object should have only a single responsibilty
* OCP (Open/Closed principle):
    software entities should be open for extension, but closed for modification
* LSP (Liskov substitution principle):
    objects in a program should be replaceable with instances of their subtypes
    without altering the correctenss of that program
* ISP (interface segregation principle):
    many client specific interfaces are better than one general purpose
    interface
* DIP (dependency inversion principle):
    one should depend upon abstractions. Do not depend upon concretions

## Design patterns

### What are design patterns?

* A design pattern is a general reusable solution to a commonly occurring
  pattern.
* Gained popularity with the 1994 book by the "Gang of Four"
* You can thank these guys for AbstractSingletonProxyFactoryBean

### Example 1 : the singleton pattern

* One of the most (over)used design pattern
* Extremely polemical, which is why I'm talking about it
* Guarantees that a class is instantiated once, and only once.
* Subsequent instanciations will return the same object
* Most common critique : "isn't that essentially a global variable?"

### Example 2 : the template method pattern

* One of the few design patterns I actually like
* Closely related to C++'s NVI (Non Virtual Interface)
* Allows for the enforcement of invariants.
* What happens if someone subclasses your class and breaks LSP?
* Public methods can not be specialized.
* They delegate to private methods that can be specialized, but check for
  coherence before and after calling them.

### The danger of design patterns

* Design patterns often represent workarounds to OOP limitations.
* Most of these design patterns are not needed in other paradigms.
* If your design relies heavily on those kinds of patterns, perhaps you should
  consider another paradigm.
* If the language you're using doesn't allow any other paradign than OOP
  (*cough*java*cough*), just cry.

# Conclusion

### Contact

* That's it for me!
* You can get these slides on the GConfs bitbucket page (bitbucket.org/gconfs)
  or on my github (github.com/chewie)
* Feel free to contact me at chewie@deliciousmuffins.net
