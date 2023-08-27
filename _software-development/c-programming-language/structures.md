---
layout: default
title: Structures
parent: C Programming Language
---

# Structures

C
{: .label .label-blue }

Reference manual
{: .label .label-yellow }

@see [typedef keyword](../typedef-keyword)

Structures are a fundamental feature in C programming. They allow you to group related variables together under a single user-defined data type, facilitating organization and manipulation of complex data.

## Syntax

On the following example we define two structures *Date* and *Person*. The struct *Date* holds three variables of type `int`, one for the day, one for the month and one for the year, The struct *Person* holds a `char` array for the name, a `float` variable for the height and an instance of the *Date* struct for the birth date.

To initialize the data of a struct we separate the values of the members by commas in the order in which they were defined and we enclose them in braces: `{ value1, value2, ... }`.

To access a member of a struct we use the name of the instance followed by the dot operator (.) followed by the name of the member: `person.name`. If the instance of the struct is a pointer we use the arrow operator (->) instead of the dot operator (.): `date->day`.

{: .info }
> To make the use of struct more readable, the **typedef** keyword can be employed to define an analias for a structure.

```c
#include <stdio.h>

struct Date
{
    int day;
    int month;
    int year;
};

struct Person 
{
    char name[60];
    float height;
    struct Date birth_date;
};

void print_date(struct Date *date);

int main(void)
{
    struct Person person = {"Mike", 1.76, {12, 4, 1989}};
    printf("Name: %s\n", person.name);
    printf("Height: %.2f\n", person.height);
    print_date(&person.birth_date);
    return (0);
}

void print_date(struct Date *date)
{
    printf("Birth Date Day: %d\n", date->day);
    printf("Birth Date Month: %d\n", date->month);
    printf("Birth Date Year: %d\n", date->year);
}
```
