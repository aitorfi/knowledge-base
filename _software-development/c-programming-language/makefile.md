---
layout: default
title: Makefile
parent: C Programming Language
---

# Makefile

Makefile
{: .label .label-blue }

C
{: .label .label-blue }

Reference manual
{: .label .label-yellow }

@see [gnu make documentation](https://www.gnu.org/software/make/manual/make.html), [red hat makefile example](https://access.redhat.com/documentation/es-es/red_hat_enterprise_linux/8/html/developing_c_and_cpp_applications_in_rhel_8/example-building-a-c-program-using-a-makefile_managing-more-code-with-make)

A Makefile is a powerful tool used in software development, particularly in compiling and building C programs. A Makefile is a script that specifies how to compile and link a program. It contains rules and instructions for building the software, including information about dependencies and build steps.

## Syntax

### Run a Makefile script

To run a Makefile script we use the `make` command followed by the target we want to run, if no target is specified the default target *all* will be executed.

```bash
make [target]
```

### Variables

Variables in Makefiles are defined with = or :=. They can make your Makefile more flexible and easier to maintain.

```makefile
CC = gcc
CFLAGS = -Wall -Wextra -Werror
```

### Targets and dependencies

A target is defined with a colon (:) after its name followed by its dependencies in the same line and the steps that must be executed go in newlines and indented.

In the following example we define a variable called *NAME* for the name of the program and we create a target using its value with `$(NAME)`. We define that the target depends on the variable *OBJS* and the step that must be executed is `$(CC) $(CFLAGS) -o $(NAME) $(OBJS)`.

{: .info }
> Some common targets that appear in Makefiles are **all**, **clean** and the **name of the executable**.

```makefile
NAME = bsq
SRC = main.c square_finder.c file_procs.c calculations.c std_in_procs.c
OBJS = $(SRC:.c=.o)

$(NAME): $(OBJS)
	$(CC) $(CFLAGS) -o $(NAME) $(OBJS)
```

## Usage example

In this example we define a few variables for the following purposes:

- CC: Specifies the compiler to be used.
- CFLAGS: Specifies the compiler flags to be used.
- SRC: Specifies the names of the source files to be compiled.
- OBJS: Specifies the names of the compiled objects. Takes the value of the SRC variable and changes the .c for .o.
- RM: Specifies the command that will be used to remove the compiled objects.
- NAME: Specifies the name of the executable file obtained by compiling all the source code.

We define that the default target *all* depends on the variable *NAME*. We create a target for the variable *NAME* which depends on the variable *OBJS* and the step that is executed compiles all the objects together in an executable file with the name stored in the variable *NAME*. In the variable *OBJS* we defined that the objects are obtained by compiling each source file separately. So when the `make` command is run it will compile the source code is separate objects and then it will compile all the objects in an executable file.

The target *clean* executes a command to remove the compiled objects but not the executable file. The command to run this target is `make clean`.

The target *fclean* executes a command to remove the executable file but as it depends on the target *clean* it will remove the compiled objects before. The command to run this target is `make fclean`.

```makefile
CC = gcc
CFLAGS = -Wall -Wextra -Werror
SRC = main.c square_finder.c file_procs.c calculations.c std_in_procs.c
OBJS = $(SRC:.c=.o)
RM = rm -f
NAME = bsq

all: $(NAME)

$(NAME): $(OBJS)
	$(CC) $(CFLAGS) -o $(NAME) $(OBJS)

clean:
	$(RM) $(OBJS)
	
fclean: clean
	$(RM) $(NAME)
```
