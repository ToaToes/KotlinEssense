## ```launch {}```
In Kotlin, launch {} to start a coroutine
```
import kotlinx.coroutines.*

fun main() = runBlocking {
    launch {
        // This is a coroutine that can call suspend functions
        val result = fetchData() // Calling a suspend function
        println(result) // Output will be printed after the data is fetched
    }

    println("Coroutine launched!")
}

// A suspend function that simulates a long-running task
suspend fun fetchData(): String {
    delay(1000) // Non-blocking delay for 1 second
    return "Data fetched"
}
```

## ```suspend()``` -> 暂停 后继续

This makes it easier to work with tasks that take time to complete, such as network calls or database queries, without blocking the main thread.

## How to catch exception in corouine 
1. Prefer try-catch for Specific Errors
Local Handling: Use try-catch blocks within individual coroutines to handle exceptions that are specific to that coroutine's operation. This provides localized error handling and keeps the logic clear.
```
launch {
    try {
        // Your coroutine code
    } catch (e: SpecificException) {
        // Handle specific exception
    } catch (e: Exception) {
        // Handle general exception
    }
}

```

2. Use CoroutineExceptionHandler for Global Handling
Centralized Error Handling: Use a CoroutineExceptionHandler when you need a centralized way to handle exceptions that might occur in coroutines that are not enclosed in a try-catch. This is particularly useful for top-level coroutines or when using structured concurrency.
```
val handler = CoroutineExceptionHandler { _, exception ->
    println("Caught $exception")
}

CoroutineScope(Dispatchers.Default + handler).launch {
    // Coroutine code
}

```

3. Consider supervisorScope for Isolated Errors
Child Coroutine Independence: Use supervisorScope if you want to allow sibling coroutines to continue running even if one fails. This is useful for parallel operations where failure in one does not necessitate cancellation of others.
```
supervisorScope {
    launch {
        // Child coroutine code
    }
    launch {
        // Another child coroutine
    }
}

```

4. Log Exceptions for Debugging -> where is the log "e.LOG" comes from?
Logging: Ensure that you log exceptions appropriately. This helps in debugging issues that may arise in production.
```
val handler = CoroutineExceptionHandler { _, exception ->
    println("Caught $exception")
    // Optionally log to a logging framework
}

```


## What is FLOW in Kotlin
1. Flow is a powerful tool for managing asynchronous data streams in Kotlin.
2. It allows for cold, non-blocking, and sequential emissions of data.
3. You can transform, filter, and manipulate the data stream using various operators.
4. It handles backpressure and supports exception handling, making it suitable for complex asynchronous programming scenarios.
