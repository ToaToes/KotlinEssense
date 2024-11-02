## what is a sealed class -> usually goes with ```when```

A sealed class in Kotlin is a special kind of class that restricts class hierarchies. It allows to define a limited set of subclasses, making it easier to work with when using when expressions and providing type safety.

1. Restricted Inheritance: Sealed classes can only be subclassed within the same file where they are defined. This ensures that all possible subclasses are known at compile time, which enhances safety and maintainability.
2. Type Safety: When using sealed classes in when expressions, you don't need an else clause if you've covered all possible subclasses. This makes your code more robust, as the compiler can enforce completeness.
3. Hierarchical Structure: Sealed classes are useful for representing a restricted set of types that are closely related. This can be particularly beneficial in cases like representing states, events, or results.

```
sealed class NetworkResult {
    data class Success(val data: String) : NetworkResult()
    data class Error(val message: String) : NetworkResult()
    object Loading : NetworkResult()
}

fun handleResult(result: NetworkResult) {
    when (result) {
        is NetworkResult.Success -> println("Data: ${result.data}")
        is NetworkResult.Error -> println("Error: ${result.message}")
        is NetworkResult.Loading -> println("Loading...")
    }
}

```
- State Management: Representing different states in UI applications (e.g., loading, success, error).
- Result Wrapping: Wrapping responses from APIs to handle success and error states.
- Event Handling: Defining a set of events that can occur in a system.

### practical usage for sealed class
1. Representing UI States
Sealed classes are commonly used in Android development to represent different UI states in a single view. For example, when loading data from a network, you might have states like loading, success, and error.
```
sealed class UiState {
    object Loading : UiState()
    data class Success(val data: List<String>) : UiState()
    data class Error(val message: String) : UiState()
}

// Example usage in a ViewModel
fun fetchData() {
    // Emit Loading state
    _uiState.value = UiState.Loading
    
    // Simulate network call
    viewModelScope.launch {
        try {
            val data = fetchFromNetwork()
            _uiState.value = UiState.Success(data)
        } catch (e: Exception) {
            _uiState.value = UiState.Error(e.message ?: "Unknown error")
        }
    }
}

```
2. Handling API Responses
You can use sealed classes to wrap responses from an API call, allowing you to clearly define the possible outcomes: success with data, error with a message, or loading.
```
sealed class ApiResponse {
    data class Success(val result: String) : ApiResponse()
    data class Error(val error: String) : ApiResponse()
    object Loading : ApiResponse()
}

// Example function that processes the response
fun handleApiResponse(response: ApiResponse) {
    when (response) {
        is ApiResponse.Success -> println("Data received: ${response.result}")
        is ApiResponse.Error -> println("Error occurred: ${response.error}")
        ApiResponse.Loading -> println("Loading...")
    }
}

```
3. Managing Navigation States -> can be replaced with navigation _viewModel_
In an application with multiple screens, you can use sealed classes to define the different navigation states or destinations, making navigation logic more type-safe and easier to manage.
```
sealed class Screen {
    object Home : Screen()
    object Details : Screen()
    data class Profile(val userId: String) : Screen()
}

// Function to navigate based on the screen state
fun navigateTo(screen: Screen) {
    when (screen) {
        is Screen.Home -> // Navigate to Home
        is Screen.Details -> // Navigate to Details
        is Screen.Profile -> // Navigate to Profile with userId
    }
}

```
4. State Management in Redux-like Architectures
In architectures like Redux, you can represent the application state using sealed classes. Each state can represent different stages of the application, such as loading, loaded, or error.
```
sealed class AppState {
    object Idle : AppState()
    object Loading : AppState()
    data class Loaded(val data: List<String>) : AppState()
    data class Error(val message: String) : AppState()
}

// Example reducer function
fun reducer(state: AppState, action: Action): AppState {
    return when (action) {
        is Action.LoadData -> AppState.Loading
        is Action.DataLoaded -> AppState.Loaded(action.data)
        is Action.ErrorOccurred -> AppState.Error(action.message)
    }
}

```
5. Complex Business Logic
Sealed classes can help model complex business logic where you have multiple possible states or types of data being processed. For instance, if you're processing various types of payments, you can model each payment type with a sealed class.

```
sealed class Payment {
    data class CreditCard(val amount: Double) : Payment()
    data class PayPal(val email: String, val amount: Double) : Payment()
    object Cash : Payment()
}

// Function to process payment
fun processPayment(payment: Payment) {
    when (payment) {
        is Payment.CreditCard -> // Process credit card payment
        is Payment.PayPal -> // Process PayPal payment
        Payment.Cash -> // Process cash payment
    }
}

```

## What is a data class
A data class in Kotlin is a special type of class that is primarily used to hold and manage data. Data classes are designed to simplify the creation of classes whose main purpose is to store values. They automatically provide useful functionalities, such as generating standard methods like ```equals()```, ```hashCode()```, and ```toString()```, which are often boilerplate code in regular classes.

1. Primary Constructor: A data class must have a primary constructor that takes at least one parameter. The parameters are automatically turned into properties.

2. Generated Methods:

- ```equals()```: Checks for structural equality (i.e., whether two instances of the data class have the same property values).
- ```hashCode()```: Generates a hash code based on the property values.
- ```toString()```: Provides a string representation of the object, listing its properties and their values.
- ```copy()```: Allows you to create a copy of the data class instance, with the option to modify some properties.

3. Immutability: While you can define mutable properties, data classes are often used with val properties to make them immutable.

```
data class Person(val name: String, val age: Int)

fun main() {
    val person1 = Person("Alice", 30)
    val person2 = Person("Alice", 30)

    println(person1) // Output: Person(name=Alice, age=30)

    // Structural equality
    println(person1 == person2) // Output: true

    // Hash code
    println(person1.hashCode() == person2.hashCode()) // Output: true

    // Copying with modification
    val person3 = person1.copy(age = 31)
    println(person3) // Output: Person(name=Alice, age=31)
}

```

- Modeling Data: Representing data models in applications, such as user profiles, product details, or any data that needs to be passed around.
- Returning Results: Returning structured data from functions or APIs, making it easier to manage the returned data.
- Handling Responses: Using data classes to model API responses, simplifying parsing and accessing the data.

### to build data class equivalent in JAVA
```
public class Person {
    private final String name; // Immutable field
    private final int age;     // Immutable field

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && name.equals(person.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

```

## Abstract class and Sealed class
Sealed Class: Represents a fixed set of related types, ideal for modeling states or results with exhaustive checks in when expressions.
Abstract Class: Allows for a mix of abstract and concrete methods, providing a base class for shared functionality among related classes.


## Abstract class VS. interface

1. **Interface**
Implicitly Open: All functions in an interface are inherently open for overriding. When a class implements an interface, it must provide implementations for all of its methods. There’s no need to use any modifier like open or override in the interface itself because all methods are treated as abstract and open by default.
```
interface Drivable {
    fun drive(): String  // No body, must be implemented
}

class Car : Drivable {
    override fun drive(): String { // Must override to provide implementation
        return "Car is driving"
    }
}

```

2. Abstract class
- Abstract Methods: An abstract class can have abstract methods (which need to be implemented in derived classes) as well as concrete methods (which have an implementation).

- open Modifier: In an abstract class, you typically declare methods as abstract if you want subclasses to provide their own implementations. For concrete methods (those with a body), you can use the open modifier to allow subclasses to override them. By default, methods in a class are final, meaning they cannot be overridden unless explicitly marked as open.
```
abstract class Vehicle {
    abstract fun drive(): String  // Abstract method, must be overridden

    open fun info(): String {  // Concrete method that can be overridden
        return "This is a vehicle"
    }
}

class Car : Vehicle() {
    override fun drive(): String {
        return "Car is driving"
    }

    override fun info(): String { // Optional, can override this method
        return "This is a car"
    }
}

```

Interface: All functions are implicitly open and must be overridden in implementing classes. No modifiers are needed for the methods in the interface.

Abstract Class:
- Abstract methods must be overridden in subclasses.
- Concrete methods can be overridden if they are marked as open.
