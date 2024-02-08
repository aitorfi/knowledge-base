---
layout: default
title: pthread_detach function
parent: pthread.h
grand_parent: C Programming Language
---

# pthread_detach function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [pthread_create function](../pthread_create-function)

The pthread_detach function is used to detach a thread. When a thread is detached, its resources are automatically released when it terminates, without the need for another thread to join it. This allows the thread to run independently without being joined by another thread.

## Syntax

```c
#include <pthread.h>

int pthread_detach(pthread_t thread);
```

### Parameters

- **thread:** The thread ID of the thread to be detached. This thread must be joinable.

### Return value

- If the thread is successfully detached, the function returns 0.

- If an error occurs, a non-zero error code is returned. Possible error codes include EINVAL (invalid thread ID or already detached thread) and ESRCH (no thread could be found with the specified ID).

## Usage example

In the following example, the program creates a new thread using pthread_create and immediately detaches it using pthread_detach. The main thread continues execution without waiting for the detached thread to finish.

```c
#include <stdio.h>
#include <pthread.h>

void *thread_function(void *arg)
{
    // Thread logic
    return (NULL);
}

int main()
{
    pthread_t thread;
    int detach_result;

    pthread_create(&thread, NULL, thread_function, NULL);
    detach_result = pthread_detach(thread);
    if (detach_result == 0)
        printf("Thread detached successfully\n");
    else
        fprintf(stderr, "Error detaching thread: %d\n", detach_result);
    // Main thread continues execution without waiting for the detached thread
    return (0);
}
```
