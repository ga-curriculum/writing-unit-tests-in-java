<h1>
  <span class="headline">Writing Unit Tests in Java</span>
  <span class="subhead">Requirement Seven</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to tktk.

#### Requirement 7: Negative numbers will throw an exception

Calling Add with a negative number will throw an exception **negatives not allowed** – and the negative that was passed.
If there are multiple negatives, show all of them in the exception message.

```java 
    @Test(expected = RuntimeException.class)
    @DisplayName("When negative number is used then runtime exception is thrown")
    public final void whenNegativeNumberIsUsedThenRuntimeExceptionIsThrown() {
        Calculator.add("3,-6,15,18,46,33");
    }

    @Test
    @DisplayName("When negative numbers is used then runtime exception is thrown")
    public final void whenNegativeNumbersAreUsedThenRuntimeExceptionIsThrown() {
        RuntimeException exception = null;
        try {
            Calculator.add("3,-6,15,-18,46,33");
        } catch (RuntimeException e) {
            exception = e;
        }
        Assert.assertNotNull(exception);
        Assert.assertEquals("Negatives not allowed: [-6, -18]", exception.getMessage());
    }
```

There are two new tests. First one checks whether exception is thrown when there are negative numbers. The second one
verifies whether the exception message is correct.

```java 
      private static int add(final String numbers, final String delimiter) {
          int returnValue = 0;
          String[] numbersArray = numbers.split(delimiter);
          List<Integer> negativeNumbers = new ArrayList<Integer>();
          for (String number : numbersArray) {
              if (!number.trim().isEmpty()) {
                  int numberInt = Integer.parseInt(number.trim());
                  if (numberInt < 0) {
                      negativeNumbers.add(numberInt);
                  }
                  returnValue += numberInt;
              }
          }
          if (negativeNumbers.size() > 0) {
              throw new RuntimeException("Negatives not allowed: " + negativeNumbers.toString());
          }
          return returnValue;
      }
```

This time code was added that collects negative numbers in a List and throws an exception if there was any.
