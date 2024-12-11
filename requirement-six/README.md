<h1>
  <span class="headline">Writing Unit Tests in Java</span>
  <span class="subhead">Requirement Six</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to tktk.

#### Requirement 6: Support different delimiters

```java 
    @Test
    @DisplayName("When delimiter is specified then it is used to separate numbers")
    public final void whenDelimiterIsSpecifiedThenItIsUsedToSeparateNumbers() {
        Assert.assertEquals(3 + 6 + 15, Calculator.add("//;n3;6;15"));
    }
```

```java
package com.example.demo;

public class Calculator {

    public static int add(final String numbers) {
        String delimiter = ",|n";
        String numbersWithoutDelimiter = numbers;
        if (numbers.startsWith("//")) {
            int delimiterIndex = numbers.indexOf("//") + 2;
            delimiter = numbers.substring(delimiterIndex, delimiterIndex + 1);
            numbersWithoutDelimiter = numbers.substring(numbers.indexOf("n") + 1);
        }
        return add(numbersWithoutDelimiter, delimiter);
    }

    private static int add(final String numbers, final String delimiter) {
        int returnValue = 0;
        String[] numbersArray = numbers.split(delimiter);
        for (String number : numbersArray) {
            if (!number.trim().isEmpty()) {
                returnValue += Integer.parseInt(number.trim());
            }
        }
        return returnValue;
    }
}
```

This time there was quite a lot of refactoring. We split the code into 2 methods. Initial method parses the input
looking for the delimiter and later on calls the new one that does the actual sum. Since we already have tests that
cover all existing functionality, it was safe to do the refactoring. If anything went wrong, one of the tests would find
the problem.