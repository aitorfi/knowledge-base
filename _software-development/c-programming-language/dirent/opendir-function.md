---
layout: default
title: opendir function
parent: dirent.h
grand_parent: C Programming Language
---

# opendir function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [readdir function](../readdir-function), [closedir function](../closedir-function)

The opendir function opens a directory stream corresponding to the directory named by the given path. It returns a pointer to the opened directory stream, which can subsequently be used in calls to the readdir function.

{: .warning }
> Remember to close the directory with the `closedir` function once you are done with it.

## Syntax

```c
#include <dirent.h>

DIR *opendir(const char *dirname);
```

### Parameters

- **dirname:** A pointer to a null-terminated string containing the path to the directory that will be opened.

### Return value

- If the directory stream is successfully opened, the function returns a pointer to the `DIR` type representing the directory stream.
- If an error occurs, the function returns a null pointer.

## Usage example

In the following example we use the `opendir` function to open a directory and output if it was successfully opened or not.

```c
#include <stdio.h>
#include <dirent.h>

int main(void) {
    const char *directoryPath;
    DIR *dirStream;

    directoryPath = "/path/to/directory";
    dirStream = opendir(directoryPath);
    if (dirStream != NULL)
    {
        printf("Directory stream opened successfully.\n");
        closedir(dirStream);
    }
    else
    {
        perror("Error opening directory stream");
    }
    return (0);
}
```
