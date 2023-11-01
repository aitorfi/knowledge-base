---
layout: default
title: strlen function
parent: string.h
grand_parent: C Programming Language
---

# strlen function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man strlen](https://man7.org/linux/man-pages/man3/strlen.3.html)

The `strlen` function calculates the length of a null-terminated string by counting the number of characters in the string (excluding the null terminator). It returns the length of the string.

## Syntax

```c
size_t strlen(const char *str);
```

### Parameters

- `str`: The input string for which the length is to be determined.

### Return value

Returns the length of the string, which is the number of characters in the string.

## Example

In the following example we use the `strlen` function to count the number of characters in the string "Hello, World!" and we output it.

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    const char str[] = "Hello, World!";
    size_t length = strlen(str);

    printf("String length: %zu\n", length);
    return (0);
}
```
