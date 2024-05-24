# C# Coding Conventions

This document outlines the coding conventions for C# projects. Adhering to these conventions ensures that our code is consistent, reliable, and easy to understand. This is crucial for maintaining a high standard of code quality and facilitating collaboration among team members.

## Formatting

### Indentation and Spacing

- Use spaces, not tabs, to create indentation.
- Set your editor to insert 4 spaces for a tab.
- Leave a single blank line between method definitions and between the local variables in a method and its first statement.
- Place open braces (`{`) on the same line as the statement that begins the block of code.
- Place close braces (`}`) on their own line.

### Line Length

- Avoid lines longer than 120 characters. When a statement does not fit on a single line, break it according to these rules:
    - Break after a comma.
    - Break before an operator.
    - Align the new line with the beginning of the expression at the same level on the previous line.
    - Line breaks should occur before binary operators, if necessary.

## Commenting and Documentation

## String Handling
- Prefer string interpolation over concatenation for readability and ease of formatting. String interpolation is identified by the `$` symbol.

Example:
```csharp
var fullName = $"{firstName} {lastName}";
```

- Use string interpolation for constructing dynamic strings or when embedding variables into a string.

Example:
```csharp
var greeting = $"Hello, {fullName}. Today is {DateTime.Now.DayOfWeek}.";
```

- Be mindful of escape sequences and verbatim strings when using string interpolation.

- Use `StringBuilder` for complex string manipulations, particularly within loops or when constructing large strings.

Example:
```csharp
var builder = new StringBuilder();
for (int i = 0; i < 10; i++)
{
    builder.AppendLine($"Line {i}");
}
string result = builder.ToString();
```

- `StringBuilder` is more efficient than string concatenation in scenarios involving frequent modifications, as it reduces memory allocations and enhances performance.

### General Guidelines for String Operations
- Performance Considerations: Understand the performance implications of string operations. For operations involving large or numerous strings, or within performance-critical sections of code, prefer StringBuilder.

- Readability and Maintainability: Prioritize readability and maintainability of your code. Use interpolation for simpler or less frequent operations where performance is not a concern.

- Security Considerations: Be cautious with dynamic string construction, especially when constructing SQL queries or other expressions that might be executed. Use parameterized queries or similar mechanisms to avoid injection vulnerabilities.

### Inline Comments

- Use inline comments sparingly.
- Write comments to explain why something is being done, not what is being done; the code itself should be as self-explanatory as possible.

### XML Documentation Comments

- Use `///` comments to describe classes, interface, enum, property, field, and method declarations. These comments create documentation for the code and can be extracted to a separate file.
- Provide a summary for every public, protected, or internal member, and provide remarks, parameter, and return information where applicable.

## Naming

- Refer to the `naming-conventions.md` document for detailed guidelines on naming classes, methods, variables, etc.

## Error Handling

- Prefer exceptions to returning error codes.
- Throw exceptions for abnormal or unexpected conditions only, not for normal flow control.
- Use try-catch-finally blocks to recover from errors or release resources.
- When catching exceptions, be specific about the exception types you are handling.

## Performance

- Avoid premature optimization. Write clear, maintainable code and optimize only after you've identified performance issues.
- Consider the performance implications of your design decisions (e.g., choice of algorithms, data structures).

## Code Structure and Organization

### Methods

- Keep methods short and focused on a single task.
- Avoid deep nesting of control structures.
- Extract pieces of code that are reused or can be isolated into separate methods.

### Classes and Interfaces

- Follow the Single Responsibility Principle: a class or interface should have only one reason to change.
- Use interfaces or abstract base classes to provide polymorphic behavior.
- Prefer composition over inheritance where practical.

### Asynchronous Programming

- Use `async` and `await` for asynchronous code, ensuring the code remains readable and maintainable.
- Avoid blocking calls in asynchronous code, which can lead to deadlocks and performance issues.

## Asynchronous Programming Conventions

Asynchronous programming is a key part of modern software development, particularly in environments with high I/O operations or scalability requirements. Properly naming asynchronous methods improves code readability and maintainability. Avoid blocking calls in asynchronous code, which can lead to deadlocks and performance issues Follow these conventions when naming asynchronous methods:

### Async Postfix

- Append the `Async` postfix to the names of all asynchronous methods to clearly indicate that they are asynchronous and should be awaited or handled asynchronously. This makes the control flow clearer and prevents unintentional blocking calls.
  
Example:
```csharp
public async Task<HttpResponse> GetDataAsync()
{
    // Implementation
}
```

#### Exceptions to the Async Postfix Rule
While the Async postfix is a general convention, there are specific cases where it is omitted for clarity or by convention:

1. Test Methods: 
Asynchronous test methods typically do not include the Async postfix. This is because the focus is on the test scenario and behavior rather than the asynchronicity of the method itself.

Example:
```csharp
[Fact]
public async Task CanRetrieveData()
{
    // Test implementation
}

```

2. Controller Methods in Web Applications: In the context of ASP.NET or similar frameworks, controller actions that are asynchronous usually do not include the Async postfix. This is a convention stemming from the fact that the routing and action name in the URL do not need to reveal implementation details like asynchronicity.

Example:
```csharp
public async Task<ActionResult> Details(int id)
{
    // Implementation
}
```

## Object Initializers
- Use object initializers to simplify object creation and make the code more readable.

Example:
```csharp
var person = new Person
{
    FirstName = "John",
    LastName = "Doe",
    Age = 30
};
```

- For complex objects, ensure each property initialization is on a new line and properly indented.

Example:
```csharp
var order = new Order
{
    OrderId = 1,
    OrderDate = DateTime.Now,
    Items = new List<OrderItem>
    {
        new OrderItem { /* ... */ },
        new OrderItem { /* ... */ }
    }
};
```
