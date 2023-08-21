---
layout: default
title: Functions
parent: Clean Code
---

# Functions

@see [Meaningful Names](../meaningful-names)

## Blocks and Indenting

*Extracted from the book Clean Code page 35*

The blocks within `if` statements, `else` statements, `while` statements, and so on should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small, but it also adds documentary value because the function called within the block can have a nicely descriptive name.

This also implies that function should not be large enough to hold nested structures. Therefore, the indent level of a function should not be greater than one or two. This, of course, makes the functions easier to read and understand.

## One Level of Abstraction per Function

*Extracted from the book Clean Code page 36*

In order to make sure our functions are doing "one thing", we need to make sure that the statements within our function are all at the same level of abstraction.
...
Mixing levels of abstraction within a function is always confusing. Readers may not be able to tell whether a particular expression is an essential concept or a detail.

## Use Descriptive Names

*Extracted from the book Clean Code page 39*

Don't be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment.

## Function Arguments

*Extracted from the book Clean Code page 40*

The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification and then shouldn't be used anyway.

Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. If there are no arguments this is trivial. If there's one argument, it's not too hard. With two arguments the problem gets a bit more challenging. With more than two arguments, testing every combination of appropriate values can be daunting.

### Common Monadic Forms

*Extracted from the book Clean Code page 41*

There are two very common reasons to pass a single argument into a function. You may be asking a question about that argument, as in `boolean fileExists("MyFile")`. Or you may be operating on that argument, transforming it into something else and *returning it*. For example, `InputStream fileOpen("MyFile")` transforms a file name `String` into an `InputStream` return value. These two uses are what readers expect when they see a function.

A somewhat less common, but still very useful form of a single argument function, is an *event*. In this form there is an input argument but no output argument. The overall program is meant to interpret the function call as an event and use the argument to alter the state of the system, for example, `void passwordAttemptFailedNTimes(int attempts)`. Use this form with care. It should be very clear to the reader that this is an event.

### Flag Arguments

*Extracted from the book Clean Code page 41*

**Flag arguments should be avoided** as they are a clear indicator that a function does more than one thing.

Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice. It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing, It does one thing if the flag is true and another if the flag is false!

### Argument Objects

*Extracted from the book Clean Code page 43*

Related function arguments can be encapsulated in objects to reduce the number of arguments.

When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own. Consider, for example, the difference between the two following declarations:

```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

Reducing the number of arguments by creating objects out of them may seem like cheating, but it's not. When groups of variables are passed together, the way x and y are in the example above, they are likely part of a concept that deserves a name of its own.

## Prefer Exceptions to Returning Error Codes

*Extracted from the book Clean Code page 46*

...When you return an error code, you create the problem that the caller must deal with the error immediately.

On the other hand, if you use exceptions instead of returned error codes, then the error processing code can be separated from the happy path code and can be simplified:

```java
if (deletePage(page) == E_OK) {
	if (registry.deleteReference(page.name) == E_OK) {
		if (configKey.deleteKey(page.name.makeKey()) == E_OK) {
			logger.log("page deleted");
		} else {
			logger.log("configKey not deleted");
		}
	} else {
		logger.log("deleteReference from registry failed");
	}
} else {
	logger.log("delete failed");
	return E_ERROR;
}
```

```java
try {
	deletePage(page);
	registry.deleteReference(page.name);
	configKey.deleteKey(page.name.makeKey());
} catch (Exception e) {
	logger.log(e.message());
}
```

### Extract Try/Catch Blocks

*Extracted from the book Clean Code page 46*

`Try/Catch` blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So it is better to extract the bodies of the `try` and `catch` blocks out into functions of their own.

```java
public void delete(Page page) {
    try {
        deletePageAndAllReferences(page);
    } catch (Exception e) {
        logError(e);
    }
}

private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage();
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
}

private vopid logError(Exception e) {
    logger.log(e.getMessage());
}
```

### Structured Programming

*Extracted from the book Clean Code page 47*

Some programmers follow Edsger Dijkstra's rules of structured programming. Dijkstra said that every function, and every block within a function, should have one entry and one exit. Following these rules means that there should only be one `return` statement in a function, no `break` or `continue` statements in a loop, and never, *ever*, any `goto` statements.

While we are sympathetic to the goal and disciplines of structured programming, those rules serve little benefit when functions are very small. It is only in larger functions that such rules provide significant benefit.

So if you keep your functions small, then the occasional multiple `return`, `break`, or `continue` statement does no harm and can sometimes even be more expressive than the single-entry, single-exit rule. On the other hand `goto` only makes sense in large functions, so it should be avoided.
