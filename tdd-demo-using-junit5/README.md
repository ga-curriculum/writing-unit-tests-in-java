<h1>
  <span class="headline">Writing Unit Tests in Java</span>
  <span class="subhead">TDD Demo using JUnit5</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be able to apply test-driven-development approach using JUnit5 framework and developing a unit of java application code (method).

## Calculator app: Reqirement No. 1
Develop the `divide()` method for a `Calculator` app with the following behavior:
1. Computes and returns the quotient when the divident and divisor are passed as arguments.
2. Throws an `ArithmeticException` if the `divisor` passed is `0`.

## TDD's Red phase
In TDD, we do not code the functionality first. Instead, we create the tests from the requirements. In an agile project, a java developer who's going to code the functionality sits with the requirement owner and writes these tests. 
Hence, at the end of this phase we need to have JUnit5 tests in our `CalculatorTest` class that would fail to demonstrate that our `Calculator` class does not have _Requirement No. 1_ implemented yet.

Our `CalculatorTest` class must contain:
1. Required `import` statements to load JUnit5 annotations and assertions that we need.
2. `CalculatorTest` class declaration
3. Setup and Teardown steps, if any, using appropriate JUnit5 annotations
4. Test cases that use JUnit5 appropriate assertion methods that test normal scenarios, edge-case scenarios and error scenarios for validating `divide()` method's behavior
5. Custom configurations, if needed, using JUnit5 annotations to make our test class understandable and maintainable.

<details>
<summary><b>Expand to view the implementation:</b></summary>
<pre>
<code>
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

@DisplayName("Calculator Tests for Integer Divide Functionality")
class CalculatorTest {

    private Calculator calculator;

    @BeforeEach
    void setUp() {
        calculator = new Calculator(); // Initialize calculator before each test
    }

    @Test
    @DisplayName("Dividing two positive integers yields a positive quotient")
    void testDivideTwoPositiveIntegers() {
        assertEquals(2, calculator.divide(10, 5));
    }

    @Test
    @DisplayName("Dividing a positive integer by a negative integer yields a negative quotient")
    void testDividePositiveByNegativeInteger() {
        assertEquals(-3, calculator.divide(9, -3));
    }

    @Test
    @DisplayName("Dividing two negative integers yields a positive quotient")
    void testDivideTwoNegativeIntegers() {
        assertEquals(4, calculator.divide(-16, -4));
    }

    @Test
    @DisplayName("Dividing zero by an integer yields zero")
    void testDivideZeroByInteger() {
        assertEquals(0, calculator.divide(0, 5));
    }

    @Test
    @DisplayName("Dividing any integer by zero throws ArithmeticException")
    void testDivisionByZeroThrowsException() {
        assertThrows(ArithmeticException.class, 
            () -> calculator.divide(10, 0));
    }
}
</code>
</pre>
</details>

####

After writing the tests we run them by right-clicking on the project folder in our IntelliJ IDEA project navigator pane and selecting **Run 'All Tests'** option. This will make IntelliJ's test runner run all our JUnit Tests, format the results, and display it in the **Run** pane.

## TDD's Green phase
In this phase, our objective is to implement the minimum code for `divide()` method in our `Calculator` class so that all the tests in our `CalculatorTest` pass.

If some tests fail during our test run, we keep making only the necessary changes to the source code until all the tests pass.

<details>
<summary><b>Expand to view the implementation:</b></summary>
<pre>
<code>
 class Calculator {

        public int divide(int a, int b) {
            if (b == 0) {
                throw new ArithmeticException();
            }
            return a / b;
        }
    }
</code>
</pre>
</details>

## TDD's Refactor phase
Refactoring is the process of improving the quality of our code while ensuring all tests still pass. Here's a non-exhaustive list of activities we do during refactoring:

- Renaming methods, classes, or variables to give them more descriptive and meaningful names.
- Breaking long or complex method into smaller, self-contained methods that adhere to the _Single Responsibility Principle (Each class or method in a program should have a single responsibility or function)_
- Adding human-readable descriptions to programmatic messages, and adding comments to make the code more readable
- Any other Java best practices

<details>
<summary><b>Expand to view the implementation:</b></summary>
<pre>
<code>
/**
 * A simple calculator class for basic arithmetic operations using integers.
 */
class Calculator {

    /**
     * Divides one integer by another.
     * @throws ArithmeticException if the divisor is zero.
     */
    public int divide(int divident, int divisor) {
        validateDivisor(divisor);
        return divident / divisor;
    }

    /**
     * Validates the divisor to ensure it is not zero.
     * @throws ArithmeticException if the divisor is zero.
     */
    private void validateDivisor(int divisor) {
        if (divisor == 0) {
            throw new ArithmeticException("Division by zero is not allowed.");
        }
    }
}

</code>
</pre>
</details>

## Conclusion
In a real agile project, the next requirement may be:
- **Modification**: Implementing the `divide()` function accepts and returns decimal (`float`) values too.
- **New implementation**: Adding `multiply()` function to `Calculator`

When using TDD, each and every requirement implementation goes through the same **Red-Green-Refactor** cycle. TDD is an **extreme programming** approach that ensures that:
- Application development is rapid.
- No matter when the sprint stops, there is always tested and working code available to be deployed.
- Automated unit tests are available for any future application updates.