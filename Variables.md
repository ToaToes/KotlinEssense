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
