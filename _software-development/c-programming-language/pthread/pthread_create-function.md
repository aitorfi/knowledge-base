---
layout: default
title: pthread_create function
parent: pthread.h
grand_parent: C Programming Language
---

# pthread_create function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [pthread_detach function](../pthread_detach-function), [pthread_join function](../pthread_join-function)

The pthread_create function is used to create a new thread within a program. It allows developers to specify the function that will be executed by the new thread, along with any arguments that need to be passed to that function.

## Syntax

```c
#include <pthread.h>

int pthread_create(
    pthread_t *thread,
    const pthread_attr_t *attr,
    void *(*start_routine)(void*),
    void *arg
);
```

### Parameters

- **thread:** A pointer to a variable of type pthread_t where the thread ID of the newly created thread will be stored.

- **attr:** A pointer to a variable of type pthread_attr_t that specifies the attributes for the new thread. If NULL is passed, default attributes will be used.

- **start_routine:** A pointer to the function that will be executed by the new thread. This function must accept a single argument of type void* and return a void*.

- **arg:** A pointer to the argument that will be passed to the start_routine function when the new thread is created. This argument can be used to pass data to the thread function.

### Return value

- If the thread is successfully created, the function returns 0.

- If an error occurs, a non-zero error code is returned. Possible error codes include EAGAIN (insufficient resources to create another thread) and EINVAL (invalid attributes).

## Usage example

In the following example, the program creates a new thread using pthread_create, specifying the function thread_function as the entry point for the new thread. The &thread_id argument is passed to thread_function to provide a unique identifier for the thread. The main thread then waits for the new thread to finish using pthread_join.

```c
#include <stdio.h>
#include <pthread.h>

void *thread_function(void *arg)
{
    int *thread_id = (int *)arg;
    printf("Thread %d is running\n", *thread_id);
    pthread_exit(NULL);
}

int main(void)
{
    pthread_t thread;
    int thread_id;
    int create_result;

    thread_id = 1;
    create_result = pthread_create(&thread, NULL, thread_function, &thread_id);
    if (create_result == 0)
    {
        printf("Thread created successfully\n");
        pthread_join(thread, NULL); // Wait for the thread to finish
    }
    else
    {
        fprintf(stderr, "Error creating thread: %d\n", create_result);
    }
    return (0);
}
```
