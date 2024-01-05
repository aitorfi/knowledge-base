---
layout: default
title: ttyname function
parent: unistd.h
grand_parent: C Programming Language
---

# ttyname function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [isatty function](../isatty-function)

The ttyname function returns a pointer to the null-terminated string associated with the given terminal device file descriptor. This function is typically used to determine the name of the terminal device associated with a given file descriptor.

## Syntax

```c
#include <unistd.h>

char *ttyname(int fd);
```

### Parameters

**fd:** The file descriptor representing the terminal device.

### Return value

If the given file descriptor is associated with a terminal device, the function returns a pointer to the null-terminated string representing its name. Otherwise, a null pointer is returned.

## Usage example

In the following example we assume that standard input is connected to a terminal to retrieve and print its name.

```c
#include <stdio.h>
#include <unistd.h>

int main(void)
{
    int fd;
    char *terminalName;

    fd = 0; // Assuming standard input is connected to a terminal
    terminalName = ttyname(fd);
    if (terminalName != NULL)
        printf("Terminal name: %s\n", terminalName);
    else
        printf("Not associated with a terminal.\n");
    return (0);
}
```
