---
layout: default
title: strnstr function
parent: string.h
grand_parent: C Programming Language
---

# strnstr function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

The `strnstr` function is used to find the first occurrence of a substring within a larger string, considering a specified maximum length.

## Syntax

```c
char *strnstr(const char *haystack, const char *needle, size_t haystack_len);
```

### Parameters

- `haystack`: A pointer to the null-terminated string to search within.
- `needle`: A pointer to the null-terminated substring to search for.
- `haystack_len`: The maximum length of the haystack string to consider.

### Return value

Returns a pointer to the first occurrence of the substring `needle` within the `haystack` string, or `NULL` if the substring is not found within the specified length.

## Example

In the following example we use the `strnstr` function to search for the substring "world" within the first 10 characters of the string "Hello, world! How are you?" and output the substring if it was found or an error message if it wasn't.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    const char *haystack = "Hello, world! How are you?";
    const char *needle = "world";
    char *result = strnstr(haystack, needle, 10);
    
    if (result != NULL)
        printf("Substring found: %s\n", result);
    else
        printf("Substring not found within the first 10 characters.\n");
    return (0);
}
```
