---
layout: default
title: getenv function
parent: stdlib.h
grand_parent: C Programming Language
---

# getenv function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

The getenv function searches the environment list to find the environment variable specified by the parameter `name` and returns a pointer to the associated value string.

## Syntax

```c
#include <stdlib.h>

char *getenv(const char *name);
```

### Parameters

- **name:** A pointer to a null-terminated string containing the name of the requested environment variable.

### Return Value

If the environment variable exists, the function returns a pointer to the associated value string. Otherwise, a null pointer is returned.

## Usage Example

In this example, the program retrieves the value of the "HOME" environment variable using the getenv function. If the variable exists, it prints the value; otherwise, it notifies that the variable was not found.

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *homePath;

    homePath = getenv("HOME");
    if (homePath != NULL)
        printf("The value of HOME is: %s\n", homePath);
    else
        printf("HOME environment variable not found.\n");
    return (0);
}
```
