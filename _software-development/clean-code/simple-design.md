---
layout: default
title: Simple Design
parent: Clean Code
---

# Kent Beck's Simple Design Rules

Robert C. Martin
{: .label .label-green }

Kent Beck
{: .label .label-green }

Book Notes
{: .label .label-yellow }

Best Practices
{: .label .label-yellow }

*Extracted from the book Clean Code pages 172 - 176*

According to Kent, a design is "simple" if it follows these rules:
1. Runs all the tests.
2. Contains no duplication.
3. Expresses the intent of the programmer.
4. Minimizes the number of classes and methods.

## Simple Design Rule 1: Runs All the Tests

*Extracted from the book Clean Code page 173*

Fist and foremost, a design must produce a system that acts as intended. A system might have a perfect design on paper, but if there is no simple way to verify that the system actually works as intended, then all the paper effort is questionable.

A system that is comprehensively tested and passes all of its test all of the time is a testable system, That's an obvious statement, but an important one. Systems that aren't testable aren't verifiable. Arguably, a system that cannot be verified should never be deployed.

Fortunately, making our system testable pushes us towards a deign where our classes are small and single purpose. It's just easier to test classes that conform to the *Single Purpose Principle (SRP)*. The more tests we write, the more we'll continue to push toward things that are simple to test. So making sure our system is fully testable helps us create better designs.

Tight coupling makes it difficult to write tests. So, similarly, the more tests we write, the more we use principles like *Dependency Inversion Principle (DIP)* and tools like dependency injection, interfaces, and abstraction to minimize coupling. Our designs improve even more.

Once we have tests, we are empowered to keep our code and classes clean. We do this by incrementally refactoring the code. For each few lines of code we add, we pause and reflect on the new design. Did we just degrade it? I do, we clean it up and run our tests to demonstrate that we haven't broken anything. The fact that we have tests eliminates the fear that cleaning up the code will break it!

## Simple Design Rule 2: No Duplication

*Extracted from the book Clean Code pages 173 - 174*

Duplication is the primary enemy of a well-design system. It represents additional work, additional risk, and additional unnecessary complexity. Duplication manifests itself in many forms. Lines of code that look exactly alike are, of course, duplication. Lines of code that are similar can often be massaged to look even more alike so that they can be more easily refactored. And duplication can exist in other forms such as duplication of implementation. For example, we might have two methods in a collection class:

```java
int size() {...}
boolean isEmpty() {...}
```

We could have separate implementations  for each method. The `isEmpty` method could track a boolean, while `size` could track a counter. Or, we can eliminate the duplication by tying `isEmpty` to the definition of `size`:

```java
boolean isEmpty() {
    return size() == 0;
}
```

Creating a clean system requires the will to eliminate duplication, event in just a few lines of code. For example, consider the following code:

```java
public void scaleToOneDimension(float desiredDimension, float imageDimension) {
    if (Math.abs(desiredDimension - imageDimension) < errorThreshold)
	    return;

    float scalingFactor = desiredDimension / imageDimension;
    scalingFactor = (float) (Math.floor(scalingFactor * 100) * 0.01f);

    RenderOp newImage = ImgeUtilities.getScaledImge(
        image, scalingFactor, scalingFactor);

    image.dispose();
    System.gc();
    image = newImage;
}

public synchronized void rotate(int degrees) {
    RenderOp newImage = ImgeUtilities.getRotatedImge(image, degrees);
    
    image.dispose();
    System.gc();
    image = newImage;
}
```

To keep this system clean, we should eliminate the small amount of duplication between the `scaleToOneDimension` and `rotate` methods:

```java
public void scaleToOneDimension(float desiredDimension, float imageDimension) {
    if (Math.abs(desiredDimension - imageDimension) < errorThreshold)
	    return;

    float scalingFactor = desiredDimension / imageDimension;
    scalingFactor = (float) (Math.floor(scalingFactor * 100) * 0.01f);

    replaceImage(ImgeUtilities.getScaledImge(
        image, scalingFactor, scalingFactor));
}

public synchronized void rotate(int degrees) {
    replaceImage(ImgeUtilities.getRotatedImge(image, degrees));
}

public void replaceImge(RenderOp newImage) {
    image.dispose();
    System.gc();
    image = newImage;
}
```

As we extract commonality at this very tiny level, we start to recognize violations of *Single Purpose Principle (SRP)*. So we might move a newly extracted method to another class. That elevates its visibility. Someone else on the team may recognize the opportunity to further abstract the new method and reuse it in a different context. This "reuse in the small" can cause system complexity to shrink dramatically.

The *Template Method* patter is a common technique for removing higher-level duplication. For example:

```java
public class VacationPolicy {
    public void accruelUSDivisionVacation() {
        // code to calculate vacation based on hours worked to date
        // ...
        // code to ensure vacation meets US minimums
        // ...
        // code to apply vacation to payroll record
        // ...
    }
    
    public void accruelEUDivisionVacation() {
        // code to calculate vacation based on hours worked to date
        // ...
        // code to ensure vacation meets EU minimums
        // ...
        // code to apply vacation to payroll record
        // ...
    }
}
```

The code across `accruelUSDivisionVacation` and `accruelEUDivisionVacation` is largely the same, with the exception of calculating legal minimums. That bit of algorithm changes based on the employee type. We can eliminate the obvious duplication by applying the *Template Method* patter.

```java
abstract public class VacationPolicy {
    public void accruelVacation() {
        calculateBaseVacationHours();
        alterForLegalMinimums();
        applyToPayroll();
    }

    private void calculateBaseVacationHours () {...}
    abstract protected void alterForLegalMinimums () {...}
    private void applyToPayroll () {...}
}

public class USVacationPolicy extends VacationPolicy {
    @Override
    protected void alterForLegalMinimums() {
        // US specific logic
    }
}

public class EUVacationPolicy extends VacationPolicy {
    @Override
    protected void alterForLegalMinimums() {
        // EU specific logic
    }
}
```

The subclasses fill the "hole" in the `accruelVacation` algorithm, supplying the only bits of information that are not duplicated.

## Simple Design Rule 3: Expressive

*Extracted from the book Clean Code page 175*

@see [Meaningful Names](../meaningful-names)

The majority of the cost of a software project is in long-term maintenance. In order to minimize the potential for defects as we introduce change, it's critical for us to be able to understand what the system does. As systems become more complex, they take more and more time for a developer to understand, and there is an ever greater opportunity for a misunderstanding. Therefore, code should clearly express the intent of its author. The clearer the author can make the code, the less time other will have to spend understanding it. This will reduce defects and shrink the cost of maintenance.

You can express yourself by choosing good names. We want to be able to hear a class or function name and not be surprised when we discover its responsibilities.

You can also express yourself by keeping your functions and classes small. Small classes and function are usually easy to name, easy to write, and easy to understand.

Well-written unit tests are also expressive. A primary goal of test is to act as documentation by example. Someone reading our tests should be able to get a quick understanding of what a class is all about.

## Simple Design Rule 4: Minimal Classes and Methods

*Extracted from the book Clean Code page 176*

Even concepts as fundamental as elimination of duplication, code expressiveness, and the *Single Responsibility Principle (SRP)* can be taken too far. In an effort to make our classes and methods small, we might create too many tiny classes and methods. So this rule suggests that we also keep our function and class counts low.

High class and method counts are sometimes the result of pointless dogmatism. Consider, for example, a coding standard that insists on creating an interface for each and every class. Or consider developers who insist that fields and behavior must always be separated into data classes and behavior classes, Such dogma should be resisted and a more pragmatic approach adopted.

Our goal is to keep our overall system small while we are also keeping our functions and classes small. Remember, however, that this rule is the lowest priority of the four rules of Simple Design. So, although it's important to keep class and function counts low, it's more important to have tests, eliminate duplication, and express yourself.
