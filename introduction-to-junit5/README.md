<h1>
  <span class="headline">Writing Unit Tests in Java</span>
  <span class="subhead">Introduction to JUnit5</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be able to:
- Explain what JUnit framework is.
- Describe the structure and components of a JUnit test.

## Java frameworks
A **framework** in Java is a pre-designed, reusable set of classes that simplify development by providing pre-written code and a predefined structure, so developers can focus on implementing the logic rather than building low-level components from scratch. A framework provides the following:
- **Inversion of Control (IoC)**: The framework takes care of the program control flow. We, as developers, need not design the control flow. In other words, we need not code the `main()` method to specify the entry point, design the control flows through the code execution, and code the execution termination to mark the end of the program.
- **Reusable Components**: Ready-to-use building blocks for common tasks.

Let's suppose we want to automate the unit testing of a specific method of a class (for example, lets say `add()` method of the `Calculator` class), we would have design and code a program that does all the following:

- **Test setup**: For example, instantiating the `Calculator` class so that it's `add()` method can be accessed.
- **Test case definition**: Simulating the method call with the required input data and defining the corresponding expected results.
- **Test execution**: Comparing the actual result returned by the method call with expected result and reporting whether the test passed or failed.
- **Test teardown**: Closing the test and releasing all the resources.

In real life, a simple method like `add()` might have multiple test cases, each testing for multiple inputs as defined by the requirements. Imagine coding automated tests for hundreds of unit test cases that needs to be executed on all the units (methods) of the `Calculator` class. It might actually take more than 10 times the effort need for coding the actual `Calculator` class itself. This is where unit testing frameworks like JUnit5 come and save our day.

## The JUnit5 unit testing framework

JUnit is a popular, open-source framework for unit testing in Java. JUnit5 (also known as JUnit Jupiter) is the latest version of JUnit. JUnit5 framework provides:
- **Test Runner**: Tool that executes all the tests on the JVM, documents the test results, and provides an overall summary of the execution.
- **JUnit Annotations**:These are informational messages that are meant for the Test Runner, about how to treat the methods immediately below them during the test execution control flow. For developers, these annotations simplify test case definition, structuring, execution and documentation.
- **Assertions**: These are pre-defined methods that can validate that a test case's actual outcomes match the expected behavior. Using the appropriate assertion ensures robust and meaningful unit tests, facilitating quick debugging when test cases fail.


### Frequently used JUnit5 annotations
1. `@Test`: Marks a method as a test case.
2. `@DisplayName`: Declares a human-readable name for `@Test` methods, for documentation purposes.
3. `@BeforeAll`: Marks a method as a **high-level test setup** task. It is executed only once before the actual execution of test cases start. This method needs to be a `static` method.
4. `@BeforeEach`: Marks a method as a **testcase-level test setup** task. It is defined once but executed before each and every test case.
5. `@AfterEach`: Marks a method as a **testcase-level teardown** task. It is defined once but executed after each and every test case.
6. `@AfterAll`: Marks a method as a **high-level test teardown** task. It is executed only once after the all the test cases are. This method needs to be a `static` method.
7. `@Disabled`: Marks a test case to be skipped during execution

### Frequently used assertions
1. `assertEquals(expected, actual)`: Validates that the expected value equals the actual value.
    - Example: `assertEquals(5, calculator.add(2, 3));`
2. `assertNotEquals(expected, actual)`:  Validates that the expected and actual values are not equal.
    - Example: `assertNotEquals(4, calculator.add(2, 3));`
3. `assertTrue(condition)`: Validates that the specified condition evaluates to boolean `true`.
    - Example: `assertTrue(calculator.isPositive(5));`
4. `assertFalse(condition)`:  VAlidates that the specified condition evaluates to boolean `false`.
    - Example: `assertNotEquals(4, calculator.add(2, 3));`
5. `assertThrows(expectedException, executable)`:  Ensures that the provided executable throws the specified exception.
    - Example: `assertThrows(RuntimeException.class, () -> calculator.add("1,2,3"));`
6. `assertNull(actual)`:  Validates that the provided object is `null`.
    - Example: `assertNull(user.getMiddleName());`
7. `assertNotNull(actual)`:  Validates that the provided object is not `null`.
    - Example: `assertNotNull(user.getFirstName());`

## Anatomy of a JUnit5 test class
### 1. `Import` statements
We need to import JUnit annotations and assertion methods, before coding a JUnit5 test class. 
```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;
```


### 2. Test class declaration
The test class is a public class, ideally named after the functionality or class being tested, with a `Test` suffix. For example, if we are going to test the components (methods) of `Calculator` class, then we declare our JUnit test class as:
```java
public class CalculatorTest {
}
```

### 3. Setup and teardown methods (Optional, but recommended)
We can use `@BeforeEach` and `@AfterEach` annotations to set up and clean up resources before and after each test respectively, and `@BeforeAll` and `@AfterAll` for one-time setup or cleanup tasks.
```java
@BeforeEach
void initialize() {
    // Code to set up a common test state
}

@AfterEach
void cleanup() {
    // Code to clean up after each test
}
```

### 4. Test methods with assertions
Each test method is annotated with `@Test` and ideally focuses on a single test case. For example:
```java
@Test
void testAddition() {
    assertEquals(5, calculator.add(2, 3));
}
```

### 5. Custom configurations (Optional)
On test methods, we can use annotations like `@DisplayName` for custom human-readable test method names, or `@Tag` for grouping tests.
```java
@Test
@DisplayName("Testing subtraction functionality")
@Tag("Sprint 1 unit tests")
void testSubtraction() {
    assertEquals(2, calculator.subtract(5, 3));
}
```