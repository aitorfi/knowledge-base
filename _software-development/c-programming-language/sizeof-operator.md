---
layout: default
title: sizeof operator
parent: C Programming Language
---

# sizeof operator

C
{: .label .label-blue }

Operator
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

The `sizeof` operator in the C is used to determine the size, in bytes, of a data type or an expression. It allows programmers to write code that is more flexible and portable by enabling them to work with the actual memory sizes used by various data types, regardless of the platform.

## Return value

The `sizeof` operator returns the size (in bytes) of the specified expression or data type as an unsigned integral constant, typically of type `size_t`.

{: .info}
> To convert the return value of the **sizeof** operator from bytes to other units (e.g., kilobytes), simple arithmetic operations can be performed.

## Usage examples

- Calculating the **size of a data type**:

```c
int main(void)
{
    size_t intSize = sizeof(int);       // Returns the size of int in bytes
    size_t floatSize = sizeof(float);   // Returns the size of float in bytes
    size_t charSize = sizeof(char);     // Returns the size of char in bytes
    return (0);
}
```

- Determining the **size of variables**:

```c
int main(void)
{
    int num = 42;
    size_t numSize = sizeof(num); // Returns the size of the 'num' variable in bytes
    char str[] = "Hello, World!";
    size_t strSize = sizeof(str); // Returns the size of the 'str' array in bytes
    return (0);
}
```
