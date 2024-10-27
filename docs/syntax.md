# X3 Syntax
## Variable
```x3
let x: i32 = 10 // variable name must be camelCase
const Y: i32 = 50 // const name must be an UPPERCASE
```

## Function
```x3
fn add(a: i32, b: i32) i32 {
    return a + b
}

fn add_expr(a: i32, b: i32) i32 => a + b

fn<T> add_generic(a: T, b: T) T => a + b // will cause an error durining compile-time if T have not implemented addition on itself
```

## Typedef
```x3
// typedef keyword can be used to declare custom types
typedef<T> Vec3 { x: T, y: T, z: T }
let position: Vec3<f32> = Vec3(10.4, -3.0, 660.243)
let x: f32 = position.x
let y: f32 = position.y
let z: f32 = position.z

// typedef keyword can also be used as an alias, but then..
// int type will not be equal i32 type, they are different as int is new declared type
typedef int i32

// This example was made to show how function can be declared
typedef<T> MapFn fn(T) T
```

## Array
```x3
// as array size should be known at compile-time, it has this uncommon syntax to declare size of an array
let integers: i32 x 10 = [2, 6, -3, 4, 9, -10, 44, 5, 5, 10]

// [0] * 10 will be replace with [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
let bytes: u8 x 10 = [0] * 10
```

## Memory Allocation
```x3
use std::alloc

// alloc will try allocate a memory of a type and return it's address
// as alloc function may return an error, symbol ? is used after calling it to unwrap value.
// If error happens will crash program, it's better catch and process error
let x: &i32 = alloc<i32>()?
```

## Error
```x3
use std::{String, io::println}

// always error function will return nothing or String as an error type
fn always_error() ?String => error String::new("Always an Error")

// will not compile, as function may return an error
// must use ? after calling at least
always_error()

// to process an error, lambda function can be used after symbol ?
always_error()? |err: String| {
    println(String::new("[Error]: Oh no, it's an error, look what it says: ") + err)
}
```

## Built-in Data Types
+ `i8` - `i128` signed integer
+ `u8` - `u128` unsigned integer
+ `f16` - `f128` floating point
+ `bool` - a boolean true/false
+ `(<type...>,)` - tuple
+ `&<type>` - reference

# X3 Examples
## Hello, World!
```x3
use std::io::println

fn main() {
    println("Hello, World!")
}
```