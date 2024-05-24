# TypeScript Coding Standards

This document outlines the coding standards for TypeScript projects, inspired by Google's style guide. These standards are intended to promote code clarity, consistency, and best practices in our TypeScript codebase.

## General Principles

- **Readability**: Code should be written for readability. Someone unfamiliar with your code should be able to understand its purpose without extensive documentation.
- **Maintainability**: Write code that is easy to maintain and extend. Consider the future developers who will work on your code.
- **Consistency**: Consistent coding practices make the codebase easier to understand and work with.

## Coding Standards

### Indentation and Spacing

- Use 2 spaces for indentation, not tabs.
- Use whitespace to make the code more readable.
- Place one space before the opening brace of a block.
- Place no space between the function name and the parentheses for parameters.

Example:
```typescript
  if (condition) {
    // Code block
  }

  function exampleFunction(param: string): void {
    // ...
  }
```

### Variable Declaration and Usage

#### 1. Avoid `var`

- Never use `var` for declaring variables. The `var` keyword is function-scoped and can lead to unexpected behavior due to variable hoisting. Instead, use block-scoped variable declarations: `let` and `const`.

#### 2. Use `const` and `let`

- **`const`**: Use `const` for declaring variables that will not be reassigned after initialization. This signals that the variable's value will remain constant, which can help prevent accidental reassignments and provide more readable code.

Example:
```typescript
const MAX_ATTEMPTS = 5;
const userName = 'JohnDoe';
```

- `let`: Use `let` for declaring variables whose values will or might change over time. let is block-scoped, which makes it a safer choice than `var` and helps prevent issues related to variable hoisting and scope confusion.

Example:
```typescript
let counter = 0;
counter += 1;
```

### Semicolons
- Use semicolons to terminate statements. This helps avoid potential pitfalls with JavaScript's automatic semicolon insertion.
Example:

```typescript
let name: string = 'Example';
console.log(name);
```

### Naming Conventions
- Follow the naming conventions outlined in the [TypeScript Naming Conventions document](./naming-conventions.md)

### Types and Interfaces
- Always use explicit types where possible. Avoid using any as it bypasses the compiler's type checking.
- Use interfaces for object type definitions to benefit from TypeScript's powerful type system. Prefer interfaces over the types (`type`).

Example:
```typescript
interface User {
  name: string;
  age: number;
}
```

### Arrow Functions vs. Traditional Functions
- Prefer arrow functions over traditional function expressions for anonymous functions, especially for inner functions or callbacks.

Example:
```typescript
const names = ['Alice', 'Bob', 'Charlie'];
const lengths = names.map((name) => name.length);
```

### Modules
- Use modules (`import`/`export``) over namespaces. Modules provide a way to structure your code and manage dependencies.

### Comments and Documentation
- Use comments meaningfully. Comment on the why, not the what.
- Use JSDoc-style comments for function documentation, including parameters and return types.

Example:
```typescript
/**
 * Calculates the area of a rectangle.
 * @param width - The width of the rectangle.
 * @param height - The height of the rectangle.
 * @return The area of the rectangle.
 */
function calculateArea(width: number, height: number): number {
  return width * height;
}

```

### Error Handling
- Use try-catch blocks for operations that might throw errors.
- Always handle errors in a meaningful way, avoiding empty catch blocks.

### Import Statement Formatting

- **No Spaces in Brackets**: Do not include spaces between brackets and the imported entities.
- **Multiline Imports**: For long import lists, use multiline import statements to maintain readability.

Example:
```typescript
  // Single line import
  import {Component, OnInit} from '@angular/core';
  
  // Multiline import
  import {
    LongDependencyOne,
    LongDependencyTwo,
    LongDependencyThree,
    // ...other dependencies
  } from '@angular/core';
```

- Use aliases prefixed with `@` to simplify import paths and avoid long relative paths.
- Avoid using absolute paths for internal modules.

Example:
```typescript
// Avoid
import {UserService} from '../../../services/userService';

// Prefer
import {UserService} from '@services';
```

### Module Organization with index.ts
- Create an `index.ts` file in each directory to re-export entities (classes, types, interfaces, constants).
- This practice simplifies import paths and enhances code organization.

Example
```typescript
// In index.ts of a folder
export * from './myClass';
export * from './myInterface';
export * from './myConstants';

// Usage in other files
import {MyClass, MyInterface, MY_CONSTANT} from '@myModule';
```

### Package Management
- Be mindful of the packages you install. Avoid adding redundant or unnecessary packages to keep the project lightweight and maintainable.
- Regularly review and clean up package dependencies.

### Program Entry File
- Name the program entry file `main.ts`.
- Use this file to call initialization or setup functions, setting a clear entry point for the application.

Example:
```typescript
// main.ts
import {initializeApp} from '@appInitializer';

initializeApp();

// the class based approach
import {initializeApp} from '@appInitializer';

class App {
  run() {
    initializeApp();
  }
}

(new App()).run();
```

### Utility Functions and Strong OOP Approach
- Avoid standalone helper or utility functions. Instead, encapsulate these functions within technical classes.
- Define utility functions within abstract classes marked as static.
- This approach aligns with a strong OOP philosophy and keeps the codebase organized.

Example:
```typescript
export abstract class StringUtils {
  static capitalizeFirstLetter(input: string): string {
    return input.charAt(0).toUpperCase() + input.slice(1);
  }

  static isNullOrEmpty(input: string): boolean {
    return input == null || input === '';
  }
}
```


### Linting with Google ESLint
- Ensure code quality and consistency by using ESLint with Google's configuration.
- To install, run the following command:

```bash
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-config-google
```

- Create an `.eslintrc` file in your project root and add the following configuration:

```json
{
    "parser": "@typescript-eslint/parser",
    "plugins": ["@typescript-eslint"],
    "extends": ["eslint:recommended", "google", "plugin:@typescript-eslint/recommended"],
    "parserOptions": {
        "ecmaVersion": 2020,
        "sourceType": "module"
    },
    "rules": {
        // Add custom rules here
    }
}
```

### Null Usage
- Prefer using `null` over `undefined` to represent the intentional absence of a value.
- For checking null or undefined, use `== null` or `!= null` which checks for both `null` and `undefined`.

Example:
```typescript
if (variable == null) {
  // variable is null or undefined
}

// or you can use the operator !
if (!variable) {
  // variable is null, undefined or equals to zero
}
```

### Strict Equality
- Use === and !== operators for comparisons, except when checking for null or undefined as mentioned above. This avoids type coercion and ensures that the comparison is made with proper type checking.

Example:
```typescript
if (value === 123) {
  // value is strictly equal to 123
}
```

### Modifiers and Field Initialization
- Explicitly specify visibility modifiers (private, protected) for fields, getter/setter properties, and methods to enhance code clarity and encapsulation.
- For public methods, the public modifier is not necessary as it's the default.
- Use `override` keyword for overriding the parent class method

Example:

```typescript
class Example {
  private privateMethod(): void {
    // ...
  }

  protected protectedMethod(): void {
    // ...
  }

  // public is optional
  public publicMethod(): void {
    // ...
  }

  public override virtualMethod(): void {
    // ...
    super.virtualMethod(); // usually you would call the base method but it depends on the case
  }
}
```

- Prefer initializing fields directly when you declare them, rather than in the constructor. This makes the code cleaner and ensures that the fields are initialized before any methods are called.
- For union types or when the field might hold a null value, explicitly specify the type.

Example:

```typescript
class Example {
  // Direct initialization
  private str1 = '';
  private num1 = 0;

  // Explicit type for union types or potential null values
  private str2: string | null = null;
}
```
