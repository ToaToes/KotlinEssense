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

