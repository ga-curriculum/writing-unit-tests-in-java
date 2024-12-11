<h1>
  <span class="headline">Writing Unit Tests in Java</span>
  <span class="subhead">Requirement One</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to tktk.

#### Requirement 1: The method can take 0, 1 or 2 numbers separated by comma (,).

Let’s write our first set of tests.

```java
package com.example.demo;

import org.junit.Assert;
import org.junit.Before;
import org.junit.Test;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;

public class CalculatorTest {

    Calculator calculator;

    @BeforeEach
    public void setUp() {
        calculator = new Calculator();
    }

    @Test(expected = RuntimeException.class)
    @DisplayName("When more than 2 numbers are used then exception is thrown")
    public final void whenMoreThan2NumbersAreUsedThenExceptionIsThrown() {
        calculator.add("1,2,3");
    }

    @Test
    @DisplayName("when 2 numbers are used then no exception is thrown")
    public final void when2NumbersAreUsedThenNoExceptionIsThrown() {
        calculator.add("1,2");
        Assert.assertTrue(true);
    }

    @Test(expected = RuntimeException.class)
    @DisplayName("when non number is used then exception is thrown")
    public final void whenNonNumberIsUsedThenExceptionIsThrown() {
        calculator.add("1,X");
    }
}
```

**Note**
Here you can see I'm importing `@BeforeEach` and `@DisplayName` annotation, and it is not part of `JUnit4`. You can
install dependency by mouse hovering line 5, and click on Add `JUnit5.x.x` to classpath when dialog box appears.

![img.png](./assets/6-import-junit-5.png)

Keep in mind that the idea behind TDD is to do the necessary minimum to make the tests pass and repeat the process until
the whole functionality is implemented. In this case the name of one of the test methods
is `whenMoreThan2NumbersAreUsedThenExceptionIsThrown`. Our first set of tests verifies that up to two numbers can be
passed to the calculator's add method. If there's more than two or if one of them is not a number, exception should be
thrown. Putting `expected` inside the `@Test` annotation tells the JUnit runner that the expected outcome is to throw
the specified exception.

- The method annotated with `@BeforeEach` runs before each test
- A method annotated with `@Test` defines a test method
- `@DisplayName` can be used to define the name of the test which is displayed to the user
- This is an assert statement which validates that expected and actual value is the same, if not the message at the end
  of the method is shown

```java
public class Calculator {
    public static void add(final String numbers) {
        String[] numbersArray = numbers.split(",");
        if (numbersArray.length > 2) {
            throw new RuntimeException("Up to 2 numbers separated by comma (,) are allowed");
        } else {
            for (String number : numbersArray) {
                Integer.parseInt(number); // If it is not a number, parseInt will throw an exception
            }
        }
    }
}
```