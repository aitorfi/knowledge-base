---
layout: default
title: printf function
parent: stdio.h
grand_parent: C Programming Language
---

# printf function

C
{: .label .label-blue }

Function
{: .label .label-yellow }

Reference manual
{: .label .label-yellow }

@see [variadic functions](../../variadic-functions)

The printf function is part of the standard C library and is defined in the `<stdio.h>` header. It stands for "print formatted" and is used for sending formatted output to the standard output (usually the console).

## Syntax

```c
#include <stdio.h>

int printf(const char *format, ...);
```

### Parameters

- **format:** A string containing format specifiers and literal characters.
- **...:**  A variable number of arguments corresponding to the format specifiers in the *format* string.

Here is a list of common **format specifiers** used as placeholders in the *format* string:

- **%d and %i**: Placeholder for a decimal integer.
- **%u**: Placeholder for an unsigned integer.
- **%o**: Placeholder for an octal integer.
- **%x**: Placeholder for a hexadecimal integer in lowercase.
- **%X**: Placeholder for a hexadecimal integer in uppercase.
- **%f**: Placeholder for a floating-point number.
- **%c**: Placeholder for a single character.
- **%s**: Placeholder for a string (char *).
- **%p**: Placeholder for a void pointer printed in hexadecimal.
- **%%**: Prints the '%' character.

The printf function supports various **formatting flags** that affect how the output is displayed. These flags are preceded by the percent sign (%) and are placed between the percent sign and the format specifier.

```
%[flags][width][.precision][length]specifier
```

Here is a list of common flags:

- **- :** Left-justifies the value with blanks on the right side (the default is right justification). This flag overrides the 0 flag if both are given.
- **0 :** The default behavior is to right-justify the value padding it with blanks on the left side. The 0 flag uses the '0' character instead of blanks.
- **. :** Separate the width and precision with a period (.).
- **# :** Used with the o, x, or X specifiers, it adds a prefix (0, 0x, or 0X) to octal or hexadecimal values. For f conversions the result will always contain a decimal point, even if no digits follow it.
- **+ :** A sign (+ or -) should always be placed before a number produced by a signed conversion. By default a sign is used only for negative numbers. The + flag overrides a space if both are used.
- **' ' (space character):** If no sign character is present insert a space before positive values.

### Return value

The printf function return the number of characters printed (excluding the null-terminator) if successful or a negative value otherwise.

## Usage example

In this example, the printf function is used to format and print various data types. The return value is used to count the total number of characters printed to the console.

```c
#include <stdio.h>

int main(void)
{
    int age = 30;
    double height = 175.5;
    char grade = 'A';
    char name[] = "John";

    int charCount = printf("Name: %s\n", name);
    charCount += printf("Age: %d\n", age);
    charCount += printf("Height: %.2f\n", height);
    charCount += printf("Grade: %c\n", grade);
    printf("Total characters printed: %d\n", charCount);
    return (0);
}
```
