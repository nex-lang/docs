# Welcome to the Nex Programming Language

This page provides a brief introduction and will almost act as a TLDR to the Nex language through samples of its main features.

To learn more about the language, and find a more interactive cheat sheet, refer to [language::introduction](language/introduction)

---

## Hello World

Every program requires one main entry program at the top-level which is denoted by the **: fn main()** function, where execution starts. Functions that don't explicitly return a value have the **void** return type. To display text on the console, you can use the **fprint()** function from std.io:

```rust
@import fprint from std.io;

: fn main => ()  {
  fprint('Hello, World!');
}
```

## Variables

Variables can be declared according to their types **var**, **const** and **mut**. Type inferences and multiple type specifications are supported. Read more about this in [language::variables](/language/types/type-system)

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

Functions can be declared using the **fn** keyword. Although type inference and multiple type specification work, it is recommended and good practice to specify the type of functions using a the same data specifiers followed by a colon and the function keyword , e.g. **int: fn**

### Parameters
A function can easily define the parameters it requires by specifying the type and name of the parameter, e.g. **(int: x, str: y)**

```rust
(long int, int): fn sum_xy => (int: x, int: y) {
    return x + y;
}
```
