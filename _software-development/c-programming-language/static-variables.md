---
layout: default
title: Static variables
parent: C Programming Language
---

# Static variables

C
{: .label .label-blue }

Reference manual
{: .label .label-yellow }

In C, static variables are used to preserve their values between function calls, making them retain their values across multiple invocations of the same function. They are defined using the `static` keyword and can be either local to a function or global.

{: .info }
> Static variables are initialized to zero by default if no initial value is provided.

{: .warning }
> It's essential to be aware of the scope and lifetime of static variables to avoid unintended side effects when using them.

## Syntax

```c
static data_type variable_name;
```

### Local static variables

When a static variable is declared within a function, it is referred to as a local static variable. Local static variables are initialized only once, at the start of the program, and retain their values between function calls. **They have block scope**, meaning they are only accessible within the function where they are defined.

### Global static variables

When a static variable is declared outside of any function or at the file scope, it is referred to as a global static variable. Global static variables are initialized only once at the start of the program, are available for the entire lifetime of the program and **they are accessible from any function within the same source file.**

## Use cases

- Local static variables are often used when you need to maintain state or store information across multiple function calls within the same function.
- Global static variables are used when you want to limit the visibility of a variable to a single source file and ensure it retains its value throughout the program's execution.

## Example

In the following example the local static variable `counter` retains its value between calls to the `example` function, allowing it to count the number of function invocations.

```c
#include <stdio.h>

void example(void)
{
    static int counter = 0;

    counter++;
    printf("Counter: %d\n", counter);
}

int main(void)
{
    example(); // Prints "Counter: 1"
    example(); // Prints "Counter: 2"
    example(); // Prints "Counter: 3"
    return (0);
}
```
