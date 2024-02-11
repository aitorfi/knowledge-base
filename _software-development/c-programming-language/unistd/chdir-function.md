---
layout: default
title: chdir function
parent: unistd.h
grand_parent: C Programming Language
---

# chdir function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man chdir](https://man7.org/linux/man-pages/man2/chdir.2.html)

The chdir function is used to change the current working directory of the calling process to the specified directory.

## Syntax

```c
#include <unistd.h>

int chdir(const char *path);
```

### Parameters

- **path:** A pointer to a null-terminated string containing the path of the directory to change to.

### Return value

- If the directory is successfully changed, the function returns 0.

- If an error occurs, -1 is returned, and errno is set to indicate the error.

## Usage example


```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>

int main(void)
{
    if (chdir("/path/to/directory") == -1)
    {
        perror("chdir");
        return (EXIT_FAILURE);
    }
    printf("Current working directory changed successfully\n");
    return (EXIT_SUCCESS);
}
```
