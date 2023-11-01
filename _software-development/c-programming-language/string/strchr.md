---
layout: default
title: strchr function
parent: string.h
grand_parent: C Programming Language
---

# strchr function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man strchr](https://man7.org/linux/man-pages/man3/strchr.3.html)

The `strchr` function searches for the first occurrence of a specified character `c` in the given string `str`. It returns a pointer to the first occurrence of the character, or a null pointer if the character is not found within the string.

## Syntax

```c
char *strchr(const char *str, int c);
```

### Parameters

- `str`: The input string to search.
- `c`: The character to be located within the string.

### Return Value

Returns a pointer to the first occurrence of the character `c` within the string `str`. If `c` is not found, it returns `NULL`.

## Example

In the following example we use the `strchr` function to locate the character 'W' in the string "Hello, World!" and output its position withing the string by using the pointer returned by `strchr`.

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    const char str[] = "Hello, World!";
    char *ptr = strchr(str, 'W');

    if (ptr != NULL)
        printf("Found 'W' at position %ld\n", ptr - str);
    else
        printf("Character not found.\n");
    return (0);
}
```
