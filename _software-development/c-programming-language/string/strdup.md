---
layout: default
title: strdup function
parent: string.h
grand_parent: C Programming Language
---

# strdup function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man strdup](https://man7.org/linux/man-pages/man3/strdup.3.html)

The `strdup` function allocates memory for a new string and duplicates the content of the provided string. It returns a pointer to the newly created string. The memory allocated by `strdup` should be released using `free` when it is no longer needed.

## Syntax

```c
char *strdup(const char *str);
```

### Parameters

- `str`: The input string to be duplicated.

### Return Value

Returns a pointer to a new string containing a copy of the input string. If memory allocation fails, it returns `NULL`.

## Example

In the following example we use the `strdup` function to create a copy of the string "Hello, World!" and we output both the original and the copy in case the memory allocation was successful, else we output an error message.

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void) {
    const char *original = "Hello, World!";
    char *duplicate = strdup(original);

    if (duplicate != NULL) {
        printf("Original: %s\n", original);
        printf("Duplicate: %s\n", duplicate);
        free(duplicate);
    } else {
        printf("Memory allocation failed.\n");
    }
    return (0);
}
```
