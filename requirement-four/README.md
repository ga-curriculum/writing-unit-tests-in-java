<h1>
  <span class="headline">Writing Unit Tests in Java</span>
  <span class="subhead">Requirement Four</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to tktk.

#### You do: Requirement 4: Allow the Add method to handle an unknown amount of numbers (15 min)

- Create `whenAnyNumberOfNumbersIsUsedThenReturnValuesAreTheirSums` method in `CalculatorTest.java`
- Use `Assert.assertEquals(3+6+15+18+46+33, StringCalculator.add("3,6,15,18,46,33"))` to evaluate **modified** add
  method
- Don't forget to comment `whenMoreThan2NumbersAreUsedThenExceptionIsThrown` when testing
  <details>
  <summary>CalculatorTest.java solution</summary>

    ```java 
      //    @Test(expected = RuntimeException.class)
      //    @DisplayName("When more than 2 numbers are used then exception is thrown")
      //    public final void whenMoreThan2NumbersAreUsedThenExceptionIsThrown() {
      //        Calculator.add("1,2,3");
      //    }
  
          @Test
          @DisplayName("when any number of numbers is used then return values are their sums")
          public final void whenAnyNumberOfNumbersIsUsedThenReturnValuesAreTheirSums() {
              Assert.assertEquals(3 + 6 + 15 + 18 + 46 + 33, Calculator.add("3,6,15,18,46,33"));
          }
    ```
  </details>
  <details>
  <summary>Calculator.java solution</summary>

    ```java
    package com.example.demo;
  
    public class Calculator {
      public static int add(final String numbers) {
        int returnValue = 0;
        String[] numbersArray = numbers.split(",");
        // removed after exception
        // if (numbersArray.length > 2) {
        // throw new RuntimeException("Up to 2 numbers separated by comma (,) are allowed");
        // }
        for (String number : numbersArray) {
          if (!number.trim().isEmpty()) { // After refactoring
            returnValue += Integer.parseInt(number);
          }
        }
        return returnValue;
      }
    }
    ```

  All we had to do to accomplish this requirement was to remove part of the code that throws an exception if there are
  more than 2 numbers. However, once tests are executed, the first test failed. In order to fulfill this requirement,
  the test `whenMoreThan2NumbersAreUsedThenExceptionIsThrown` needed to be removed.

  </details>