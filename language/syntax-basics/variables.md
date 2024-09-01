# Variables

Here's an example of creating a variable and initializing it:

```rust
var: name = "Jhon Wick";
```

Variables store pointers. The variable called `name` contains a
reference to a `str` object with a value of "Jhon Wick"

The type of the `name` variable is inferred to be `str`,
you can change it by specifiying the type.
If an object isn't restricted to a single type,
use the `mut` keyword or use `unions`
[language::best-practices::mutables](/language/syntax-basics/)

```rust
var str: name = "Jhon Wick";
```

## Null safety

Nex ensures null safety.

Null safety prevents an error that results use of variables 
set to `null`. The error is called a null (pointer) dereference error.
This excepts the cases where the type is implicitly allowed 
to be set to `null`

For example, say you want to find the absolute value of an `int` variable `i`.
If `i` is `null`, calling `i.abs()` causes a null dereference error.

1.  When you specify a type for a variable, parameter, or another
2.  You must initialize variables before using them.
3.  You can't access properties or call methods on an expression with a
    nullable type.

## Default value

Uninitialized variables that have a nullable type
have an initial value of `null`.
Even variables with numeric types are initially null,

With null safety, you must initialize the values
of non-nullable variables before you use them:

<?code-excerpt "misc/lib/language_tour/variables.dart (var-ns-init)"?>
```dart
int lineCount = 0;
```

You don't have to initialize a local variable where it's declared,
but you do need to assign it a value before it's used.
For example, the following code is valid because
Dart can detect that `lineCount` is non-null by the time

```dart
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
```

Top-level and class variables are lazily initialized;
the initialization code runs
the first time the variable is used.

## Const

If you never intend to change a variable, use `final` or `const`, either
instead of `var` or in addition to a type. A final variable can be set
only once; a const variable is a compile-time constant. (Const variables
are implicitly final.)

:::note
[Instance variables][] can be `final` but not `const`.
:::

Here's an example of creating and setting a `final` variable:

<?code-excerpt "misc/lib/language_tour/variables.dart (final)"?>
```dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';
```

You can't change the value of a `final` variable:

<?code-excerpt "misc/lib/language_tour/variables.dart (cant-assign-to-final)"?>
```dart tag=fails-sa
name = 'Alice'; // Error: a final variable can only be set once.
```

Use `const` for variables that you want to be **compile-time constants**. If
the const variable is at the class level, mark it `static const`.
Where you declare the variable, set the value to a compile-time constant
such as a number or string literal, a const
variable, or the result of an arithmetic operation on constant numbers:

<?code-excerpt "misc/lib/language_tour/variables.dart (const)"?>
```dart
const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```

The `const` keyword isn't just for declaring constant variables.
You can also use it to create constant _values_,
as well as to declare constructors that _create_ constant values.
Any variable can have a constant value.

<?code-excerpt "misc/lib/language_tour/variables.dart (const-vs-final)"?>
```dart
var foo = const [];
final bar = const [];
const baz = []; // Equivalent to `const []`
```

You can omit `const` from the initializing expression of a `const` declaration,
like for `baz` above. For details, see [DON'T use const redundantly][].

You can change the value of a non-final, non-const variable,
even if it used to have a `const` value:

<?code-excerpt "misc/lib/language_tour/variables.dart (reassign-to-non-final)"?>
```dart
foo = [1, 2, 3]; // Was const []
```

You can't change the value of a `const` variable:

<?code-excerpt "misc/lib/language_tour/variables.dart (cant-assign-to-const)"?>
```dart tag=fails-sa
baz = [42]; // Error: Constant variables can't be assigned a value.
```

You can define constants that use
[type checks and casts][] (`is` and `as`),
[collection `if`][],
and [spread operators][] (`...` and `...?`):

<?code-excerpt "misc/lib/language_tour/variables.dart (const-dart-25)"?>
```dart
const Object i = 3; // Where i is a const Object with an int value...
const list = [i as int]; // Use a typecast.
const map = {if (i is int) i: 'int'}; // Use is and collection if.
const set = {if (list is List<int>) ...list}; // ...and a spread.
```

:::note
Although a `final` object cannot be modified,
its fields can be changed. 
In comparison, a `const` object and its fields
cannot be changed: they're _immutable_.
:::

For more information on using `const` to create constant values, see
[Lists][], [Maps][], and [Classes][].


[Assert]: /language/error-handling#assert
[Instance variables]: /language/classes#instance-variables
[DON'T use const redundantly]: /effective-dart/usage#dont-use-const-redundantly
[type checks and casts]: /language/operators#type-test-operators
[collection `if`]: /language/collections#control-flow-operators
[spread operators]: /language/collections#spread-operators
[Lists]: /language/collections#lists
[Maps]: /language/collections#maps
[Classes]: /language/classes