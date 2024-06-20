# Interpreter Design Pattern

## Summary

### Problem

The Interpreter design pattern is used to define a grammatical representation for a language and provide an interpreter to deal with this grammar. The pattern solves the problem of parsing and interpreting expressions from a language, making it useful when you need to interpret sentences in a simple language, typically domain-specific languages (DSLs).

### Solution

The Interpreter pattern involves defining a class hierarchy that represents the grammar of the language. Each rule in the grammar is represented by a class. An interpreter object then processes expressions of the language by recursively evaluating the grammar.

### When to Use

Use the Interpreter design pattern when:

- You have a simple language or grammar to interpret.
- The grammar is relatively stable and not subject to frequent changes.
- The language can be represented as a syntax tree, with each node representing a rule in the grammar.

### Example Code

Here's an example of using the Interpreter pattern to evaluate simple mathematical expressions:

```java
import java.util.Map;
import java.util.HashMap;

// Abstract Expression
interface Expression {
    int interpret(Map<String, Integer> context);
}

// Terminal Expression
class Number implements Expression {
    private final int number;

    public Number(int number) {
        this.number = number;
    }

    @Override
    public int interpret(Map<String, Integer> context) {
        return number;
    }
}

// Variable Expression
class Variable implements Expression {
    private final String name;

    public Variable(String name) {
        this.name = name;
    }

    @Override
    public int interpret(Map<String, Integer> context) {
        if (context.get(name) == null) {
            throw new RuntimeException("No value for variable: " + name);
        }
        return context.get(name);
    }
}

// Add Expression
class Add implements Expression {
    private final Expression leftExpression;
    private final Expression rightExpression;

    public Add(Expression leftExpression, Expression rightExpression) {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    @Override
    public int interpret(Map<String, Integer> context) {
        return leftExpression.interpret(context) + rightExpression.interpret(context);
    }
}

// Subtract Expression
class Subtract implements Expression {
    private final Expression leftExpression;
    private final Expression rightExpression;

    public Subtract(Expression leftExpression, Expression rightExpression) {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    @Override
    public int interpret(Map<String, Integer> context) {
        return leftExpression.interpret(context) - rightExpression.interpret(context);
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        // Construct the expression (a + b) - (c - 10)
        Expression expression = new Subtract(
            new Add(new Variable("a"), new Variable("b")),
            new Subtract(new Variable("c"), new Number(10))
        );

        // Define the context
        Map<String, Integer> context = new HashMap<>();
        context.put("a", 20);
        context.put("b", 5);
        context.put("c", 30);

        // Interpret the expression
        int result = expression.interpret(context);
        System.out.println("Result: " + result);  // Result: 5
    }
}
```

### Explanation

- **Expression Interface**: Defines the `interpret` method.
- **Terminal Expressions (Number, Variable)**: Represent the basic elements of the language.
- **Non-terminal Expressions (Add, Subtract)**: Represent the composite elements of the language and can contain other expressions.
- **Client**: Builds an abstract syntax tree (AST) representing the expression and then interprets it using a context (variable values).

### Cons

- **Complexity**: The pattern can lead to a large number of classes for each rule in the grammar, making it hard to manage.
- **Performance**: Recursive calls can lead to performance issues for complex grammars or large expressions.
- **Maintainability**: Changes in the grammar may require changes in multiple classes, making maintenance difficult.
- **Scalability**: Not suitable for complex or constantly evolving grammars due to the explosion of class count and interdependencies.

### Summary

The Interpreter design pattern is useful for defining a grammar and interpreting sentences in that grammar, especially for simple or domain-specific languages. While it provides a clear and manageable way to handle expressions and their evaluation, it can become cumbersome and inefficient for more complex languages or frequently changing grammars.