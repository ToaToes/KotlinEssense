Different type 'var' vs. 'val':
```
var test: Int = 1 // can be reassigned
val test: Int = 2 // cannot be reassigned
```
Variables need to be declare type first
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

Data Types:
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


Calculations:
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
Boolean:
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
