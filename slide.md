<!-- .slide: data-background-color="#282C34" -->
# Java Lambdas
### An Introduction to Functional Programming

---

## What is a Lambda Expression?

- A lambda expression is a short block of code which takes in parameters and returns a value.
- Syntax:
  ```java
  (parameters) -> expression
  ```
- Example:
  ```java
  (int x, int y) -> x + y
  ```

---

## Why Use Lambdas?

- Reduces boilerplate code.
- Makes code more readable and concise.
- Can be used to create **anonymous functions**.

---

## Syntax Breakdown

- **Parameters**: The input values for the lambda.
- **Arrow (`->`)**: Separates parameters and the body.
- **Body**: The logic or expression to execute.

Example:

```java
(int a, int b) -> a * b
```

---

## Example: Lambda as a Parameter

```java
import java.util.function.IntBinaryOperator;

public class LambdaExample {
    public static void main(String[] args) {
        IntBinaryOperator add = (x, y) -> x + y;
        System.out.println(add.applyAsInt(10, 20));  // Output: 30
    }
}
```

---

## Common Use Cases

- Functional interfaces like `Runnable`, `Callable`, `Comparator`.
- Stream API operations (e.g., `filter`, `map`, `reduce`).

---

## Let's Try a Lambda!

- Write a lambda that multiplies two numbers.
- Syntax: `(a, b) -> a * b`

---

## Resources

- [Oracle Documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)
- [Baeldung Guide](https://www.baeldung.com/java-8-lambda-expressions-tips)
