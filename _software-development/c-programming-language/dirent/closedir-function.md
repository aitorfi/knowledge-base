---
layout: default
title: closedir function
parent: dirent.h
grand_parent: C Programming Language
---

# closedir function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [opendir function](../opendir-function), [readdir function](../readdir-function)

The closedir function closes the directory stream opened with opendir releasing resources associated with the directory stream.

## Syntax

```c
#include <dirent.h>

int closedir(DIR *dirp);
```

### Parameters

- **dirp:** A pointer to the `DIR` type representing the directory stream that will be closed.

### Return value

- If the directory stream is successfully closed the function returns 0.
- If an error occurs it returns -1.

## Usage example

The following example is a very simple program that opens a directory with the `opendir` function and closes it with the `closedir` function.

```c
#include <stdio.h>
#include <dirent.h>

int main(void)
{
    const char *directoryPath;
    DIR *dirStream;

    directoryPath = "/path/to/directory";
    dirStream = opendir(directoryPath);
    if (dirStream != NULL)
    {
        if (closedir(dirStream) == 0)
            printf("Directory stream closed successfully.\n");
        else
            perror("Error closing directory stream");
    }
    else
    {
        perror("Error opening directory stream");
    }
    return (0);
}
```
