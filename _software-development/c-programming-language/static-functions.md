---
layout: default
title: Static functions
parent: C Programming Language
---

# Static functions

C
{: .label .label-blue }

Reference manual
{: .label .label-yellow }

In C a static function is a type of function declared using the `static` keyword that is limited in scope to the translation unit (source file) where it is defined.

## Syntax

```c
static return_type function_name(parameters)
{
    // Function body
}
```

## Characteristics

- Static functions are local to the source file in which they are defined, and they are not visible to other source files.

- Static functions are not exposed in the program's symbol table, reducing the risk of naming collisions with functions from other parts of the program.

- Static functions are not accessible via function pointers, making them more secure and predictable in terms of their behavior.

## Use Cases

- **Encapsulation:** Static functions are commonly used to encapsulate functionality within a source file, providing a level of abstraction and preventing external code from interfering with or accessing internal implementation details.

- **Avoiding Naming Collisions:** By using static functions, you can define functions with common names without causing naming conflicts when linking multiple source files.

- **Code Organization:** Static functions are useful for organizing code within a source file, separating related functionality into smaller, manageable units.
