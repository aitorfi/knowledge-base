---
layout: default
title: memset function
parent: string.h
grand_parent: C Programming Language
---

# memset function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man memset](https://man7.org/linux/man-pages/man3/memset.3.html)

The `memset` function sets the first `n` bytes of the memory area pointed to by `ptr` to the specified byte value.

## Syntax

```c
void *memset(void *ptr, int value, size_t n);
```

### Parameters

- **ptr:** A pointer to the memory area to be filled.
- **value:** The byte value to be set (usually in the range 0 to 255).
- **n:** The number of bytes to be set.

### Return value

Returns a pointer to the memory area `ptr`.

## Example

In the following example we use the `memset` function to fill the first 10 bytes of a character array to the character 'A'.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char str[20];
    
    memset(str, 'A', 10);
    printf("Filled string: %s\n", str);
    return (0);
}
```
