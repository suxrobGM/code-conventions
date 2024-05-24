# TypeScript Naming Conventions

This document outlines the naming conventions for TypeScript code, ensuring consistency, readability, and maintainability. Similar to C# conventions, these guidelines help in creating a unified codebase that is easy to understand and work with.
Below are the naming conventions for TypeScript code inspired by [Google's](https://google.github.io/styleguide/tsguide.html) style guide.

## General Principles

- **Clarity and Readability**: Names should clearly convey the purpose of the entity. Avoid abbreviations and single-letter names unless they are widely accepted and understood.
- **Consistency**: Use the same naming patterns throughout your TypeScript code.
- **Predictability**: Names should be predictable, allowing team members to infer what an entity does or represents without needing to read the implementation.

## Naming Styles

- **camelCase**: Begin with a lowercase letter and capitalize the first letter of subsequent concatenated words, e.g., `localVariable`, `jsonString`.
- **PascalCase**: Capitalize the first letter of each word, including acronyms over two letters in length, e.g., `HtmlButton`, `CpuUsage`.

## Specific Conventions

### File Names

- Use **camelCase** for file names, reflecting the primary export or the most significant entity in the file.
  - Example: `userRepository.ts`

- Use lower kebab case for file names for the assets such as images, fonts, css etc, reflecting the primary export or the most significant entity in the file.
  - Example: `user-avatar.png`

### Classes and Interfaces

- Use **PascalCase** for class and interface names.
  - Example: `UserProfile`, `HttpService`, `IUserRepository`

### Methods and Functions

- Use **camelCase** for method and function names.
  - Example: `getUserData()`, `sendRequest()`

### Constants

- Use **UPPER_CASE** for constants. For constant values that are meant to be hard-coded and unchanging, use uppercase letters with underscores.
  - Example: `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`

### Variables and Properties

- Use **camelCase** for variable and property names.
  - Example: `let itemCount`, `const userName`

### Private Variables with Accessors

In cases where private variables have associated getter and setter properties, it is a common practice to prefix the private variable names with an underscore (`_`). This convention helps to avoid naming conflicts between the private variable and its public getter and setter, and also clearly indicates that the variable is intended for private use within the class.

#### Rules and Examples

- **Prefix private variables with an underscore** (`_`) if you are going to create getter and setter properties with the same base name.

```typescript
class User {
  private _name: string;

  public get name(): string {
    return this._name;
  }

  public set name(value: string) {
    this._name = value;
  }
}
```

- Use `camelCase` for the getter and setter names, and ensure they match the base name of the private variable, omitting the underscore prefix.

- This convention provides clarity by differentiating the private variable from its public interface and indicates that direct access to the variable should be avoided in favor of the accessors.

#### General Guidelines
- `Consistency`: Apply this naming convention consistently across your classes. Inconsistencies can lead to confusion and make the code harder to maintain.
- `Clarity`: Choose clear and descriptive names for your variables and accessors to make the code self-explanatory.
- `Encapsulation`: Use getters and setters to control access to the data and to add validation logic if needed, adhering to the principles of encapsulation.

### Enums

- Use **PascalCase** for enum names and **UPPER_CASE** for enum values.

Example:
```typescript
enum Color {
  RED = "RED",
  GREEN = "GREEN",
  BLUE = "BLUE"
}
```
