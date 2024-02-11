---
layout: default
title: unlink function
parent: unistd.h
grand_parent: C Programming Language
---

# unlink function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man unlink](https://man7.org/linux/man-pages/man2/unlink.2.html)

The unlink function is used to delete a name from the file system. If the name was the last link to the file, the file is deleted and its space is deallocated.

## Syntax

```c
#include <unistd.h>

int unlink(const char *pathname);
```

### Parameters

- **pathname:** The path to the file to be unlinked (deleted).

### Return value

- If the file is successfully unlinked, the function returns 0.

- If an error occurs, -1 is returned, and errno is set to indicate the error.

## Usage example

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>

int main(void)
{
    if (unlink("file.txt") == -1)
    {
        perror("Failed to unlink file");
        return (EXIT_FAILURE);
    }
    printf("File unlinked successfully\n");
    return (EXIT_SUCCESS);
}
```
