---
layout: default
title: readdir function
parent: dirent.h
grand_parent: C Programming Language
---

# readdir function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [opendir function](../opendir-function), [closedir function](../closedir-function)

The readdir function reads the next entry from the directory stream obtained from the opendir function. It returns a pointer to a structure representing the directory entry.

{: .warning }
> Remember to close the directory with the `closedir` function once you are done with it.

## Syntax

```c
#include <dirent.h>

struct dirent *readdir(DIR *dirp);
```

### Parameters

- **dirp:** A pointer to the `DIR` type representing the directory stream.

### Return value

- The function returns a pointer to a structure of type `struct dirent` representing a directory entry.
- When the end of the directory stream is reached the function returns a null pointer.

## Usage example

In the following example we use the `readdir` function to output the name of all the files in a directory.

```c
#include <stdio.h>
#include <dirent.h>

int main(void) {
    const char *directoryPath;
    DIR *dirStream;
    struct dirent *dirEntry;

    directoryPath = "/path/to/directory";
    dirStream = opendir(directoryPath);
    if (dirStream != NULL)
    {
        while ((dirEntry = readdir(dirStream)) != NULL)
        {
            printf("File name: %s\n", dirEntry->d_name);
        }
        closedir(dirStream);
    }
    else
    {
        perror("Error opening directory stream");
    }
    return (0);
}
```
