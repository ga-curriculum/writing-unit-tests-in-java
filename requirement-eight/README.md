<h1>
  <span class="headline">Writing Unit Tests in Java</span>
  <span class="subhead">Requirement Eight</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to tktk.

#### Requirement 8: Numbers bigger than 1000 should be ignored

Example: adding `2 + 1001 = 2`

```java 
    @Test
    @DisplayName("When one or more numbers are greater than 1000 is used then it is not included in sum")
    public final void whenOneOrMoreNumbersAreGreaterThan1000IsUsedThenItIsNotIncludedInSum() {
        Assert.assertEquals(3 + 1000 + 6, Calculator.add("3,1000,1001,6,1234"));
    }
```

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
                } else if (numberInt <= 1000) {
                    returnValue += numberInt;
                }
            }
        }
        if (negativeNumbers.size() > 0) {
            throw new RuntimeException("Negatives not allowed: " + negativeNumbers.toString());
        }
        return returnValue;
    }
```

This one was simple. We moved `returnValue += numberInt;` inside an `else if (numberInt <= 1000)`.

### Summary

TDD doesn't exist without a **clean** approach because it minimizes the number of bug errors and duplicates. TDD
involves moving in small steps and comparing the expected results with reality in the context of the **Red** >
**Green** >**Refactoring** process. **Throws** error handling chains are among **Clean Code** practices. One may
transition from one test to another only after receiving a positive result in **Refactoring**. By-products or methods at
the **Green** >**Refactoring** stage may indicate which methods and qualities need to be encapsulated or removed
completely.

It is the efficiency of TDD that cuts its costs:

- This process decreases the time needed to launch and build the project, especially during cold starts
- Tests change before changing the functionality which allows them to perform better
- TDD brings down your stress levels
- This approach supports the project legacy while simplifying writing tests
- It is easier to study architecture in tests because they better indicate the ownership of objects
- TDD its a part of software development automation
- Finally, the code is cleaner