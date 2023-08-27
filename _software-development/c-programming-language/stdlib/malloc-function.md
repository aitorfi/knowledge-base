---
layout: default
title: malloc function
parent: stdlib.h
grand_parent: C Programming Language
---

# malloc function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [free function](../free-function), [sizeof operator](../../sizeof-operator), [Pointers](../../pointers)

The malloc function in the C programming language is used for dynamic memory allocation. It allows programmers to allocate memory during program execution, enabling the creation of data structures of varying sizes based on runtime requirements. The allocated memory is taken from the heap, and it persists until explicitly deallocated using the `free` function.

The memory allocated by malloc is uninitialized. It may contain random values, so you need to initialize it before using it.

## Syntax

```c
#include <stdlib.h>

void *malloc(size_t size);
```

### Parameters

The `malloc` function receives a single parameter which holds the size of the requested memory block in bytes. This parameter is usually filled using the `sizeof` operator.

### Return value

The malloc function returns a pointer to the first byte of the allocated memory block. If the allocation fails due to insufficient memory, it returns NULL.

{: .warning }
> Always check the return value of malloc to ensure that memory allocation was successful. If it returns NULL, it means that the memory allocation failed. See the usage example bellow.

## Usage example

```c
#include <stdlib.h>

int main(void)
{
    int *arr;
    
    arr = (int *)malloc(10 * sizeof(int));
    if (arr == NULL)
        handle_malloc_error();
    return (0);
}
```

In the previous example we declared a pointer to an integer and we assigned it the return value of the `malloc` function which is a pointer to the begining of the memory block we requested. The pointer returned by `malloc` is of type `void` that's why we have to parse it to the desired type, in this case `(int *)`. To determin the size of the memory block we want to allocate we used the `sizeof` operator to determin the size of one integer and then multiplied it by 10 so now the array `*arr` has enough space to hold 10 integers.

Right after attempting to allocate the memory we checked if the pointer filled by the call to `malloc` was NULL which would mean an error occurred during the memory allocation. This is an important step if we want to prevent unexpected behaviors by our program.
