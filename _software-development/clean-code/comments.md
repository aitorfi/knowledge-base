---
layout: default
title: Comments
parent: Clean Code
---

# Comments

*Extracted from the book Clean Code pages 53 - 54*

> Don't comment bad code, rewrite it.
> 
> \- Brian W. Kernighan and P. J. Plaugher

Comments are not like Schindler's List. They are not "pure good". Indeed, comments are, at best, a necessary evil. If our programming languages were expressive enough, or if we had the talent to subtly wield those languages to express our intent, we would not need comments very much, perhaps not at all.

The proper use of comments is to compensate for our failure to express ourself in code. Note that I used the word *failure*. I meant it. Comments are always failures, We must have them because we cannot always figure out how to express ourselves without them, but their use is not a cause for celebration.

## Don't Use Comments When You Can Use a Function or a Variable

*Extracted from the book Clean Code page 67*

Consider the following stretch of code:
```java
// does the module from the global list <moddepend on the
// subsystem we are part of?
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
```
This could be rephrased without the comments as
```java
ArrayList moduleDependees = smodule.getDependSubsystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```

## Mandated Comments

*Extracted from the book Clean Code page 64*

It is just plain silly to have a rule that says that every function must have a javadoc, or every variable must have a comment. Comments like this just cutter up the code, propagate lies, and lend to general confusion and disorganization.

Example of redundant javadoc due to mandatory comments:
```java
/**
 *
 * @param title The title of the CD
 * @param author The author of the CD
 * @param tracks The number of tracks on the CD
 * @param durationInMinutes The duration of the CD in minutes
 */
public void addCD(String title, String author, 
				  int tracks, int durationInMinutes) {
    CD cd = new CD();
    cd.title = title;
    cd.author = author;
    cd.tracks = tracks;
    cd.duration = duration;
    cdList.add(cd);
 }
```

## Noise Comments

*Extracted from the book Clean Code page 64 - 65*

Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.

These comments are so noisy that we learn to ignore them. As we read through code, our eyes simply skip over them. Eventually the comments begin to lie as the code around them changes.

Example of noisy comments:
```java
/**
 * Default constructor
 */
protected AnnualDateRule() { }

/** The day of the month **/
private int dayOfMonth;

/**
 * Returns the day of the month.
 * 
 * @return the day of the month.
 */
public int getDayOfMonth() {
    return dayOfMonth;
}
```

## Javadoc in Nonpublic Code

*Extracted from the book Clean Code page 71*

As useful as javadocs are for public APIs, they are anathema to code that is not intended for public consumption. Generating javadoc pages for the classes and functions inside a system is not generally useful, and the extra formality of the javadoc comments amount to little more than cruft and distraction.
