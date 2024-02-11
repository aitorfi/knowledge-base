---
layout: default
title: pipe function
parent: unistd.h
grand_parent: C Programming Language
---

# pipe function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [man pipe](https://man7.org/linux/man-pages/man2/pipe.2.html)

The pipe function is used to create a pipe, which is a unidirectional communication channel that can be used for inter-process communication (IPC) between a parent process and its child processes.

## Syntax

```c
#include <unistd.h>

int pipe(int pipefd[2]);
```

### Parameters

- **pipefd:** An array of two integers where the file descriptors for the read and write ends of the pipe will be stored. pipefd[0] refers to the read end of the pipe, and pipefd[1] refers to the write end.

### Return value

- If the pipe is successfully created, the function returns 0.

- If an error occurs, -1 is returned, and errno is set to indicate the error.

## Usage example

```c
#include <stdio.h>
#include <unistd.h>

int main(void)
{
    int pipefd[2];

    if (pipe(pipefd) == -1)
    {
        perror("Pipe creation failed");
        return 1;
    }
    printf("Pipe created successfully\n");
    return (0);
}
```
