## what is a sealed class

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

## Abstract class VS. interface
