# What is OOP?
Object-Oriented Programming (OOP) is a programming paradigm based on objects that contains data (fields) and methods (behaviour). It helps in creating reusable,
scalable, and maintainable code.

# 🎯 Key OOP Concepts

## 1️⃣ Class & Object

- A class is a blueprint for creating objects.
- An object is an instance of a class.

✅ Example: Class & Object in Java

```
class Car {
    String brand;
    int speed;

    void drive() {
        System.out.println(brand + " is driving at " + speed + " km/h");
    }
}

// Main Class
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();  // Object Creation
        myCar.brand = "Toyota";
        myCar.speed = 100;
        myCar.drive(); // Output: Toyota is driving at 100 km/h
    }
}

```

## 2️⃣ Data Abstraction

- Hides implementation details and shows only the necessary information.
- Achieved using abstract classes & interfaces.

✅ Example: Abstraction in Java

```
abstract class Vehicle {
    abstract void start(); // Method without implementation
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car engine starting..."); 
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle myCar = new Car();
        myCar.start(); // Output: Car engine starting...
    }
}

```
✔ Users only see start() but don’t know how it works internally.

## 3️⃣ Encapsulation

- It means binding of data and methods together in a single entity.
- Hides data & allows controlled access via methods.
- Prevents direct modification of variables.

✅ Example: Encapsulation in Java

```
class BankAccount {
    private double balance; // Private variable (hidden data)

    public BankAccount(double initialBalance) {
        this.balance = Math.max(initialBalance, 0); // Ensures valid balance
    }

    public double getBalance() { // Getter method
        return balance;
    }

    public void deposit(double amount) { // Controlled modification
        if (amount > 0) balance += amount;
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount myAccount = new BankAccount(1000);
        myAccount.deposit(500);
        System.out.println("Balance: " + myAccount.getBalance()); // ✅ Output: 1500
    }
}

```
✔ Prevents direct modification of balance.

## 4️⃣ Inheritance

- Allows a class (child) to reuse properties & methods of another class (parent).
- Helps in code reusability.

- Single Inheritance : A subclass inherits from one parent class.
- Multilevel Inheritance : A subclass inherits from another subclass, forming a chain.
- Hierarchical Inheritance : Multiple subclasses inherit from a single parent class.
- Multiple Inheritance (via Interfaces) – Sub class inheriting from multiple parents(Java doesn’t support multiple class inheritance). so class implements multiple interfaces.

✅ Example: Inheritance in Java

```
// Parent Class
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

// Child Class
class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.makeSound(); // Output: Dog barks
    }
}

```

✔ Dog reuses makeSound() from Animal but overrides it.

## 5️⃣ Polymorphism

- Condition of occuring in several different Forms. Same method behaves differently for different objects.

Two types:

### Method Overloading (Compile-time Polymorphism)

- Same method name with different number of parameters.

### Method Overriding (Runtime Polymorphism)

- Subclass inherits the methods of parent class and can also provide a new implementation for a method already defined in the parent class.

✅ Example: Method Overloading (Compile-time Polymorphism)

```
class MathUtils {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        MathUtils math = new MathUtils();
        System.out.println(math.add(5, 10));     // Output: 15
        System.out.println(math.add(3.5, 2.5)); // Output: 6.0
    }
}

```
✔ Same method name add() but different parameters.

✅ Example: Method Overriding (Runtime Polymorphism)

```

class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Cat();
        myAnimal.makeSound(); // Output: Cat meows
    }
}

```
✔ The method makeSound() is overridden in Cat class.

## Constructor

- It is a specialised method used for initialising the objects.
- The name of the class and constructor should be same.
- The constructor is invoked whenever the object of that associated class is created.

##  this Keyword 

- The this keyword refers to the current object of a class.
- It helps to avoid naming conflicts between instance variables and method parameters.

✅ Example: Using this to differentiate between instance variable and parameter

```

class Person {
    String name;

    Person(String name) {
        this.name = name;  // `this.name` refers to instance variable, `name` is parameter
    }

    void show() {
        System.out.println("Name: " + this.name);
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person("Alice");
        p.show();  // Output: Name: Alice
    }
}

```

## Access Modifiers

- They control access to data fields, methods and classes.

- Public    : Allows classes, methods, data fields accessible from any class.
- Private   : Allows classes, methods, data fields accessible only from within the own class.
- Default   : Allows classes, methods, data fields accessible by any class in the same package.
- Protected : Allows classes, methods, data fields accessible by any class and sub class in the same package as well as subclass in other package.

## Super

- The super keyword in Java is used to refer to the parent class.
- It helps access parent class variables, methods, and constructors.

```
super.variable → Accesses a parent class variable if a child class has the same name.
super.method() → Calls an overridden method from the parent class.
super() → Calls the parent class constructor and must be the first statement in a child class constructor.

```

## Final

- final class → Cannot be inherited by other classes.
- final method → Cannot be overridden in subclasses.
- final variable → Its value cannot be changed after initialization (acts as a constant).

## Abstract Class
An abstract class is a class that cannot be instantiated (you can't create objects of it). It’s meant to be a base for other classes.

Key Features of Abstract Classes
- ✔ Can have both normal methods and abstract methods (methods without a body).
- ✔ Can have instance variables (fields).
- ✔ Used when you want to provide some common functionality but still enforce certain rules.

Example of Abstract Class

```
abstract class Animal {  
    String name; // Instance variable

    void eat() {  // Concrete method
        System.out.println("Eating...");
    }

    abstract void makeSound(); // Abstract method (must be implemented by subclasses)
}

class Dog extends Animal {  
    @Override
    void makeSound() {  
        System.out.println("Woof! Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Animal a = new Animal(); ❌ ERROR! Can't create an abstract class object.
        Dog d = new Dog();
        d.eat();  // ✅ Common method from Animal
        d.makeSound();  // ✅ Dog’s version of makeSound()
    }
}

```

## When to Use Abstract Classes?
- When you want to partially implement functionality but force subclasses to implement specific methods.
- When you need instance variables (fields).

## Interface
An interface is like a contract that classes must follow. It only contains abstract methods (before Java 8).

Key Features of Interfaces
- ✔ All methods in an interface are abstract by default (before Java 8).
- ✔ Cannot have instance variables (only constants).
- ✔ A class can implement multiple interfaces (unlike abstract classes, which support only single inheritance).

Example of Interface

```
interface Animal {  
    void makeSound(); // No need for 'abstract', it's implicit
}

class Dog implements Animal {  
    @Override
    public void makeSound() {  
        System.out.println("Woof! Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.makeSound();  // ✅ Dog’s version of makeSound()
    }
}

```

## When to Use Interfaces?
- When you want full abstraction (no method implementations).
- When you need multiple inheritance (since Java does not allow multiple inheritance with classes).
- use implements keyword to implement interface and extend keyword to extend classes


### Extends and Implements keyword

```

abstract class Animal {
    abstract void makeSound();
}

interface Pet {
    void play();
}

class Dog extends Animal implements Pet {  // Extends a class and implements an interface
    @Override
    void makeSound() {
        System.out.println("Woof!");
    }

    @Override
    public void play() {
        System.out.println("Dog is playing!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.makeSound();  // From Animal
        d.play();  // From Pet
    }
}

```

- A class can extend only one class (Java does not support multiple inheritance for classes).
- A class can implement multiple interfaces (solves multiple inheritance problem).


## Static 

- Belongs to the class, not to instances (objects).
- Shared across all objects of the class.
- Can be accessed without creating an object of the class.
- Think of static as something "global" to the class.

### Static Variables (static Fields)
A static variable is shared among all instances of a class.

```

class Example {
    static int count = 0; // Shared variable

    Example() {
        count++;
    }

    void showCount() {
        System.out.println("Count: " + count);
    }
}

public class Main {
    public static void main(String[] args) {
        Example e1 = new Example();
        Example e2 = new Example();
        
        e1.showCount();  // Output: Count: 2
        e2.showCount();  // Output: Count: 2
    }
}

```
✅ Why use static variables?
- If we didn't use static, each object would have its own count variable instead of sharing one.

### Static Methods (static Functions)
- Can be called without creating an object.
- Cannot access non-static (instance) variables directly.

```

class MathUtils {
    static int square(int x) { // Static method
        return x * x;
    }
}

public class Main {
    public static void main(String[] args) {
        int result = MathUtils.square(5); // No need to create an object
        System.out.println("Square: " + result); // Output: 25
    }
}

```
✅ Why use static methods?
- If a method doesn’t need instance variables, make it static.

### Static Classes (Nested Static Classes)
A static class is a nested class inside another class that does not depend on the outer class instance.

```
class Outer {
    static class Inner {  // Static nested class
        void show() {
            System.out.println("Inside Static Inner Class");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Outer.Inner obj = new Outer.Inner(); // No need for Outer class instance
        obj.show();
    }
}

```
✅ Why use static classes?
- If the inner class does not need access to the outer class’s variables.
