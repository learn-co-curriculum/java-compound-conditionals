# Compound Conditionals

## Learning Goals

- Learn about compound conditionals.

## Introduction to Compound Conditionals

In this lesson, we will be talking more about logical operators and combining
them with conditional clauses!

Let's apply these new operators to conditional statements. Consider the
following example:

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class GradeExample {
  public static void main (String[] args) {
    Scanner scanner = new Scanner(System.in);

    try {
      // Prompt the user to enter a numeric grade from 0 to 100
      System.out.println("Enter a numeric grade from 0 - 100:");
      int grade = scanner.nextInt();
      
      if (grade < 0) {
        // A valid grade is between 0 and 100 inclusively
        System.out.println("Sorry, that is not a valid grade.");
      } else if (grade > 100) {
        System.out.println("Sorry, that is not a valid grade.");
      } else if (grade >= 70) {
          // A passing grade is a 70 or higher
        System.out.println("Congrats! You passed!");
      } else {
        System.out.println("Oops! Better luck next time!");
      }

    } catch (InputMismatchException exception) {
      System.out.println("Invalid input");
    }
  }
}
```

In this example, let's focus on the first two conditional clauses:

```java
if (grade < 0) {
    // Some statements
} else if (grade > 100) {
    // Some other statements
} ...
```

When we prompt the user for a grade, we ask for the user to provide a grade
between 0 and 100. These two conditional clauses take care of the same issue:
if a user enters a valid integer, but an invalid grade. Let's think about what
we are asking from the user. If the user enters a grade that is less than 0
**or** a grade greater than 100, then the user entered an invalid grade.

Hey! We see the word **or** and we have a logical operator called to represent
an `or`. Let's rewrite this code a little and condense these two conditional
clauses:

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class GradeExample {
  public static void main (String[] args) {
    Scanner scanner = new Scanner(System.in);

    try {
      // Prompt the user to enter a numeric grade from 0 to 100
      System.out.println("Enter a numeric grade from 0 - 100:");
      int grade = scanner.nextInt();
      
      if ((grade < 0) || (grade > 100)) {
          // A valid grade is between 0 and 100 inclusively
        System.out.println("Sorry, that is not a valid grade.");
      } else if (grade >= 70) {
          // A passing grade is a 70 or higher
        System.out.println("Congrats! You passed!");
      } else {
        System.out.println("Oops! Better luck next time!");
      }

    } catch (InputMismatchException exception) {
      System.out.println("Invalid input");
    }
  }
}
```

The conditional clause, in this case, combines two boolean expressions:
`grade < 0` and `grade > 100`. Since we are using the `||` operator, Java will
first evaluate the first boolean expression: `grade < 0`. If that expression is
`true`, it will immediately return `true`, as we saw in the truth tables above.
Otherwise, it will evaluate the second expression.

When we combine two or more boolean expressions in a conditional clause, we can
refer to this as a **compound conditional**. Notice in the example above, we
grouped each individual boolean expression between parentheses `()`. It should
be noted that this is not required and that the following is valid as well:
`if (grade < 0 || grade > 100)`. Take into account the readability of the code
to see if the parentheses are fully necessary. They may be helpful when
combining three or more boolean expressions.

Let's run this code in the debugger with a breakpoint at the compound
conditional and a user input of `-8`:

![compound-conditional-breakpoint](https://curriculum-content.s3.amazonaws.com/java-mod-1/logical-operators/intellij-compound-conditional-breakpoint-1.png)

As we can see, the `grade` variable has a value of -8. When we look at the first
conditional clause, `grade < 0 || grade > 100`, we'll see this is equivalent to
`-8 < 0 || -8 > 100`. As we know, with `||` if the first expression is `true`,
Java will evaluate this whole conditional to `true`. And since -8 is less than
0, we should see when we step-over that we fall into this `if` block:

![execute-if-block](https://curriculum-content.s3.amazonaws.com/java-mod-1/logical-operators/intellij-debugger-if-block-execution-3.png)

When we resume the program and look in the console, we will see that the output
looks like this:

```text
Enter a numeric grade from 0 - 100:
-8
Sorry, that is not a valid grade.
```

If we enter in `101` instead, we should get the same message printed in the
console due to the compound conditional!

![compound-conditional-breakpoint](https://curriculum-content.s3.amazonaws.com/java-mod-1/logical-operators/intellij-debugger-compound-conditional-breakpoint.png)

This time, since `grade` has a value of 101, the conditional clause will be
equivalent to `101 < 0 || 101 > 100`. Notice here that Java evaluates both
boolean expressions instead of just the first one. This is because `101 < 0`
results in a `false` value. Therefore, we need to check to see if the second
boolean expression is now `true`, which it is since 101 is greater than 100.
When we step-over, we'll enter in the `if` block again:

![execute-if-block](https://curriculum-content.s3.amazonaws.com/java-mod-1/logical-operators/intellij-debugger-if-block-execution-4.png)

When we resume the program and look in the console, we will see that the output
looks like this:

```text
Enter a numeric grade from 0 - 100:
101
Sorry, that is not a valid grade.
```
