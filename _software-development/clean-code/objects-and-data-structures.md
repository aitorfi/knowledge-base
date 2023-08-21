---
layout: default
title: Objects and Data Structures
parent: Clean Code
---

# Objects and Data Structures

## Data/Object Anti-Symmetry

*Extracted from the book Clean Code page 95*

Objects hide their data behind abstraction and expose functions that operate on that data. Data structures expose their data and have no meaningful functions.

### Example 1

*Extracted from the book Clean Code pages 94 - 95*

Consider the following two examples. The first uses concrete terms to communicate the fuel level of a vehicle, whereas the second does so with the abstraction of percentage. In the concrete case you can be pretty sure that these are just accessors of variables. In the abstract case you have no clue at all about the form of the data.

```java
public interface Vehicle {
    double getFuelTankCapacityInGallons();
    double getGallonsOfGasoline();
}
```

```java
public interface Vehicle {
    double getPercentFuelRemainig();
}
```

The first example is a data structure that exposes data so that you can manually operate with it, the second however is an object that hides its data and exposes a function that operates with it.

### Example 2

*Extracted from the book Clean Code pages 95 - 97*

Consider the following procedural shape example. The `Geometry` class operates on the three shape classes. The shape classes are simple data structures without any behavior. All the behavior is in the `Geometry` class.

```java
public class Square {
    public Point topLeft;
    public double side;
}

public class Rectangle {
    public Point topLeft;
    public double height;
    public double width;
}

public class Circle {
    public Point center;
    public double radius;
}

public class Geometry {
    public final double PI = 3.1415926535;

    public double area(Object shape) throws NoSuchShapeException {
        if (shape instanceof Square) {
            Square s = (Square) shape;
            return s.side * s.side;
        }
        else if (shape instanceof Rectangle) {
            Rectangle r = (Rectangle) shape;
            return r.height * r.width;
        }
        else if (shape instanceof Circle) {
            Circle c = (Circle) shape;
            return PI * c.radius * c.radius;
        }

        throw new NoSuchShapeException();
    }
}
```

Consider what would happen if a `perimeter()` function were added to `Geometry`. The shape classes would be unaffected. Any other classes that depend upon the shapes would also be unaffected. On the other hand, if I add a new shape, I must change all the functions in `Geometry` to deal with it.

Now consider the following object-oriented solution. Here the `area()` method is polymorphic. No `Geometry` class is necessary. So if I add a new shape, none of the existing functions are affected, but if I add a new functions all of the `shapes` must be changed.

```java
public interface Shape {
    double area();
}

public class Square implements Shape {
    private Point topLeft;
    private double side;

    public double area() {
        return side * side;
    }
}

public class Rectangle implements Shape {
    private Point topLeft;
    private double height;
    private double width;

    public double area() {
        return height * width;
    }
}

public class Circle implements Shape {
    private Point center;
    private double radius;
    public final double PI = 3.1415926535;

    public double area() {
        return PI * radius * radius;
    }
}
```

## The Law of Demeter

*Extracted from the book Clean Code pages 97 - 98*

The is a well known heuristic called `Law of Demeter` that says a module should not know about the innards of the objects it manipulated. As we saw in the last section, objects hide their data and expose operations. This means that an object should not expose its internal structure through accessors because to do so is to expose, rather than to hide, its internal structure.

More precisely, the Law of Demeter says that a method `f` of a class `C` should only call the methods of these:
	- `C`
	- An object created by `f`
	- An object passed as an argument to `f`
	- An object held in an instance variable of `C`

The method should not invoke methods on objects that are returned by any of the allowed functions. In other words, talk to friends, not strangers.

The following code appears to violate the Law of Demeter because it calls the `getScratchDir()` function on the return value of `getOptions()` and then calls `getAbsolutePath()` on the return value of `getScratchDir()`.

```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

If `ctxt` is an object we should be telling it to do something we should not be asking it about its internals, So why did we want the absolute path of the scratch directory? What were we going to do wit it? What if we told `ctxt` object to do it?

```java
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```

That seems like a reasonable thing for an object to do. This allows `ctxt` to hide its internals and prevent the current function from having to violate the Law of Demeter by navigating though objects it shouldn't know about.

## Hybrids

*Extracted from the book Clean Code page 99*

Data structures should have public variables and no functions, whereas objects should have private variables and public functions. However there are frameworks and standards (e.g. java beans) that demand that even simple data structures have accessors and mutators.

This confusion sometimes leads to unfortunate hybrid structures that are half objects and half data structures. They have functions that do significant things, and they also have either public variables or public accessors and mutators that, for all intents and purposes, make the private variables public, tempting other external functions to use those variables the way a procedural program would use a data structure.

Such hybrids make it hard to add new functions but also make it hard to add new data structures. They are the worst of all both worlds. Avoid creating them.
