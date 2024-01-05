---
layout: default
title: isatty function
parent: unistd.h
grand_parent: C Programming Language
---

# isatty function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [ttyname function](../ttyname-function)

The isatty function checks whether the given file descriptor refers to a terminal.

## Syntax

```c
#include <unistd.h>

int isatty(int fd);
```

### Parameters

- **fd:** The file descriptor to be checked.

### Return value

If the given file descriptor refers to a terminal the function returns 1, otherwise it returns 0.

## Usage example

In the following example we use the `isatty` funtion to check if standard input refers to a terminal.

```c
#include <stdio.h>
#include <unistd.h>

int main(void) {
    int fd;

    fd = 0;
    if (isatty(fd))
        printf("File descriptor %d refers to a terminal.\n", fd);
    else
        printf("File descriptor %d does not refer to a terminal.\n", fd);
    return (0);
}
```
