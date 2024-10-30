## What is OOP:

1. Encapsulation (private) : Bundling the data (attributes) and methods (functions) that operate on the data into a single unit, or class. Access to the data is controlled through methods.
```
class BankAccount(private var balance: Double) { // private viriable of this class

    fun deposit(amount: Double) {
        if (amount > 0) {
            balance += amount
        }
    }

    fun withdraw(amount: Double) {
        if (amount > 0 && amount <= balance) {
            balance -= amount
        }
    }

    fun getBalance(): Double {
        return balance
    }
}

fun main() {
    val account = BankAccount(1000.0)
    account.deposit(500.0)
    account.withdraw(200.0)
    println("Current Balance: $${account.getBalance()}")
}

```
Private variables of a class cannot be accessed directly from outside the class. Has to use its public function to do set get modification on this variable

2. Inheritance (Reuse repeated code) : Mechanism where a new class can inherit the properties and methods of an existing class. This promotes code reuse.
```
// Base class
open class Animal(val name: String) { // open -> abstract in Java
    open fun makeSound() {
        println("$name makes a sound")
    }
}

// Derived class
class Dog(name: String) : Animal(name) {
    override fun makeSound() {
        println("$name barks")
    }
}

// Another derived class
class Cat(name: String) : Animal(name) {
    override fun makeSound() {
        println("$name meows")
    }
}

fun main() {
    val dog = Dog("Buddy")
    val cat = Cat("Whiskers")

    dog.makeSound() // Outputs: Buddy barks
    cat.makeSound() // Outputs: Whiskers meows
}

```
One can extend the base class to override its fucntion -> for code reusability

3. Polymorphism (override overload) : Ability of different classes to be treated as instances of the same class through a common interface. It allows methods to do different things based on the object they are acting upon.

Override(Runtime polymorphism): Same parameters but used in different subclasses

Overload(Compiletime polymorphism): Same function name but different parameters


5. Abstraction: Hiding the complex reality while exposing only the necessary parts. It allows a programmer to focus on interactions at a higher level.



## Companion Object

a companion object is a singleton object that is tied to a class rather than an instance of the class. It allows you to define members (properties and methods) that can be accessed without creating an instance of the class. Companion objects can be used to implement factory methods or to hold constants.


**Singleton Behavior:** It provides a way to create a singleton associated with the class, which can be beneficial for managing shared resources, configurations, or utility functions.

**Factory Methods:** You can define factory methods inside a companion object to create instances of the class, which can be helpful for managing object creation logic.

**Dependency Injection:** Because a companion object can provide methods or properties that can be accessed without creating an instance, it can simplify dependency injection by allowing easy access to configurations or services.

**Testing:** Companion objects can facilitate testing by allowing you to mock or stub out certain behaviors or dependencies without needing to instantiate the class itself. You can replace the companion object's methods in tests with mock implementations.

```
class User(val name: String) {
    companion object {
        const val DEFAULT_NAME = "Guest"

        fun createWithDefaultName(): User {
            return User(DEFAULT_NAME)
        }
    }
}

fun main() {
    // Using the factory method to create an instance
    val user1 = User.createWithDefaultName()
    println(user1.name) // Outputs: Guest

    // Creating an instance directly
    val user2 = User("Alice")
    println(user2.name) // Outputs: Alice
}

```

## Instance of the Class
An instance of a class, on the other hand, represents a specific object with its own state. While you can perform dependency injection using instances, it usually requires creating and managing those instances explicitly. This approach might be less convenient compared to using companion objects, especially when you want to provide shared behavior or configuration.

```
class User(val name: String)

fun main() {
    // Creating instances of the User class
    val user1 = User("Alice")
    val user2 = User("Bob")

    println(user1.name) // Outputs: Alice
    println(user2.name) // Outputs: Bob
}

```
