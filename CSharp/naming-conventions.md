# C# Naming Conventions

Proper naming is crucial for readability and maintainability of the code. This document outlines the naming conventions for the C# projects to ensure consistency across our codebase. Adhering to these conventions is important for all team members.

## General Principles

1. **Clarity and Readability**: Names should clearly convey the purpose of the entity. Avoid abbreviations and single-letter names (except for local variables and well-known entities like `i` in loops).
2. **Consistency**: Follow the same naming patterns throughout the codebase.
3. **Predictability**: Names should be predictable, allowing team members to infer what an entity does or represents without needing to read the implementation.

## Naming Styles

- **PascalCase**: Capitalize the first letter of each word, including acronyms over two letters in length, e.g., `HtmlButton`, `CpuUsage`.
- **camelCase**: Begin with a lowercase letter and capitalize the first letter of subsequent concatenated words, e.g., `localVariable`, `jsonString`.

## Specific Conventions

### Classes and Interfaces

- Use **PascalCase**.
- Prefer nouns or noun phrases, e.g., `Employee`, `BusinessProcess`.
- For interfaces, start with an uppercase 'I' followed by PascalCase, e.g., `IRepository`, `IService`.

### Methods

- Use **PascalCase**.
- Prefer verbs or verb phrases, e.g., `CalculateTotal`, `ValidateInput`.
- Parameters should use **camelCase**.

### Variables

- Use **camelCase** for local variables and method parameters.
- Use **PascalCase** for properties, fields, and constants.
- For private or internal fields, prefix with an underscore, e.g., `_internalCache`, `_maxSize`.

### Local Variables and Lambda Expressions

- Choose meaningful and descriptive names that clearly indicate the purpose of the variable.
- **Avoid short, vague names** like `x`, `y`, `i`, or `j`, which do not provide context or meaning. These names make the code harder to understand and maintain. The only exception is for indexes in simple loops or well-known mathematical algorithms where such names are traditional.

#### Exception for Lambda Functions

- When using lambda functions, it's acceptable to use short names like `x` or `y` for arguments if the lambda expression is short, and the purpose of the argument is clear and unambiguous within the context of the lambda. This is a common convention in LINQ queries or simple delegates.
- Example of acceptable usage in a lambda function:

```csharp
var evenNumbers = numbers.Where(x => x % 2 == 0);
```

- Even in lambda functions, if the expression is complex or spans multiple lines, prefer descriptive names to enhance readability.

By adhering to these conventions, we aim to ensure that our code is immediately understandable, reducing the cognitive load on the reader and making the codebase more maintainable and enjoyable to work with.

### Constants and Enumerations

- Use **PascalCase** for enumeration values.
- Constants should be all uppercase, with words separated by underscores, e.g., `MAX_RETRY_COUNT`.

### Namespaces

- Use **PascalCase**.
- Namespaces should be named after the project or service name, and possibly subdivided based on functionality or layer, e.g., `ProjectName.DataAccess`.

### Generics

- Use descriptive names with **PascalCase**, unless the type parameter is unconstrained and generic, in which case use single uppercase letters, e.g., `T`, `TKey`, `TValue`.
- Example: `public class Repository<TItem> where TItem : IEntity`.

## Exceptions

- Avoid using abbreviations, except for well-accepted ones like `Id`, `Xml`, `Ftp`, etc.
- In cases where existing .NET naming conventions conflict with these guidelines, align with the .NET conventions to ensure consistency.
