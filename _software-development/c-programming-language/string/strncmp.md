---
layout: default
title: strncmp function
parent: string.h
grand_parent: C Programming Language
---

# strncmp function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man strncmp](https://linux.die.net/man/3/strncmp)

The `strncmp` function is used to compare a specified number of characters in two null-terminated strings. It compares the characters in the two strings up to a specified maximum length and returns an integer value indicating the result of the comparison.

## Syntax

```c
int strncmp(const char *str1, const char *str2, size_t n);
```

### Parameters

- `str1`: A pointer to the first null-terminated string to be compared.
- `str2`: A pointer to the second null-terminated string to be compared.
- `n`: The maximum number of characters to compare.

### Return value

Returns a value less than, equal to, or greater than zero, depending on whether `str1` is lexicographically less than, equal to, or greater than `str2`, respectively.

## Example

In the following example we use the `strncmp` function to compare the strings "apple" and "appetite" adn based on the return value output which is lexicographically greater or wether they are equal.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    const char *str1 = "apple";
    const char *str2 = "appetite";
    int result = strncmp(str1, str2, 3);
    
    if (result < 0)
        printf("str1 is lexicographically less than str2.\n");
    else if (result == 0)
        printf("str1 is equal to str2.\n");
    else
        printf("str1 is lexicographically greater than str2.\n");
    return (0);
}
```
