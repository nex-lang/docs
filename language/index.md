# Welcome to the Nex Programming Language

This page provides a brief introduction and will almost act as a TLDR to the Nex language through samples of its main features.

To learn more about the language, and find a more interactive cheat sheet, refer to [language::introduction](language/introduction)

---

## Comments
Nex supports single line and multi line comments
```rust
// This is a single line comment

/*
This is
a
multi line comment
*/
```


## Imports
Use the **@import** keyword use functions, variables, methods and objects from local, public and standard libraries. Multiple items can be imported by sperating with **,** commas.  The use of **from** specifies the head module from which the submodule(s) will be imported. Similarly, the **as** gives the imported sub-module. It is important to note that **as alias1, alias2, ...** should be used while importing multiple modules from a single import statement.

```rust

@import fprint from std.io; // fprint (function)

@import math from std // std.math (lib) imports entire lib

@import sin, cosin from std.math // functions sin and cosin can be used without refrencing the std.math library

@import LocalClass from localfile as L // LocalClass from localfile.nex is imported as L

```



## The Main Entry Point

Every program requires one main entry program at the top-level which is denoted by the **: fn main()** function, where execution starts. Functions that don't explicitly return a value have the **void** return type.

```rust
: fn main => ()  {
  return 0;
}
```

## Variables

Variables can be declared according to their types **var**, **const** and **mut**. Type inferences and multiple type specifications are supported. Refer to [language::types::type-system](/language/types/type-system) for a detailed explanation

```rust
: fn main => () {
    const: natural_ability = 10; // type is inferred to s_short int and neither value not type can be changed
    var s_short int: no_of_eyes = 2; // variable whose value can be changed within the s_short int range
    var: no_of_muscles = 600; // short int type is inferred and value can be changed within the short int range 

    mut: name = "Human"; // type is inferred to str, value and type can be changed

    return 0;
}
```

## Functions

To declare functions use the **fn** keyword. Although type inference and multiple type specification work, it is recommended and good practice to specify the type of functions using a the same data specifiers followed by a colon and the function keyword , e.g. **int: fn**

```rust
int: fn return_0 => () {
	return 0;
}
```


### Function Parameters
A function can easily define the parameters it requires by specifying the type and name of the parameter, e.g. **(int: x, str: y)**

```rust
int : fn sum_xy => (int: x, int: y) {
    return x + y;
}
```

## Classes
To define classes, use the **class** keyword.
