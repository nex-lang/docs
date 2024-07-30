# Welcome to the Nex Programming Language

This page provides a brief introduction and serves as a TL;DR to the Nex language through samples of its main features.

To learn more about the language and find a more interactive cheat sheet, refer to [language::introduction](language/introduction)

---

## Comments
Nex supports single-line and multi-line comments:
```rust
// This is a single-line comment

/*
This is
a
multi-line comment
*/
```

## Imports
Use the **@import** keyword to use functions, variables, methods, and objects from local, public, and standard libraries. Multiple items can be imported by separating them with **,** commas. The use of **from** specifies the head module from which the submodule(s) will be imported. Similarly, **as** gives the imported sub-module an alias. When importing multiple modules from a single import statement, use **as alias1, alias2, ...**.

```rust
@import fprint from std.io; // fprint (function)

@import math from std // std.math (lib) imports entire lib

@import sin, cosin from std.math // functions sin and cosin can be used without referencing the std.math library

@import LocalClass from localfile as L // LocalClass from localfile.nex is imported as L
```

## The Main Entry Point

Every program requires one main entry point at the top-level, which is denoted by the **: fn main()** function, where execution starts. Functions that don't explicitly return a value have the **void** return type.

```rust
: fn main => () {
    return 0;
}
```

## Variables

Variables can be declared according to their types **var**, **const**, and **mut**. Type inferences and multiple type specifications are supported. Refer to [language::types::type-system](/language/types/type-system) for a detailed explanation.

```rust
: fn main => () {
    const: natural_ability = 10; // type is inferred to s_short int and neither value nor type can be changed
    var s_short int: no_of_eyes = 2; // variable whose value can be changed within the s_short int range
    var: no_of_muscles = 600; // short int type is inferred and value can be changed within the short int range 

    mut: name = "Human"; // type is inferred to str, value and type can be changed

    return 0;
}
```

## Functions

To declare functions, use the **fn** keyword. Although type inference and multiple type specification work, it is recommended and good practice to specify the type of functions using the same data specifiers followed by a colon and the function keyword, e.g. **int: fn**.

```rust
int: fn return_0 => () {
    return 0;
}
```

### Function Parameters
A function can easily define the parameters it requires by specifying the type and name of the parameter, e.g. **(int: x, str: y)**.

```rust
int: fn sum_xy => (int: x, int: y) {
    return x + y;
}
```

## Classes and Attributes
To define classes, use the **class** keyword. Classes are reproducible objects and have two functions, **__init__** and **__free__**, by default. **__init__** is called when the class is instantiated, and **__free__** is called when the class is freed. A class can have its methods and components (functions and variables) defined with an access specifier (`pub`, `priv`). They can `ext` (extend and be extended) other classes and attributes.

```rust
class A => {
    var priv: component1;

    pub: fn get_component1 { return self.component1; };
}
```

Attributes are a group of methods and components that can be extended by both attributes and classes (Note: attributes can't extend classes). To define them, use the **attr** keyword. Attributes don't have **__init__** or **__free__** functions and just provide a group of methods and components for others to build upon.

```rust
attr having_component_2 => {
    var priv: component2;

    pub: fn get_component2 { return self.component2; };
}
```

### Extension of Methods and Components
The **ext** keyword allows for classes and attributes to share components and methods.

```rust
class B ext attr.having_component_2, A;
/*
    `B `will contain components from attribute `having_component_2` and `A`
    var priv: component1;
    var priv: component2;

    pub: fn get_component1 { return self.component1; };
    pub: fn get_component2 { return self.component2; };
*/
```

## Loops
Nex supports two major types of loops, **for** and **while**, which allow for repetition of a code block. Both loops support the **break** statement, which tells the program to exit the loop, and **continue**, which skips to the next iteration. The **break; continue;** statements are commonly used in combination with other control statements.

### For Loop
A for loop can be declared using the **for** keyword followed by certain conditions according to specific requirements. Nex supports classic **initial; compare; update** and iterative loops like in Python.

#### Generic For Loops
This loop consists of 3 expressions at its core: **initial; compare; update**. The loop starts off by executing the initialization expression, and the comparison expression is checked. If the comparison is false, the loop runs, and the update expression is executed. This process goes on until the comparison expression is true.

```rust
var int: x = 0;
// after int = 1, i++ and x += 1 (block) is run until i < 100 is false
for (var int: i = 1; i < 100; i++) {
    x += i;
}
```

#### Iterative and Range For Loops
This loop utilizes **:**, the range symbol. The range (`:`) makes it so that the value starts from 0 and increments until it reaches the value or list/array after `:`.

Similarly, the **::** (iterate) symbol will make it so that the list/array after **::** is iterated over, and each value from the iterated array/list is incrementally set to the provided variable.

```rust
var SomeComplexObject: x[5]; // assuming pre-defined

for (var: obj :: x) {
    // can access obj.(...) components and methods iteratively 
}

for (var: obj : 2) {
    // obj is set to 1 on the first pass and 2 on the second pass 
}
```

### While Loop
A while loop is yet another super-useful loop that allows for repetition in blocks of code. It has an expression that, when **expr == true**, the loop runs, and when **expr == false**, the loop stops.

```rust
while (x >= 100) {
    x += 1;
}
// loop runs while x >= 100 and stops if x >= 100 is false
```

## Control Statements
Control statements provide a way for the computer to make decisions and perform logical checks.

### If.. elif.. else
The **if... elif... else** statements are used to make decisions. **if** is an independent comparison that checks if the expression is true and executes the code if it is true. **else** is a dependent comparison that is run when all if and elif statements fail to run. **elif** (else + if) is another dependent comparison that, when used with **if**, provides a way to implement alternatives logically.

```rust
var int: IQ = 85;
var str: smartness;

if (x > IQ) {
    smartness = "SMART!";
} elif (x < IQ) {
    smartness = "BELOW AVERAGE";
} else {
    smartness = "AVERAGE ON THE DOT!!";
}
```

### Switch, case, and default
The **switch** statement evaluates the provided expression and compares it with the values of each case label.

If there is a match, the statements of the label are executed. The code runs until it finds a **break;** statement, and if none of the labels match, the **default** label is invoked.

```rust
var: options = 2;
var: operation;

switch () {
    case 1:
        operation = "multiplication";
        break;
    case 2:
        operation = "addition";
        break;
    default: break;
}
```

### Try, except, and finally
The **try** statement is used to test a block of code for errors and custom handle them effectively using the **except** statement. The **finally** block code is executed regardless of outcome and exceptions.

```rust
@import fprint, read from std.io;

var str: buf;

try {
    buf = read("data.csv");
} except std.io.FileNotFound {
    buf = read("data.txt");
} finally {
    fprint(buf);
}
```

#### Custom Errors
Custom errors can be defined using the **err** keyword, and custom components/information can be stored. These errors can then be thrown using the **throw** keyword.

```rust
err WindowCoordinatesExceeded {
    str: platform;
    int[]: window_init_flags;
}
```

Sure, here's the content for structs and enums in Nex:

## Structures
Structures (structs) in Nex allow you to group related data together. Use the **struct** keyword to define a structure. Each field in the struct can have its type and name specified. You can create instances of the struct and access their fields using dot notation or a initializer's list.

```rust
struct Point {
    int: x;
    int: y;
}

: fn main => () {
    var Point: r = {x: 10, y: 20};
    return 0;
}

/* or,

: fn main => () {
    var Point: p;
    p.x = 10;
    p.y = 20;
    return 0;
} */
```

## Enumerators
Enumerators (enums) in Nex allow you to define a type by enumerating its possible values. Use the **enum** keyword to define an enumerator. Each value in the enum is a constant.

```rust
enum Direction {
    NORTH;
    SOUTH;
    EAST;
    WEST;
}

: fn main => () {
    var Direction: dir = Direction.NORTH;

    switch (dir) {
        case Direction.NORTH:
            // handle north
            break;
        case Direction.SOUTH:
            // handle south
            break;
        case Direction.EAST:
            // handle east
            break;
        case Direction.WEST:
            // handle west
            break;
        default:
            break;
    }

    return 0;
}
```