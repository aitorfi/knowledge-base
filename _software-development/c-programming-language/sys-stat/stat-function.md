---
layout: default
title: stat function
parent: sys/stat.h
grand_parent: C Programming Language
---

# stat function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [struct stat](../struct-stat)

The `stat` function retrieves information about a file or symbolic link and stores it in a structure pointed to by the `struct stat` pointer provided as an argument.

## Syntax

```c
#include <sys/stat.h>

int stat(
    const char *restrict pathname,
    struct stat *restrict statbuf
);
```

### Parameters

- **pathname:** A pointer to a null-terminated string containing the path of the file or symbolic link whose information is to be retrieved.

- **statbuf:** A pointer to a struct stat variable where the retrieved file information will be stored.

### Return value

- If the operation is successful, the function returns 0.

- If an error occurs, -1 is returned, and errno is set to indicate the error.

## Usage example

In the following example we use the `stat` function to retrieve information about a file. Note that to print the file permissions you can perform a binary and between the `file_info.st_mode` variable and the value `0777`.

```c
#include <stdlib.h>
#include <stdio.h>
#include <sys/stat.h>

int main(void)
{
    const char *file_path = "example.txt";
    struct stat file_info;

    if (stat(file_path, &file_info) == -1)
    {
        perror("Failed to retieve file information");
        return (EXIT_FAILURE);
    }
    printf("File size: %lld bytes\n", (long long)file_info.st_size);
    printf("File permissions: %o\n", file_info.st_mode & 0777);
    return (EXIT_SUCCESS);
}
```
