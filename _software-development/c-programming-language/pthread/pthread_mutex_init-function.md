---
layout: default
title: pthread_mutex_init function
parent: pthread.h
grand_parent: C Programming Language
---

# pthread_mutex_init function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [pthread_mutex_destroy function](../pthread_mutex_destroy-function), [pthread_mutex_lock function](../pthread_mutex_lock-function), [pthread_mutex_unlock function](../pthread_mutex_unlock-function)

The pthread_mutex_init function is used to initialize a mutex (mutual exclusion) object with specified attributes. Mutexes are synchronization primitives used to protect shared resources from simultaneous access by multiple threads.

{: .warning }
> Remember to destroy the mutex with the pthread_mutex_destroy function once you are done using it.

## Syntax

```c
#include <pthread.h>

int pthread_mutex_init(
    pthread_mutex_t *mutex,
    const pthread_mutexattr_t *attr
);
``` 

### Parameters

- **mutex:** A pointer to a variable of type pthread_mutex_t that will be initialized by the function. This mutex object is used to control access to shared resources.

- **attr:** A pointer to a variable of type pthread_mutexattr_t that specifies the attributes for the mutex. If NULL is passed, default attributes will be used.

### Return value

- If the mutex is successfully initialized, the function returns 0.

- If an error occurs, a non-zero error code is returned. Possible error codes include EINVAL (invalid mutex attributes) and ENOMEM (insufficient memory to initialize the mutex).

## Usage example

In the following example we initialize a global mutex variable mutex using `pthread_mutex_init`, then we create three threads, each executing the `thread_function` function. Each thread locks the mutex with `pthread_mutex_lock`, enters a critical section where it prints its ID, and then unlocks the mutex with `pthread_mutex_unlock`. After all threads have finished executing, we destroy the mutex using `pthread_mutex_destroy`. This example demonstrates how to use mutexes to protect critical sections of code from concurrent execution by multiple threads.

```c
#include <stdlib.h>
#include <stdio.h>
#include <pthread.h>

pthread_mutex_t mutex;

void *thread_function(void *arg)
{
    int *thread_id;

    pthread_mutex_lock(&mutex); // Lock the mutex
    *thread_id = arg;
    printf("Thread %d is inside the critical section\n", *thread_id);
    pthread_mutex_unlock(&mutex); // Unlock the mutex
    return (NULL);
}

int main(void)
{
    pthread_t threads[3];
    int thread_args[3] = {1, 2, 3};

    // Initialize the mutex
    int init_result = pthread_mutex_init(&mutex, NULL);
    if (init_result != 0) {
        fprintf(stderr, "Error initializing mutex: %d\n", init_result);
        return (EXIT_FAILURE);
    }
    // Create three threads
    for (int i = 0; i < 3; i++) {
        int create_result = pthread_create(&threads[i], NULL, thread_function, &thread_args[i]);
        if (create_result != 0) {
            fprintf(stderr, "Error creating thread %d: %d\n", i+1, create_result);
            return (EXIT_FAILURE);
        }
    }
    // Join all threads
    for (int i = 0; i < 3; i++) {
        int join_result = pthread_join(threads[i], NULL);
        if (join_result != 0) {
            fprintf(stderr, "Error joining thread %d: %d\n", i+1, join_result);
            return (EXIT_FAILURE);
        }
    }
    // Destroy the mutex
    int destroy_result = pthread_mutex_destroy(&mutex);
    if (destroy_result != 0) {
        fprintf(stderr, "Error destroying mutex: %d\n", destroy_result);
        return (EXIT_FAILURE);
    }
    printf("All threads have finished executing\n");
    return (EXIT_SUCCESS);
}
```
