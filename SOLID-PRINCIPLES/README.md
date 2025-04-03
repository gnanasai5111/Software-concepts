### SOLID PRINCIPLES

SOLID is a set of five principles that help in writing clean, maintainable, scalable, and flexible object-oriented code.


## S - Single Responsibility Principle (SRP)

A class should have only one reason to change (one responsibility).

✅ Example: A User class should not handle both authentication and database storage.

## O - Open/Closed Principle (OCP)

Classes should be open for extension, but closed for modification.

✅ Example: Use interfaces or abstract classes to extend functionality without modifying existing code.

## L - Liskov Substitution Principle (LSP)

Subclasses should be replaceable for their base classes without breaking functionality.

✅ Example: A Rectangle class should not behave differently when replaced with a Square.

## I - Interface Segregation Principle (ISP)

Don't force classes to implement unnecessary methods. Create smaller, specific interfaces instead.

✅ Example: Instead of one Animal interface with fly(), swim(), and walk(), create separate interfaces like Flyable and Swimmable.

## D - Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions.The Dependency inversion principle (DIP) states to depend upon abstractions, [not] concretes

✅ Example: Instead of hardcoding PayPal in a PaymentService, inject it dynamically via an interface.
