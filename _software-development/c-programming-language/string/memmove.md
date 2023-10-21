---
layout: default
title: memmove function
parent: string.h
grand_parent: C Programming Language
---

# memmove function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man memmove](https://man7.org/linux/man-pages/man3/memmove.3.html), [memcpy function](../memcpy)

The `memmove` function copies `n` bytes from the memory area pointed to by `src` to the memory area pointed to by `dest`.

{: .info}
Unlike memcpy, in memmove the memory areas may overlap so it is generally better to use memmove over memcpy.

## Syntax

```c
void *memmove(void *dest, const void *src, size_t n);
```

### Parameters

- **dest:** A pointer to the destination memory area.
- **src:** A pointer to the source memory area.
- **n:** The number of bytes to be copied.

### Return value

Returns a pointer to the destination memory area `dest`.

## Example

In the following example we use the `memmove` function to copy the string "memmove can handle overlapping areas." starting on position 14 to the same memory area starting on position 20, that is two overlapping memory areas.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char str[] = "memmove can handle overlapping areas.";
    
    memmove(str + 20, str + 14, 10);
    printf("%s\n", str);
    return (0);
}
```
