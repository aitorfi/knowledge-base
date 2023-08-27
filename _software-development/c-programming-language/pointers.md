---
layout: default
title: Pointers
parent: C Programming Language
---

# Pointers

C
{: .label .label-blue }

Reference manual
{: .label .label-yellow }

@see [malloc function](../stdlib/malloc-function)

A pointer is a variable that stores the memory address of another variable. It allows you to indirectly access and modify the data stored in that memory location. Pointers provide a way to work with memory directly, offering greater flexibility and efficiency.

## Purpose

Pointers serve several key purposes in C programming:

- **Dynamic Memory Allocation:** Pointers are used to manage memory dynamically using functions like `malloc`, `calloc`, and `realloc`, enabling the creation of data structures with variable sizes.

- **Efficient Function Calls:** Pointers allow passing large data structures to functions by reference, avoiding the need to copy the entire data.

- **Manipulating Arrays and Strings:** Pointers provide an efficient way to access and modify array elements and characters in strings.

- **Data Structures:** Many advanced data structures, like linked lists and trees, are implemented using pointers to create relationships between different elements.

## Syntax

### Declaration and initialization

In the following example we declare a variable of type `int` called *num*, then we declare a pointer to an `int` called *ptr* and we assign it the address of the variable *num* usign the address-of operator (&).

```c
int main(void)
{
    int num = 10; // Regular int variable.
    int *ptr; // Declaration of a pointer to an int.
    ptr = &num; // Initialization of a pointer.
    return (0);
}
```

### Dereferencing

Dereferencing a pointer means accessing the value stored at the memory location it points to and it is done by using the indirection operator (*). The following example shows a function that recieves two pointers to int and swaps their values. Once the function is executes both pointers will still be pointing to the same memory addresses only the value in those memory addesses will have changed.

```c
void swap(int *a, int *b)
{
    int swap = *a; // Initialize swap with the value pointed by a.
    *a = *b; // Change the value pointed by a to the value pointer by b.
    *b = swap; // Change the value pointed by b to the value of the variable swap.
}
```

### Pointers in functions

In the following example we have a function called *swap* that recieves two pointers and swaps their values. From the *main* function we declare a variable called *a*, as the *swap* function needs a pointer we use the address-of operator (&) to initialize it as a pointer to *a*. For the seccond parameter we declared a variable called *b* and a pointer to *b* called *pb*, as *pb* is already a pointer we can send the address of *b* the same way we did it with *a* or by using the memory address stored in *pb* which points to *b*.

```c
void swap(int *a, int *b)
{
    int swap = *a;
    *a = *b;
    *b = swap;
}

int main(void)
{
    int a = 10;
    int b = 15;
    int *pb = &b;
    swap(&a, pb);
    return (0);
}
```

### Pointers and arrays

In the following example we have two function that recieve a null terminated array of characters, iterate through it and print each character on standard output. In the function *iterate_array* we use an `int` variable as an index to access the elements of the array. In the function *iterate_array_arithmetically* we modify the addess stored in the pointer *str* by adding 1 in each iteration, this way we manage to jump to the next element of the array.

{: .warning }
> Note that the way the array is iterated in the function *iterate_array_arithmetically* works only because array elements are sequentially allocated in memory (one after the other, in order). However, as we've modified the address of the pointer once the loop is finished the pointer no longer points to the first element of the array so if we wanted to iterate over it again we would have to store the address to the first element before the first iteration.

```c
#include <unistd.h>

void iterate_array(char *str)
{
    int i = 0;

    while (str[i] != '\0')
    {
        write(STDOUT_FILENO, &str[i], 1);
        i++;
    }
}

void iterate_array_arithmetically(char *str)
{
    while (*str != '\0')
    {
        write(STDOUT_FILENO, str, 1);
        str++;
    }
}
```
