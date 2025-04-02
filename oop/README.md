### What is OOP?
Object-Oriented Programming (OOP) is a programming paradigm based on objects that contains data (fields) and methods (behaviour). It helps in creating reusable,
scalable, and maintainable code.

🎯 Key OOP Concepts

1️⃣ ## Class & Object

- A class is a blueprint for creating objects.
- An object is an instance of a class.

✅ Example: Class & Object in Java

java
Copy
Edit
// Class (Blueprint)
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
2️⃣ Data Abstraction
Hides implementation details and shows only the necessary information.

Achieved using abstract classes & interfaces.

✅ Example: Abstraction in Java

java
Copy
Edit
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
✔ Users only see start() but don’t know how it works internally.

3️⃣ Encapsulation
Hides data & allows controlled access via methods.

Prevents direct modification of variables.

✅ Example: Encapsulation in Java

java
Copy
Edit
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
✔ Prevents direct modification of balance.

4️⃣ Inheritance
Allows a class (child) to reuse properties & methods of another class (parent).

Helps in code reusability.

✅ Example: Inheritance in Java

java
Copy
Edit
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
✔ Dog reuses makeSound() from Animal but overrides it.

5️⃣ Polymorphism
Same method behaves differently for different objects.

Two types:

Method Overloading (Compile-time Polymorphism)

Method Overriding (Runtime Polymorphism)

✅ Example: Method Overloading (Compile-time Polymorphism)

java
Copy
Edit
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
✔ Same method name add() but different parameters.

✅ Example: Method Overriding (Runtime Polymorphism)

java
Copy
Edit
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
✔ The method makeSound() is overridden in Cat class.

🎯 Key Differences Between OOP C
