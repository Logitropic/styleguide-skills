# Agent Skills

A collection of skills for AI coding agents. Skills are packaged instructions and scripts that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

## Available Skills

### pyguide

Google Python Style Guide implementation guidelines. Contains 36 rules covering both Python Language Rules (Section 2) and Python Style Rules (Section 3).

**Use when:**
- Writing new Python code
- Reviewing Python code for style and correctness
- Refactoring existing Python code
- Setting up Python projects with linting and type checking

**Categories:**
- Python Language Rules: Lint, Imports, Packages, Exceptions, Global State, Nested Functions, Comprehensions, Generators, Lambdas, and more
- Python Style Rules: Formatting, Naming, Comments, Strings, Type Annotations, and more

### tsguide

Google TypeScript Style Guide implementation guidelines. Contains 46 rules covering source file basics, imports and exports, language features, classes and functions, naming conventions, the type system, and documentation.

**Use when:**
- Writing new TypeScript code
- Reviewing TypeScript code for style and correctness
- Refactoring existing TypeScript code
- Setting up TypeScript projects with linting and type checking

**Categories:**
- Source File Basics: File encoding, copyright, file overview comments
- Imports & Exports: ES6 imports, named exports, type imports
- Language Features: Variables, arrays, objects, control flow, decorators
- Classes & Functions: Class definitions, method decorators, function declarations
- Naming: Identifiers, naming conventions
- Type System: Type inference, structural types, generics, wrapper types
- Documentation: JSDoc comments, parameter documentation

### swift-guide

Swift Style Guide implementation guidelines based on SwiftLint and Google's Swift style guide. Contains 35 rules covering code organization, naming, types, and best practices.

**Use when:**
- Writing new Swift code
- Reviewing Swift code for style and correctness
- Refactoring existing Swift code
- Setting up iOS/macOS projects with SwiftLint

**Categories:**
- Source File Basics: File structure, imports, comments
- Formatting: Indentation, braces, whitespace, line wrapping
- Naming: Conventions, type names, function names
- Types: Enums, optionals, tuples, custom operators
- Control Flow: Loops, switch statements, guard statements
- Properties & Methods: Access control, initializers, attributes
- Error Handling: Error types, propagation

## Installation

```bash
npx skills add logitropic/styleguide-skills
```

## Usage

Skills are automatically available once installed. The agent will use them when relevant tasks are detected.

**Examples:**
```
Write Python code following Google style guide
```
```
Review this Python code for style issues
```
```
Help me add type annotations to this Python file
```
```
Write TypeScript code following Google style guide
```
```
Review this TypeScript code for style issues
```
```
Help me add JSDoc comments to this TypeScript file
```
```
Write Swift code following style guide
```
```
Review this Swift code for style issues
```

## Skill Structure

Each skill contains:
- `SKILLS.md` or `SKILL.md` - Instructions for the agent
- `rules/` - Individual rule files with detailed explanations and examples

## License

Apache-2.0
