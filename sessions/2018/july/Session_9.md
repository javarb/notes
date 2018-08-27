# SOFTWARE ENGINEERING IN JAVA

## Session 9 (07/08/2018)

- TDD

### Notes:

**TDD Introduction**

An example of TDD was made for some single cases:

We created a class called `PracticeTest.java`
```java
package co.org.osso.tdd;
// Unit, component and integration Test framework (terms can vary)

import org.junit.Assert;
import org.junit.Test;

// unit tests (test only a single class)
// component tests (multiple clases but not io or databases, very fast) - a common patter is to test a package
// integration tests (classes and databases)
// System tests (a separate project test our project)
// Acceptance tests (A guided test for manual tests, can be automated) -slow
public class PracticeTest {

    // Convention for tests is to call this field object target in order not depend of the class name
    // or "mut" module under test? - not recommended target is more common
    Practice target = new Practice();
    // hast to be defined so
    /*  @Test
        - public
        - void
        - no args
    * */
    @Test
    public void a() {
        //Assert.assertEquals(1,2);
        Assert.assertEquals(2, target.returnTwo());

    }

    @Test
    public void greetsMeProperly() {

        String expected = "Hello, Javier!";
        String actual = target.greet("Javier");
        Assert.assertEquals(expected, actual);

    }

    @Test
    public void greetRogerProperly() {

        String expected = "Hello, Roger!";
        String actual = target.greet("Roger");
        Assert.assertEquals(expected, actual);

    }

}
```



**TDD**

A discipline that we have to stick to, following these laws. So w will end with good code. 

3 steps:
- Red
- Green
- Refactor

Ah do you mean I program in order to provoke crashes so I can fix them before thy occurs in the reality

Red
Write as little code as posible for make a failing test. Has to be relevant to the test that we're doing. A compilation error is a valid case.

Green
Write as little production code as possible to make all the tests we wrote in unit to pass.

Refactor
Cleaning up our code. This allows to have maintenable code (not a entangle) 

We want to program naturally green code all time, but we will end with better code and cleaner when we begin with Red, Green, Refactor

In practice each step can take 2 minutes.

folowing these rules try to solve this challenge

https://github.com/rob-lowcock/gophercon-2018

finally is needed the number of houses visited 1 time
but why up down up down are 2 houses?

TDD approach to solve it 

Use one of these cases to build using TDD https://github.com/rob-lowcock/gophercon-2018/blob/master/main_test.go
