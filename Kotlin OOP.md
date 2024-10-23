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
