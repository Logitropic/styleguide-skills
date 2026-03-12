---
name: google-python-styleguide
description: Google Python Style Guide implementation guidelines. This skill should be used when writing, reviewing, or refactoring Python code to ensure compliance with Google Python Style Guide. Triggers on tasks involving Python source files, linting, code reviews, or any Python development work.
license: Apache-2.0
metadata:
  author: google
  version: "1.0.0"
---

# Google Python Style Guide

Comprehensive Python coding guidelines based on Google's Python Style Guide. Contains 36 rules covering Python Language Rules (Section 2) and Python Style Rules (Section 3), focusing on code quality, readability, and best practices.

## When to Apply

Reference these guidelines when:
- Writing new Python code
- Reviewing Python code for style and correctness
- Refactoring existing Python code
- Setting up Python projects with linting and type checking
- Teaching Python best practices

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Linting | CRITICAL | `lint-` |
| 2 | Imports & Packages | CRITICAL | `import-` |
| 3 | Exceptions | HIGH | `exception-` |
| 4 | Type Annotations | HIGH | `type-` |
| 5 | Code Style & Formatting | HIGH | `style-` |
| 6 | Global State & Mutability | MEDIUM | `global-` |
| 7 | Control Flow | MEDIUM | `control-` |
| 8 | Functions & Methods | MEDIUM | `func-` |
| 9 | Classes & Properties | MEDIUM | `class-` |
| 10 | Modern Python | LOW | `modern-` |
| 11 | Advanced Features | LOW | `advanced-` |

## Quick Reference

### Section 2: Python Language Rules

#### 2.1 Lint (`lint`)
- `lint-lint` - Run pylint on code and address warnings

#### 2.2 Imports (`import`)
- `import-module` - Use `import x` for packages and modules
- `import-from` - Use `from x import y` with package prefix
- `import-alias` - Use aliases for conflicts or standard abbreviations

#### 2.3 Packages (`package`)
- `package-structure` - Use absolute imports, not relative

#### 2.4 Exceptions (`exception`)
- `exception-builtin` - Use built-in exception classes (ValueError, TypeError)
- `exception-assert` - Don't use assert for runtime validation
- `exception-custom` - Custom exceptions must inherit from existing classes
- `exception-catch-all` - Never use bare `except:` statements
- `exception-try-minimal` - Minimize code in try/except blocks

#### 2.5 Global State (`global`)
- `global-mutable` - Avoid mutable global state

#### 2.6 Nested (`nested`)
- `nested-functions` - Nested classes and functions allowed with care
- `nested-leaky` - Don't leak local variables to enclosing scope

#### 2.7 Comprehensions (`comprehension`)
- `comprehension-simple` - Simple comprehensions allowed
- `comprehension-multiple` - Multiple for clauses and if conditions OK
- `comprehension-avoid` - Avoid complex comprehensions

#### 2.8 Default Iterators (`iterator`)
- `iterator-dict` - Use default iterators for dict (for k in dict)
- `iterator-set` - Use default iterators for sets
- `iterator-len` - Use len() instead of sentinel values

#### 2.9 Generators (`generator`)
- `generator-use` - Use generators for large sequences
- `generator-doc` - Document generators with "Yields:"

#### 2.10 Lambda Functions (`lambda`)
- `lambda-one-line` - Lambdas OK for one-liners
- `lambda-prefer-comprehension` - Prefer comprehensions over map/filter

#### 2.11 Conditional Expressions (`conditional`)
- `conditional-simple` - Use conditional expressions for simple cases
- `conditional-one-line` - Keep conditional expressions on one line

#### 2.12 Default Argument Values (`default-arg`)
- `default-arg-mutable` - Never use mutable default arguments

#### 2.13 Properties (`property`)
- `property-use` - Use properties for computed attributes
- `property-getter` - Use getters for attribute access

#### 2.14 True/False Evaluations (`truefalse`)
- `truefalse-implicit` - Use implicit true/false evaluations
- `truefalse-none` - Use `is None` instead of `== None`

#### 2.16 Lexical Scoping (`scoping`)
- `scoping-closure` - Use lexical scoping correctly for closures

#### 2.17 Decorators (`decorator`)
- `decorator-use` - Use decorators judiciously
- `decorator functools` - Use functools.wrails for decorators

#### 2.18 Threading (`thread`)
- `thread-queue` - Use queue module for threading
- `thread-atomic` - Don't rely on atomic types

#### 2.19 Power Features (`power`)
- `power-avoid` - Avoid metaclasses, __del__, reflection

#### 2.20 Modern Python (`modern`)
- `modern-future` - Use `from __future__ import` statements

#### 2.21 Type Annotated Code (`type`)
- `type-annotations` - Add type hints to all functions
- `type-checker` - Use pytype or similar type checker

### Section 3: Python Style Rules

#### 3.1 Semicolons (`semicolon`)
- `semicolon-no` - No semicolons to terminate lines
- `semicolon-statement` - Semicolons allowed for multiple statements on one line

#### 3.2 Line Length (`line-length`)
- `line-length-80` - Maximum 80 characters per line
- `line-length-exception` - Exceptions for long imports or URLs

#### 3.3 Parentheses (`parentheses`)
- `parentheses-minimal` - Use parentheses sparingly
- `parentheses-call` - No spaces after function name

#### 3.4 Indentation (`indent`)
- `indent-4-spaces` - Use 4 spaces for indentation
- `indent-no-tabs` - No tabs
- `indent-line-continuation` - Hanging indent with 4 spaces

#### 3.5 Blank Lines (`blank`)
- `blank-top-level` - Two blank lines between top-level definitions
- `blank-methods` - One blank line between methods
- `blank-end` - No extra blank lines at end of file

#### 3.6 Whitespace (`whitespace`)
- `whitespace-operators` - No spaces around = for keyword args
- `whitespace-commas` - No trailing commas
- `whitespace-colon` - No space before colon

#### 3.8 Comments and Docstrings (`comments`)
- `comments-inline` - Use inline comments sparingly
- `comments-docstring` - Use """ for docstrings
- `comments-complete` - Write complete sentences
- `comments-block` - Use # for block comments

#### 3.10 Strings (`strings`)
- `strings-format` - Use f-strings, format(), or % for strings
- `strings-quotes` - Use consistent quotes (prefer double quotes)
- `strings-avoid-concat` - Avoid string concatenation with +

#### 3.11 Files and Sockets (`files`)
- `files-close` - Always close files and sockets
- `files-context` - Use context managers (with statement)

#### 3.12 TODO Comments (`todo`)
- `todo-format` - Use TODO(username) format
- `todo-link` - Include bug number or issue link

#### 3.13 Imports Formatting (`imports-format`)
- `imports-group` - Group imports: standard, third-party, local
- `imports-sort` - Sort imports alphabetically within groups
- `imports-future` - Place __future__ imports before others

#### 3.14 Statements (`statements`)
- `statements-one` - One statement per line
- `statements-import` - Import only one module per line

#### 3.15 Access Control (`access`)
- `access-private` - Use _ prefix for private attributes
- `access-property` - Use properties instead of public attributes

#### 3.16 Naming (`naming`)
- `naming-functions` - snake_case for functions and variables
- `naming-classes` - CapWords for classes
- `naming-constants` - CAPS_WITH_UNDERSCORES for constants
- `naming-modules` - short lowercase names for modules

#### 3.17 Main (`main`)
- `main-guard` - Use if __name__ == '__main__': guard

#### 3.18 Function Length (`function-length`)
- `function-length-limit` - Keep functions under 40 lines
- `function-single-purpose` - Each function does one thing

#### 3.19 Type Annotations (`type-annotation`)
- `type-annotation-required` - Type annotations required
- `type-annotation-none` - Use X | None instead of Optional[X]
- `type-annotation-import` - Import typing modules properly

## Rule Files Index

### Section 2: Python Language Rules (2.1 - 2.21)

| Section | File | Topic |
|---------|------|-------|
| 2.1 | lint.md | Lint |
| 2.2 | imports.md | Imports |
| 2.3 | packages.md | Packages |
| 2.4 | exceptions.md | Exceptions |
| 2.5 | global-state.md | Mutable Global State |
| 2.6 | nested.md | Nested/Local/Inner Classes and Functions |
| 2.7 | comprehensions.md | Comprehensions & Generator Expressions |
| 2.8 | default-iterators-and-operators.md | Default Iterators and Operators |
| 2.9 | generators.md | Generators |
| 2.10 | lambda-functions.md | Lambda Functions |
| 2.11 | conditional.md | Conditional Expressions |
| 2.12 | default-argument-values.md | Default Argument Values |
| 2.13 | properties.md | Properties |
| 2.14 | truefalse-evaluations.md | True/False Evaluations |
| 2.16 | lexical-scoping.md | Lexical Scoping |
| 2.17 | decorators.md | Function and Method Decorators |
| 2.18 | threading.md | Threading |
| 2.19 | power-features.md | Power Features |
| 2.20 | modern-python.md | Modern Python: from __future__ imports |
| 2.21 | type-annotated-code.md | Type Annotated Code |

### Section 3: Python Style Rules (3.1 - 3.19)

| Section | File | Topic |
|---------|------|-------|
| 3.1 | semicolons.md | Semicolons |
| 3.2 | indentation.md | Line length & Indentation |
| 3.3 | parentheses.md | Parentheses |
| 3.4 | indentation.md | Indentation |
| 3.5 | blank-lines.md | Blank Lines |
| 3.6 | whitespace.md | Whitespace |
| 3.8 | comments-and-docstrings.md | Comments and Docstrings |
| 3.10 | strings.md | Strings |
| 3.11 | files-sockets-closables.md | Files, Sockets, and similar Stateful Resources |
| 3.12 | todo-comments.md | TODO Comments |
| 3.13 | imports-formatting.md | Imports formatting |
| 3.14 | statements.md | Statements |
| 3.15 | access-control.md | Getters and Setters (Access Control) |
| 3.16 | naming.md | Naming |
| 3.17 | main.md | Main |
| 3.18 | function-length.md | Function length |
| 3.19 | type-annotations.md | Type Annotations |

## How to Use

Read individual rule files for detailed explanations and code examples:

```
rules/lint.md              # 2.1 Lint
rules/imports.md           # 2.2 Imports
rules/packages.md          # 2.3 Packages
rules/exceptions.md        # 2.4 Exceptions
rules/global-state.md      # 2.5 Global State
rules/nested.md            # 2.6 Nested
rules/comprehensions.md    # 2.7 Comprehensions
rules/default-iterators-and-operators.md  # 2.8 Default Iterators
rules/generators.md        # 2.9 Generators
rules/lambda-functions.md  # 2.10 Lambda Functions
rules/conditional.md       # 2.11 Conditional Expressions
rules/default-argument-values.md  # 2.12 Default Arguments
rules/properties.md        # 2.13 Properties
rules/truefalse-evaluations.md  # 2.14 True/False
rules/lexical-scoping.md   # 2.16 Lexical Scoping
rules/decorators.md        # 2.17 Decorators
rules/threading.md          # 2.18 Threading
rules/power-features.md    # 2.19 Power Features
rules/modern-python.md     # 2.20 Modern Python
rules/type-annotated-code.md  # 2.21 Type Annotated Code

rules/semicolons.md        # 3.1 Semicolons
rules/indentation.md        # 3.2, 3.4 Indentation
rules/parentheses.md       # 3.3 Parentheses
rules/blank-lines.md       # 3.5 Blank Lines
rules/whitespace.md        # 3.6 Whitespace
rules/comments-and-docstrings.md  # 3.8 Comments
rules/strings.md           # 3.10 Strings
rules/files-sockets-closables.md  # 3.11 Files
rules/todo-comments.md     # 3.12 TODO Comments
rules/imports-formatting.md  # 3.13 Imports Formatting
rules/statements.md        # 3.14 Statements
rules/access-control.md    # 3.15 Access Control
rules/naming.md            # 3.16 Naming
rules/main.md              # 3.17 Main
rules/function-length.md   # 3.18 Function Length
rules/type-annotations.md  # 3.19 Type Annotations
```

Each rule file contains:
- Brief explanation of why it matters
- Incorrect code example with explanation
- Correct code example with explanation
- Additional context and references

## Full Compiled Document

For the complete guide with all rules expanded, refer to the original Google Python Style Guide at: https://google.github.io/styleguide/pyguide.html
