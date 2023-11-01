---
layout: default
title: strlcat function
parent: string.h
grand_parent: C Programming Language
---

# strlcat function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man strlcat](https://linux.die.net/man/3/strlcat)

The `strlcat` function appends the content of one string `src` to another string `dst` while ensuring that the resulting string is null-terminated and does not exceed a specified buffer size. It returns the total length of the resulting string.

## Syntax

```c
size_t strlcat(char *dst, const char *src, size_t size);
```

### Parameters

- `dst`: The destination string to which the content of `src` is appended.
- `src`: The source string to be appended to `dst`.
- `size`: The size of the buffer (including the null-terminator) to prevent buffer overflows.

### Return Value

Returns the total length of the resulting string after concatenation. If the buffer size is insufficient to accommodate the entire result, it returns the required buffer size.

## Example

In the following example we use the `strlcat` function to append the string "World!" to the string "Hello, " and then we output the resulting string "Hello, World!" and its length.

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char destination[20] = "Hello, ";
    const char *source = "World!";
    size_t total_length;

    total_length = strlcat(destination, source, sizeof(destination));
    printf("Concatenated string: %s\n", destination);
    printf("Total length: %zu\n", total_length);
    return (0);
}
```
