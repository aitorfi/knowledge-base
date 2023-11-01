---
layout: default
title: strrchr function
parent: string.h
grand_parent: C Programming Language
---

# strrchr Function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man strrchr](https://linux.die.net/man/3/strrchr), [strchr function](../strchr)

The `strrchr` function is used to locate the last occurrence of a specified character within a null-terminated string. It searches the string from the end toward the beginning and returns a pointer to the last occurrence of the character.

{: .info }
> The [strchr](../strchr) function does the same thing except it searches for the first occurrence of the specified character.

## Syntax

```c
char *strrchr(const char *str, int character);
```

### Parameters

- `str`: A pointer to the null-terminated string to search within.
- `character`: The character to search for within the string.

### Return value

Returns a pointer to the last occurrence of the specified character in the string, or `NULL` if the character is not found in the string.

## Example

In the following example we use the `strrchr` function to locate the last occurrence of the character 't' in the string "This is a test string." and output the return value.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    const char *str = "This is a test string.";
    char *result = strrchr(str, 't');
    
    if (result != NULL)
        printf("Last 't' found at: %s\n", result);
    else
        printf("Character 't' not found in the string.\n");
    return (0);
}
```
