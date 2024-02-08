---
layout: default
title: pthread_join function
parent: pthread.h
grand_parent: C Programming Language
---

# pthread_join function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [pthread_create function](../pthread_create-function)

The pthread_join function is used to wait for a thread to terminate and retrieve its exit status. It blocks the calling thread until the specified thread terminates.

## Syntax

```c
#include <pthread.h>

int pthread_join(pthread_t thread, void **retval);
```

### Parameters

- **thread:** The thread ID of the thread to be joined. This thread must be joinable.

- **retval:** A pointer to a variable where the exit status of the joined thread will be stored. This value can be NULL if the exit status is not required.

### Return value

- If the thread is successfully joined, the function returns 0.

- If an error occurs, a non-zero error code is returned. Possible error codes include EINVAL (invalid thread ID or already joined thread) and ESRCH (no thread could be found with the specified ID).

## Usage example

In this example, the program creates a new thread using pthread_create and waits for it to terminate using pthread_join. The exit status of the joined thread is stored in the thread_return_value variable.

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
    void *thread_return_value;
    int join_result;

    pthread_create(&thread, NULL, thread_function, NULL);
    join_result = pthread_join(thread, &thread_return_value);
    if (join_result == 0)
        printf("Thread joined successfully\n");
    else
        fprintf(stderr, "Error joining thread: %d\n", join_result);
    // Main thread continues execution after the joined thread has terminated
    return (0);
}
```
