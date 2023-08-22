---
layout: default
title: Error Handling
parent: Clean Code
---

# Error Handling

Robert C. Martin
{: .label .label-green }

Book Notes
{: .label .label-yellow }

Best Practices
{: .label .label-yellow }

## Use Exceptions Rather Than Return Codes

*Extracted from the book Clean Code page 104*

Back in the distant past there were many languages that didn't have exceptions. In those languages the techniques for handling and reposting errors were limited. You eighter set an error flag or return an error code that the caller could check.

The problem with these approaches is that they clutter the caller. The caller must check for errors immediately after the call. Unfortunately, it's easy to forget. For this reason it is better to throw an exception when you encounter an error. The calling code is cleaner. Its logic is not obscured by error handling.

## Use Unchecked Exceptions

*Extracted from the book Clean Code page 107*

Checked exceptions allow Java programmers to define a list of exceptions a method could pass to its caller in the method signature. This seems like a good idea but there is a price to pay.

```java
public void singIn(String username, String password) thows InvalidCredentialsException;
```

The price of checked exceptions is an `Open/Close Principle` violation. If you throw a checked exception form a method in your code and the `catch` is three levels above, you must declare that exception in the signature of each method between you and the `catch`. This means that a change at a low level of the software can force signature changes on many higher levels. The changed modules must be rebuilt and redeployed, event though nothing they care about changed.

Consider the calling hierarchy of a large system. Functions at the top call functions bellow them, which call more functions bellow them, ad infinitum. Now let's say one of the lowest level functions is modified in such a way that it must throw an exception. if that exception is checked, then the function signature must add a `throws` clause. But this means that every function that calls our modified function must also be modified eighter to catch the new exception or to append the appropriate `throws` clause to its signature. Ad infinitum. The net result in a cascade of changes that work their way from the lowest levels of the software to the highest! Encapsulation is broken because all functions in the path of a throw must know about details of that low-level exception. Given that purpose of exceptions is to allow you to handle errors at a distance, it is a shame that checked exceptions break encapsulation in this way.

Checked exceptions can sometimes be useful if you are writing a critical library: You must catch them. But in general application development the dependency cost overweight the benefits.

## Define Exception Classes in Terms of a Caller Needs

*Extracted from the book Clean Code page 107 - 109*

Let's look at an example of a poor exception classification. Here is a `try-catch-finally` statement for a third party library call. It covers all of the exceptions that the calls can throw:

```java
ACMEPort port = new ACMEPort(12);

try {
    port.open();
} catch (DeviceResponseException e) {
    reportPortError(r);
    logger.log("Device response exception", e);
} catch (ATM1212UnlockedException e) {
    reportPortError(r);
    logger.log("Unlock exception", e);
} catch (GMXError e) {
    reportPortError(r);
    logger.log("Device response exception", e);
} finally {
    ...
}
```

That statement contains a lot of duplication, and we shouldn't be surprised. In most exception handling situations, the work that we do is relatively standard regardless of the actual cause. We have to record an error and make sure that we can proceed.

In this case, because we know that the work that we are doing is roughly the same regardless of the exception, we can simplify our code considerably by wrapping the API that we are calling and making sure that it returns a common exception type:

```java
LocalPort port = new LocalPort(12);

try {
    port.open();
} catch (PortDeviceFailure e) {
    reportError(e);
    logger.log(e.getMessage(), e);
} finally {
    ...
}
```

Our `LocalPort` class is just a simple wrapper that catches and translates exceptions throw by the `ACMEPort` class:

```java
public class LocalPort {
    private ACMEPort innerPort;

    public LocalPort(int portNumber) {
        innerPort = new ACMEPort(portNumber);
    }

    public void open() {
        try {
            innerPort.open();
        } catch (DeviceResponseException e) {
            throw new PortDeviceFailure(e);
        } catch (ATM1212UnlockedException e) {
            throw new PortDeviceFailure(e);
        } catch (GMXError e) {
            throw new PortDeviceFailure(e);
        }
    }
}
```

Wrappers like the one we defined for `ACMEPort` can be very useful. In fact, wrapping third-party APIs is a best practice. When you wrap a third-party API, you minimize your dependencies upon it: You can choose to move to a different library in the future without much penalty. Wrapping also makes it easier to mock out third-party calls when you are testing your own code.

One final advantage of wrapping is that you aren't tied to a particular vendor's API design choices. You can define an API that you feel comfortable with. In the preceding example, we defined a single exception type for port device failure and found that we could write much cleaner code.

Often a single exception class is fine for a particular area of code. The information sent with the exception can distinguish the errors. Use different classes only if there are times when you want to catch one exception and allow the other one to pass.

## Define the Normal Flow

*Extracted from the book Clean Code page 109 - 110*

There are times when you need to use exceptions but don't want to abort. Let's take a look at an example. Here is some code that sums expenses in a billing application:

```java
try {
    MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
    m_total += expenses.getTotal();
} catch (MealExpensesNotFound e) {
    m_total += getMealPerDiem();
}
```

In this business, if meals are expensed, they become part of the total. If they aren't, the employee gets a meal *per diem* amount for that day. The exception clutters the logic. Wouldn't it be better if we didn't have to deal with the special case? If we didn't, our code would look much simpler. It would look like this:

```java
MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
m_total += expenses.getTotal();
```

Can we make the code that simple? It turns out that we can. We can change `ExpenseReportDAO` so that it always returns a `MealExpense` object. If there are no meal expenses, it returns a `MealExpense` object that returns *per diem* as its amount:

```java
public class PerDiemMeal implements MealExpense {
    public int getTotal() {
        // return the per diem default.
    }
}
```

This is called the `SPECIAL CASE PATTERN`. You create a class or configure an object so that it handles a special case for you. When you do, the client code doesn't have to deal with exceptional behavior. That behavior is encapsulated in the special case object.
