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


## difference between ```companion object``` declare and ```object``` declare

**```companion object```** declare
Class-Related Functionality: Companion objects are ideal for static-like behavior that is specific to a class, especially when you need to create instances of that class or manage data relevant to it.

1. Definition: A companion object is defined within a class and is **associated** with that class.
2. Purpose: It is primarily used to hold static members (methods and properties) that can be accessed without creating an instance of the class.
3. Access: Members of a companion object can be accessed using the class name directly. You can also implement interfaces in companion objects.
4. Instantiation: There can only be one companion object per class.

```
class MyClass {
    companion object {
        const val CONSTANT = "I am a constant"

        fun create(): MyClass {
            return MyClass()
        }
    }
}

// Usage
val instance = MyClass.create() // Using companion object method
println(MyClass.CONSTANT) // Accessing companion object constant

```
**Companion Object Example**
Imagine you have a class representing a user, and you want to provide a factory method to create a user from a JSON string:
```
class User(val name: String) {
    companion object {
        fun fromJson(json: String): User {
            // Logic to parse JSON and create a User instance
            return User("ParsedName") // Simplified for example
        }
    }
}

// Usage
val user = User.fromJson("{\"name\":\"John\"}")

```



**```object```** declare -> _having only one instance applies to the object itself, cant create mulitple instances of it_
Standalone Functionality: Object declarations are great for features that **don't need to be tied to specific data instances**. They are useful for utility functions or global state management where you want a single instance handling certain operations.

1. Definition: An object declaration creates a singleton instance that is not tied to any class. It stands alone as a separate entity.
2. Purpose: It is used for creating a single instance of an object, often for managing shared state, utilities, or for defining singletons.
3. Access: You access the members of an object declaration using the object name directly.
4. Instantiation: There can only be one instance of an object declared with the object keyword.

```
object MySingleton {
    var count: Int = 0
}

fun main() {
    // Accessing the singleton instance
    MySingleton.count++
    println(MySingleton.count) // Output: 1

    // Attempting to create another instance (this will not compile)
    // object MySingleton { } // Uncommenting this line will cause a compile error

    // Accessing the same instance again
    MySingleton.count++
    println(MySingleton.count) // Output: 2
}

```

**Object Declaration Example**
On the other hand, if you need a singleton for logging throughout your application:
```
object Logger {
    fun log(message: String) {
        println("Log: $message")
    }
}

// Usage
Logger.log("This is a log message.")

```
