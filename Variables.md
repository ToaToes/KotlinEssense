### Different type 'var' vs. 'val':
```
var test: Int = 1 // can be reassigned
val test: Int = 2 // cannot be reassigned
```
Variables need to be declare type first

**Clear Contracts: **
When designing APIs, specifying types (including nullable types) allows API users to understand what to expect from methods and classes. This clarity helps prevent misuse and makes integration easier.

```
var test: String
test  = "123"
//OR
var test = "123"
```
Nullable variables need to be declare with '?' marks
```
var test: String?
test = null
//OR
var test = null
```
_____

### Data Types:
```
val maxIntegerValue: Int = Int.MAX_VALUE // which is +-2147483647
//Same to Long, Byte, Short


val num: Long = 28
val num = 28L

//Float, Double
val num: Float = 2.5
val num = 2.5f //OR 2.5F

//if not specified in type
val num = 2.5 // this is going to be an 'double' type in default

//Also, Char and Boolean
```

_____


### Calculations:
```
var x = 3
var y = 5
println("result is ${x + y}")
// old java logic
var z = 0
println("x = ${x++}") // x = 0, print then add
println("x = ${++x}") // x = 2, add then print
```

_____
### Boolean:
```
var text = if('condition'){
  // operation
  "Somthing 1"
}else{
  //operation
  "Somthing 2"
}
println("$text")

** text above can be assigned to different types by conditions if type is not declare at first step
```

_____

### Control Flow
```
val alarm = 12
when (alarm) {
  12 -> * some operations
  20 -> * some operations

  //**
  12, 7, 46 -> * some operations // This will be true

  //**
  in 1..10 -> * some operations // this will check if the element is in the 1 to 10 range, which is false
  !in 10..20 -> *some operations // check is not in this range

  ...

  else -> * some operations
} 
```
To assign using when
```
val text = when (alarm){
  // -> ***
  // -> ***
}
```
* Different way:
```
val text = when{
  alarm <= 10 -> * some operations
  alarm == 10 || alarm >= 100 -> * some operations
  else -> * some operations
}
```
```
//Example: 
fun describe(obj: Any): String {
    return when (obj) {
        1 -> "One"
        "Hello" -> "Greeting"
        is Int -> "An integer"  // Type check
        !is String -> "Not a string"  // Negated type check
        else -> "Unknown"
    }
}

fun main() {
    println(describe(1))        // Output: One
    println(describe("Hello"))  // Output: Greeting
    println(describe(42))       // Output: An integer
    println(describe(3.14))     // Output: Not a string
}
```

in Java when using Switch:
```
//Example:
public class DayOfWeek {
    public static void main(String[] args) {
        int day = 3; // Example day (1 for Sunday, 2 for Monday, etc.)

        String dayType;
        switch (day) {
            case 1:
            case 7:
                dayType = "Weekend";
                break;
            case 2:
            case 3:
            case 4:
            case 5:
            case 6:
                dayType = "Weekday";
                break;
            default:
                dayType = "Invalid day";
                break;
        }

        System.out.println("Day " + day + " is a " + dayType); // Output: Day 3 is a Weekday
    }
}
```

_____
## Nullable

**Prevention of NullPointerExceptions: **
Kotlin's type system distinguishes between nullable and non-nullable types, which helps prevent the infamous NullPointerException (NPE) at runtime. By default, all types are non-nullable, so you have to explicitly declare a type as nullable (e.g., String?).

**Early Error Detection: **
Because nullability is part of the type system, potential null-related issues are caught at compile time rather than at runtime. This leads to safer code and reduces the need for extensive null checks.

**Clear Code Intent: **
The use of nullable types makes the developer's intent clear. When you see a variable declared as nullable, it indicates that it may not hold a value, prompting developers to handle these cases explicitly.

**Convenient Syntax: **
Kotlin provides safe call operators (?.) and the Elvis operator (?:) to handle nullable types elegantly. This allows for concise and readable code when dealing with potential null values.

```
val length = nullableName?.length ?: 0  // Returns 0 if nullableName is null
```

Example: 
```
val text: String? = "Name"
println(text.length)
//This will not be allowed even its not 'Null' and type it 'val'
//Only safe (?.) or non-null asserted (!!) calls are allowed on a nullable receiver of type String?

//OR ->

//Have to do a nullable check first
val text: String? = "Name"
if (text != null){
  println(text.length)
} else{
// ***
}

//OR -> Add Safe call operator: '?.'

val text: String? = "Name"
println(text?.length)
//This works

//OR -> Use '!!'

val text: String? = null
println(text!!.length)
// To throw an exception if its NULL, or give answer

//OR -> Use '?:' to set something for variable if its null

var text: String? = "Name"
text = null
println(text ?: "Something here")

```


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
