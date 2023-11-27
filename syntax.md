## The _yi_ programing language Syntax

### + Comments
```c
/* single line comment */
/*
    multiline
    comment
    example
*/
```

### + Type system
Generally there are few kinds of data types in _yi_.  
 + integrals (+ booleans here)
 + floatings
 + tables

#### _Integrals_
They're basically any integer numbers and even _true|false_ boolean keywords.

#### Floatings
Floating point numbers are basically IEEE754 standard compatible ones.

#### Tables
Table is a named structure that holds several primitive data type fields of named tables.

#### [SPECIAL] Name alias
Name aliases are synonyms to original data types (and aliases of course **can** alias other aliases as well)  

### + Type alias declarations  
```rust
fast_u8 :: alias u8
fast_int :: alias int
```
Aliases are used to redeclare types or tables.

### + Original data type names
#### _Integrals_
```glsl
int, uint, i8, u8, i16, u16, i32, u32, i64, u64, i128, u128, i256, u256
```

#### _Floatings_
```c
float, double, real, f32, f64, f128, f256
```

#### _Tables_ example
```c
vec2_t :: table {
    x real,
    y real,
}

vec2f :: alias vec2_t
```
<span style="color:#4bbfa8">vec2_t</span> is a table type that contains two named floatings.  
On the other hand, <span style="color:#4bbfa8">vec2f</span> is a type-alias for <span style="color:#4bbfa8">vec2_t</span>.

### + :: (double colons)
Double colons (::) is used to define a type, or type alias.  

### + Compile-time attributes  
In the _yi_ programming language there are several attributes for functions and even variables/constants.
```
[_[ATTRIBUTE_NAME]_]
```

### + Visibility
In _yi_ the term _visibility_ means - an ability to use certain symbol/construction outside of current file's scope.  
By default every function in _yi_ is public, but you can define them as <span style="color:#4f8aba">hidden</span>.  
```rust
[_[hidden]_]
foo () {}
```

### + Functions
In the _yi_ there is all the functions.
```rust
bar () {}
```
Example of definition of an empty function with no return values required.
```rust
sqrt (x real) real {
    ret __builtin_sqrt(x)
}
```
Example of definition of an simple function that accepts single parameter _x_ of type <span style="color:#4bbfa8">real</span> and return type <span style="color:#4bbfa8">real</span>.
It also shows an example of function call with an argument placement.  
Here the part _'(x real) real'_ is a type, of function that accepts one 'real' and returns one with the same data type.  

### + Scopes
In _yi_ programming language scopes are a blocks of code, that defines lifetime of containing variables.
```c
sin (y real) real {
    x real = y * PI
    { /* definition of a new scope */
        x2 real = x * x
        x = x2
        /* here x2 was created and almost immediately destroyed */
    }
    /* and yeah, x was not used at all, so after this call it will be destroyed as well */
    ret __builtin_sin(y)
}
```

### + Constants
Constant values are simple a compile-time known values, such as <span style="color:#b77db2">#define</span>s in C or <span style="color:#4f8aba">constexpr</span> in C++.

```go
const PI real = 3.1415926
```
An example of typical constant definition with type <span style="color:#4bbfa8">real</span>.  

#### ___[NOTE]___ Constants can handle everything ___except___ functions!

### + Variables
Variables in _yi_ programming language are all partly mutable. In other words, compiler decides what variables will change during runtime and mark them as _mutable_, while all other variables will possibly be immutable (almost constant).
```c
... somewhere inside function ...

instance_id int = 0
get_instance(instance_id)

... somewhere inside function ...
```
An example of variable _instance_id_ instantiation with type <span style="color:#4bbfa8">int</span>, and initializing with value 0.  

### + Using multiple sources
In _yi_ you can mention some files to use in the top of the file with special keyword <span style="color:#4f8aba">import</span>. Compiler will solve them firstly by lookup all directories with tries to find requested source file. If it can't be found in this project, compiler decides to lookup all the dependencies. If requested file can't be found anyway -> there an import error.  
But here's the catch: by default there's no need to import sources of this project since compiler by default shares public functions and types across single project! But you can do this still..
```python
import (std, math)
```
An example of import of _std_ and _math_. SO, _std_ is a library/project so by including it, we include all the public members of it. _math_ is a source file and we have on in our project's source directory.

### + Pointers (yeah, and they're pretty important)  
Unfortunately, pointers are so important in programming, and in the computer science in general. In _yi_, we have a pointers arithmetic. Pointers here works basically like C's ones.
```c
assist (p *int, len int) { ... }
```
An example a definition of function that accepts two parameters: _p_ pointer to int, and _len_ integer.

```c
... somewhere inside function ...

attribute int = 22
attribute_ptr *int = &attribute

... somewhere inside function ...
```
An example of declaration of a variable _attribute_ptr_ with type of pointer to integer, that points to another variable _attribute_ of type int, that initialized with a value 22.

### + Arrays
Arrays and pointers are different sides of the same coin really. Arrays is a pointers that can possibly carry it's count of the elements in a row, calculated like (number_of_bytes / size_of_element).
```rust
greeting [u8] = "Hello, World!"
```
An example of declaration of a variable of type 'an array of u8s(ueights)'. This example array also carries it's length because of compile it's nature.

### + Platform-deduction (OS, Architecture)  
In _yi_ you can detect on what kind of OS this section of code will try to compile, and exclude it from a function.
```c
get_os_name () *u8 {
    [_[windows]_]
    {
        ret "Windows NT"
    }
    [_[linux]_]
    {
        ret "Linux Distro"
    }
    [_[darwin]_]
    {
        ret "Apple OSX"
    }
    
    ret "Unknown"
}
```
A great example of real usecase of this feature. __Explanation:__ we have a three blocks of code, every one of them returns a value immediately; so, if this function compiles under MS Windows machine, only block with attribute 'windows' will be compiled, so function will return _"Windows NT"_; same situation for _linux_ and _darwin_; if our machine's platform is neither windows nor linux nor mac, so the last return statement will return _"Unknown"_.

### + Control flow (if)  
In _yi_ programming language, like in most common languages there are pretty known _if ... else_ statements.
```swift
if x == 3 {
    ... code goes here ...
}
else (x > 3) {
    ... code goes here ...
}
else {
    ... code goes here ...
}
```
Usage example of if-else statements; especially, parenthesis not required at all; here also a possibility of conditional _else_ statement.

### + Control flow (loop)
In _yi_ programming language there are no distinguish between _while_ and _for_ loops. And here's the catch: all loops in _yi_ by default is ___infinite___ (yeah, really). And you can restrict amount of iterations by checking for conditions like in _if...else_ statements. Here's an example:
```swift
loop        { ... code here will be looped infinitely ... }
loop true   { ... same situation ... }
loop false  { ... will never be executed and emit a warning ... }
loop x      { ... code here will be looped as long as x can be interpreted as true ... }
```

### + Control flow (cases)
So, in _yi_ we also have a case-matching statement, mostly like _switch_.
```swift
case x {
    [12] {
        ... code here executes only when x == 12 ...
    }
    [0] {
        ... code here executes only when x == 0 ...
    }
    [...] {
        ... code here executes only when x variant is not listed in case ...
    }
}
```

### Summary
```c
import (std, math)

const MINIMAL_LOOP_COUNT int = 0x10

[_[entry, hidden]_]
main (args [*u8]) int {
    if (length(args) >= 2) {
        print("Here is something passed in command prompt")
    }
    else {
        print("Hello, world!")
    }
    ret 0
}

```
