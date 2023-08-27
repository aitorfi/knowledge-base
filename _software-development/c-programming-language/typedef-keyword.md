---
layout: default
title: typedef keyword
parent: C Programming Language
---

# typedef keyword

C
{: .label .label-blue }

Keyword
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [Structures](../structures)

The `typedef` keyword is used to create new names for existing data types. It essentially provides a way to define aliases for data types.

## Syntax

### Primitive types

In the following example we define *Age* as an alias for the `int` data type and we declare avariable using the alias. The only thing that changes here is the readability of the code.

```c
typedef int Age;

int main(void)
{
    Age person_age = 32;
    return (0);
}
```

### Complex types

In the following example we use **typedef** to define aliases for two structures making the declaration of struct instances easier to read.

{: .info }
> When we use **typedef** with structures the name of the struct is optional as shown in the example bellow.

```c
typedef struct 
{
    char first_name[50];
    char last_name[50];
} FullName;

typedef struct car
{
    char brand[20];
    int year;
} Car;

int main(void)
{
    FullName full_name = {"Erlich", "Bachman"};
    Car car = {"Toyota", 2022};
    return (0);
}
```
