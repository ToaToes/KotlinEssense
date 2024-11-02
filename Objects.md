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

## Object Expression - anonymous class -> you dont have to create class to implement interface
In Kotlin, an object expression is a powerful feature that allows you to create **anonymous** objects, which can be particularly useful for **implementing interfaces** or **creating simple classes without having to formally define them**. This is similar to Java's anonymous classes but is often more concise and expressive in Kotlin.

- when you want to implement an interface, you typically would create a class that provides the implementation for the interface's methods. However, with object expressions, you can directly create an instance of an anonymous class that implements the interface without the need to define a named class.

```
interface Greeting {
    fun greet(name: String)
}

fun main() {
    val greetingObject = object : Greeting { //-> object expression
        override fun greet(name: String) {
            println("Hello, $name!")
        }
    }

    greetingObject.greet("Alice") // Output: Hello, Alice!
}

```
1. Anonymous Objects: You can create an object on-the-fly that implements an interface or inherits from a class without declaring a separate class.
2. Instantiation: You can provide implementations for any methods defined in the interface or class.
3. No Need for a Named Class: This is particularly useful when you need a one-off implementation and don’t want to clutter your code with a full class definition.


## Object declaration
Object Declarations: Create singleton objects that can be used throughout the application.
```
object Singleton {
    fun sayHello() {
        println("Hello from Singleton!")
    }
}

// Usage
Singleton.sayHello() // Output: Hello from Singleton!
```
1. Global State Management
Singletons are often used to manage global state or configuration settings in an application. For instance, you might have a configuration object that holds settings that should be accessible **throughout** the app.
```
object AppConfig {
    var apiUrl: String = "https://api.example.com"
    var timeout: Int = 30
}

```
2. Logs
You can create a singleton for logging purposes, ensuring that all parts of your application log messages through a single instance.
```
object Logger {
    fun log(message: String) {
        println("Log: $message")
    }
}

```
3. Service Locator or Dependency Injection
Singletons can be used in service locators or simple dependency injection frameworks to provide instances of services throughout an application.
```
object ServiceLocator {
    val networkService: NetworkService by lazy { NetworkService() }
    val databaseService: DatabaseService by lazy { DatabaseService() }
}

```

4. Event Bus
In applications that require communication between different parts, a singleton event bus can facilitate this by allowing components to subscribe and publish events.
```
object EventBus {
    private val listeners = mutableListOf<(String) -> Unit>()

    fun subscribe(listener: (String) -> Unit) {
        listeners.add(listener)
    }

    fun publish(message: String) {
        listeners.forEach { it(message) }
    }
}

```

5. Caching
A singleton can also be used for caching data that needs to be accessed frequently across different parts of the application.
```
object DataCache {
    private val cache = mutableMapOf<String, Any>()

    fun put(key: String, value: Any) {
        cache[key] = value
    }

    fun get(key: String): Any? {
        return cache[key]
    }
}

```
6. Testing
In unit tests, you can use singletons to create mock or stub implementations of services that can be reused across different tests.
