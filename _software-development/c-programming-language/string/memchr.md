---
layout: default
title: memchr function
parent: string.h
grand_parent: C Programming Language
---

# memchr function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man memchr](https://man7.org/linux/man-pages/man3/memchr.3.html)

The `memchr` function searches for a specific byte in a block of memory. It scans the first `n` bytes of the memory area pointed to by `ptr` for the first occurrence of the byte `c`.

## Syntax

```c
void *memchr(const void *ptr, int c, size_t n);
```

### Parameters

- **ptr:** A pointer to the memory area to be searched.
- **c:** The byte to be located.
- **n:** The number of bytes to be examined.

### Return value

- If the byte `c` is found, a pointer to the first occurrence is returned.
- If `c` is not found within the first `n` bytes, the function returns `NULL`.

## Example

In the following example we use the `memchr` function to search for a byte containing the value 'W' in the string "Hello World!", if the byte is located we print the position at which it was located else we print an error message.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    const char str[] = "Hello, World!";
    const char *ptr = memchr(str, 'W', strlen(str));
    
    if (ptr != NULL)
        printf("Found 'W' at position %ld\n", ptr - str);
    else
        printf("Character not found.\n");
    return (0);
}
```
