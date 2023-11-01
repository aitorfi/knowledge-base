---
layout: default
title: Variadic functions
parent: C Programming Language
---

# Variadic functions

C
{: .label .label-blue }

Reference manual
{: .label .label-yellow }

@see [printf function](../stdio/printf-function)

Variadic functions are a powerful feature in the C programming language that allows you to define functions that can accept a variable number of arguments. They are commonly used for functions like *printf* and *scanf*, which can handle different types and numbers of arguments.

## Usage

Variadic functions in C are typically implemented using the `<stdarg.h>` header, which provides a set of macros and types to work with variable-length argument lists.

To create a variadic function, you define a function with a fixed number of parameters followed by an ellipsis (...) These fixed parameters are typically used to specify information about the variable arguments, such as the number or type of arguments.

```c
#include <stdarg.h>

int myVariadicFunction(int fixedArg1, int fixedArg2, ...)
{
    // Function implementation
}
```

Inside the variadic function, you typically use the following macros and functions provided by `<stdarg.h>` to access the variable arguments:

- **va_list:** Type that represents the argument list, which is an internal data structure used to access the arguments passed to a variadic function.

- **va_start:** A macro that initializes the `va_list` for variable argument processing. It takes two arguments: the `va_list` itself and the name of the last known parameter in the function. The last known parameter serves as a reference point for accessing the variable arguments.

- **va_arg:** A macro that retrieves the next argument from the `va_list` with a specified data type.

- **va_end:** A macro that is used to clean up and release resources associated with the `va_list`. It should be called once you're done processing variable arguments.

## Example

In the following example *average* is a variadic function that receives a regular parameter named *num* which specifies how many parameters follow. The function asumes the argument list elements are of type `double` and uses them to calculate and return the average number.

```c
#include <stdio.h>
#include <stdarg.h>

double average(int num, ...)
{
    va_list args;
    double sum;

    sum = 0;
    va_start(args, num);
    for (int i = 0; i < num; i++)
    {
        sum += va_arg(args, double);
    }
    va_end(args);
    return (sum / num);
}

int main(void)
{
    printf("Average: %.2f\n", average(4, 2.5, 3.0, 4.5, 5.0));
    return (0);
}
```
