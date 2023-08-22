---
layout: default
title: Unit Tests
parent: Clean Code
---

# Unit Tests

Robert C. Martin
{: .label .label-green }

Book Notes
{: .label .label-yellow }

Best Practices
{: .label .label-yellow }

## The Three Laws of TDD

*Extracted from the book Clean Code pages 122 - 123*

By now everyone knows that TDD asks us to write unit tests first, before we write production code. But that rule is just the tip of the iceberg. Consider the following three laws:

**First Law:** You may not write production code until you have written a failing unit test.

**Second Law:** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.

**Third Law:** You may not write more production code than is sufficient to pass the currently failing test.

These three laws lock you in a cycle that is perhaps thirty seconds long. The tests and the production code are written *together*, with the tests just a few seconds ahead of the production code.

If we work this way, we will write dozens of tests every day, hundreds of tests every month, and thousands of tests every year. If we work this way, those tests will cover virtually all of our production code.

## Domain-Specific Testing Language

*Extracted from the book Clean Code page 127*

Rather than using the APIs that programmers use to manipulate the system, we build up a set of functions and utilities that make use of those APIs and that make the tests more convenient to write and easier to read. These functions and utilities become a specialized API used by the tests. They are a testing *language* that programmers use to help themselves to write their tests and to help those who must read those tests later on.

This testing API is not designed up front; rather it evolves from continued refactoring of test code that has gotten too tainted by obfuscating detail.

In the following example we can see a unit test that makes use of functions defined to make tests easier to read and write:

```java
public void testGetPageHierarchyAsXML() thows Exception {
    makePages("Page One", "PageOne.ChildOne", "PageTwo");

    submitRequest("root", "type:pages");

    assertResponseIsXML();
    assertResponseContains(
        "<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>"
    );
}
```

## F.I.R.T.S.

*Extracted from the book Clean Code pages 132 - 133*

Clean tests follow five other rules that form the above acronym:

**Fast:** Tests should be fast. They should run quickly. When tests run slow, you won't want to run them frequently. If you don't run them frequently, you won't find problems early enough to fix them easily. You won't feel as free to clean up the code. Eventually the code will begin to rot.

**Independent:** Tests should not depend on each other. One test should not set up the conditions for the nest test. You should be able to run each test independently and run the tests in any order you like. When tests depend on each other, then the first one to fail causes a cascade of downstream failures, making diagnosis difficult and hiding downstream defects.

**Repeatable:** Tests should be repeatable in any environment, You should be able to run the tests in a production environment, in the QA environment, and on your laptop while riding home on the train without a network. If your tests aren't repeatable in any environment, then you'll always have an excuse for why they fail. You'll also find yourself unable to run the tests when the environment isn't available.

**Self-Validating:** The tests should have a boolean output. Either they pass or fail. You should not have to read through a log file to tell whether the tests pass. You should not have to manually compare two different text files to see whether the test pass. If the tests aren't self-validating, then failure can become subjective and running the tests can require a long manual evaluation.

**Timely:** The test need to be written in a timely fashion. Unit test should be written *just before* the production code that makes them pass. If you write tests after the production code, then you may find the production code to be hard to test. You may decide that some production code is too hard to test. You may not design the production code to be testable.
