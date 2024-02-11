---
layout: default
title: dup function
parent: unistd.h
grand_parent: C Programming Language
---

# dup function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man dup](https://man7.org/linux/man-pages/man2/dup.2.html)

The dup function creates a new file descriptor that refers to the same open file as the given file descriptor. The new file descriptor number is guaranteed to be the lowest-numbered file descriptor that was unused in the calling process.

## Syntax

```c
#include <unistd.h>

int dup(int oldfd);
```

### Parameters

- **oldfd:** The file descriptor to be duplicated.

### Return value

- If the duplication is successful, the function returns a new file descriptor that refers to the same open file description as `oldfd`.

- If an error occurs, -1 is returned, and errno is set to indicate the error.

## Usage example

In the following example we use the `dup` function to duplicate the `fd` file descriptor into the `new_fd` file descriptor meaning we now have two different file descriptors that point to the same file.

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main(void)
{
    int fd;
    int new_fd;

    fd = open("file.txt", O_RDONLY);
    if (fd == -1)
    {
        perror("open");
        return (EXIT_FAILURE);
    }
    new_fd = dup(fd);
    if (new_fd == -1)
    {
        perror("File descriptor duplication failed");
        close(fd);
        return (EXIT_FAILURE);
    }
    printf("File descriptor duplicated successfully\n");
    close(fd);
    close(new_fd);
    return (EXIT_SUCCESS);
}
```
