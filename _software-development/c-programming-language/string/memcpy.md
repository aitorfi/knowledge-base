---
layout: default
title: memcpy function
parent: string.h
grand_parent: C Programming Language
---

# memcpy function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man memcpy](https://man7.org/linux/man-pages/man3/memcpy.3.html), [memmove function](../memmove)

The `memcpy` function copies `n` bytes from the memory area pointed to by `src` to the memory area pointed to by `dest`.

{: .warning }
The memory areas must not overlap as the behavior is undefined, that's why it is better to use the memmove function instead.

## Syntax

```c
void *memcpy(void *dest, const void *src, size_t n);
```

### Parameters

- **dest:** A pointer to the destination memory area.
- **src:** A pointer to the source memory area.
- **n:** The number of bytes to be copied.

### Return value

Returns a pointer to the destination memory area `dest`.

## Example

In the following example we use the `memcpy` function to copy the string "Hello, World!" to an empty character array.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char source[] = "Hello, World!";
    char destination[20];

    memcpy(destination, source, strlen(source) + 1);
    printf("Copied string: %s\n", destination);
    return (0);
}
```
