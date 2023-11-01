---
layout: default
title: strlcpy function
parent: string.h
grand_parent: C Programming Language
---

# strlcpy Function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man strlcpy](https://linux.die.net/man/3/strlcpy)

The `strlcpy` function copies the content of one string `src` to another string `dst` while ensuring that the resulting string is null-terminated and does not exceed a specified buffer size. It returns the length of the source string.

## Syntax

```c
size_t strlcpy(char *dst, const char *src, size_t size);
```

### Parameters

- `dst`: The destination string where the content of `src` is copied.
- `src`: The source string to be copied to `dst`.
- `size`: The size of the buffer (including the null-terminator) to prevent buffer overflows.

### Return Value

Returns the length of the source string. If the buffer size is insufficient to accommodate the entire source string, it returns the required buffer size.

## Example

In the following example we use the `strlcpy` function to copy the string "Hello, World!" to an empty string with insuficient space to hold the entire source string, then we output the destination string and the lenght it would need to fit the entire source string.

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char destination[10];
    const char *source = "Hello, World!";
    size_t source_length;

    source_length = strlcpy(destination, source, sizeof(destination));
    printf("Copied string: %s\n", destination);
    printf("Source length: %zu\n", source_length);
    return (0));
}
```
