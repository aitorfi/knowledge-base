---
layout: default
title: free function
parent: stdlib
grand_parent: C Programming Language
---

# free function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [malloc function](../malloc-function)

The free function in the C programming language is used to deallocate memory that was previously allocated using dynamic memory allocation functions like `malloc`, `calloc`, or `realloc`. Deallocating memory with free is crucial to prevent memory leaks, where memory is consumed but not released back to the system.

## Syntax

```c
#include <stdlib.h>

void free(void *ptr);
```

### Parameters

The `free` function receives a single argument which is a pointer the memory block that you want to deallocate.

## Usage example

In the following example we use the `malloc` function to allocate memory for an array of 10 integers, we call a function that performs some undefined operations over the array and once we are done operating with the array we use the `free` function to deallocate the memory used by the array.

```c
#include <stdlib.h>

int main(void)
{
    int *arr;
    
    arr = (int *)malloc(10 * sizeof(int)); // Allocate memory
    do_something(arr);
    free(arr); // Deallocate memory
    return (0);
}
```

{: .warning }
> When you're done using dynamically allocated memory, make sure to free it to prevent memory leaks. Failing to do so can lead to your program consuming more and more memory over time.
