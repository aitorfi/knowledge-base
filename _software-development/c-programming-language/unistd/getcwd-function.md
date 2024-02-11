---
layout: default
title: getcwd function
parent: unistd.h
grand_parent: C Programming Language
---

# getcwd function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man getcwd](https://man7.org/linux/man-pages/man3/getcwd.3.html)

The getcwd function is used to get the current working directory of the calling process. The directory can be retrieved both from the return value or the first parameter of the function.

## Syntax

```c
#include <unistd.h>

char *getcwd(char *buf, size_t size);
```

### Parameters

- **buf:** A pointer to a buffer where the current working directory path will be stored.

- **size:** The size of the buffer pointed to by buf.

### Return value

- If the current working directory is successfully retrieved, the function returns a string containig the current working directory of the calling process.

- If an error occurs, NULL is returned, and errno is set to indicate the error.

## Usage example

```c
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *dir;

    dir = getcwd(NULL, 0);
    if (dir == NULL)
    {
        perror("Failed to retrieve current working directory");
        return (EXIT_FAILURE);
    }
    printf("Current working directory: %s\n", dir);
    free(dir);
    return (EXIT_SUCCESS);
}
```
