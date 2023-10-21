---
layout: default
title: memcmp function
parent: string.h
grand_parent: C Programming Language
---

# memcmp function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man memcmp](https://man7.org/linux/man-pages/man3/memcmp.3.html)

The `memcmp` function compares two blocks of memory. It compares the first `n` bytes of the memory areas pointed to by `ptr1` and `ptr2`.

## Syntax

```c
int memcmp(const void *ptr1, const void *ptr2, size_t n);
```

### Parameters

- **ptr1:** A pointer to the first memory area to be compared.
- **ptr2:** A pointer to the second memory area to be compared.
- **n:** The number of bytes to be compared.

### Return value

Returns an integer value less than, equal to, or greater than zero, depending on whether the first differing byte in `ptr1` is less than, equal to, or greater than the corresponding byte in `ptr2`.

## Example

In the following example we use the `memcmp` function to compare the strings "Hello" and "Helxo", then we will print a message if they are equal, that is if the return value is 0, or a different message if they are different.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    const char str1[] = "Hello";
    const char str2[] = "Helxo";
    int result = memcmp(str1, str2, 5);

    if (result == 0)
        printf("Strings are equal.\n");
    else
        printf("Strings are not equal.\n");
    return (0);
}
```
