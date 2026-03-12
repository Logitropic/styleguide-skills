---
name: google-swift-styleguide
description: Google Swift Style Guide implementation guidelines. This skill should be used when writing, reviewing, or refactoring Swift code to ensure compliance with Google Swift Style Guide. Triggers on tasks involving Swift source files, Swift code reviews, Swift linting, or any Swift development work.
license: Apache-2.0
metadata:
  author: google
  version: "1.1.0"
---

# Google Swift Style Guide

Comprehensive Swift coding guidelines based on Google's Swift Style Guide. Contains rules covering code formatting, naming conventions, programming practices, and documentation.

## When to Apply

Reference these guidelines when:
- Writing new Swift code
- Reviewing Swift code for style and correctness
- Refactoring existing Swift code
- Setting up Swift projects with formatting tools

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Formatting | CRITICAL | `format-` |
| 2 | Naming | HIGH | `name-` |
| 3 | Programming Practices | HIGH | `practice-` |
| 4 | Source File Structure | MEDIUM | `file-` |
| 5 | Documentation | MEDIUM | `doc-` |

## Quick Reference

### Section 1: Source File Basics
- `format-encoding` - UTF-8 encoding (in `source-file-basics.md`)
- `format-whitespace` - U+0020 space only (in `source-file-basics.md`)
- `format-literals` - String literal rules (in `source-file-basics.md`)

### Section 2: Source File Structure
- `file-naming` - File naming conventions (in `file-structure.md`)
- `file-imports` - Import statement grouping (in `imports.md`)
- `file-order` - Logical member order and MARK comments (in `file-structure.md`)

### Section 3: General Formatting
- `format-column-limit` - 100 characters per line (in `column-limit.md`)
- `format-indentation` - 2 spaces, no tabs (in `indentation.md`)
- `format-braces` - K&R style braces (in `braces.md`)
- `format-line-wrapping` - Detailed wrapping rules (in `line-wrapping.md`)
- `format-whitespace` - Horizontal/Vertical rules (in `horizontal-whitespace.md`, `vertical-whitespace.md`)

### Section 4: Programming Practices
- `practice-optionals` - Safe unwrapping and sentinel avoidance (in `optional-types.md`)
- `practice-errors` - Throwing errors vs optionals (in `error-types.md`)
- `practice-guards` - Early exits with guard (in `guard-statements.md`)
- `practice-init` - Initializer naming and usage (in `initializers.md`)

## Rule Files Index

| Section | File | Topic |
|---------|------|-------|
| 1 | `source-file-basics.md` | Encoding, Whitespace, Escape Sequences, Literals |
| 2 | `file-structure.md` | File Naming, Member Order, MARK comments |
| 2 | `imports.md` | Import Statement Grouping and Order |
| 3 | `column-limit.md` | 100 Character Column Limit |
| 3 | `indentation.md` | 2-Space Indentation |
| 3 | `braces.md` | K&R Brace Style, Closures, Empty Blocks |
| 3 | `semicolons.md` | No Semicolons Rule |
| 3 | `one-statement-per-line.md` | One Statement Per Line Rule |
| 3 | `line-wrapping.md` | Detailed Line-Wrapping Indentation (+2) |
| 3 | `horizontal-whitespace.md` | Spaces Around Operators, Colons, Commas |
| 3 | `vertical-whitespace.md` | Blank Lines Between Members |
| 3 | `horizontal-alignment.md` | Forbidding Horizontal Alignment |
| 3 | `parentheses.md` | Parentheses in Control Flow |
| 4 | `comments.md` | File, Documentation, and Non-Doc Comments |
| 4 | `properties.md` | Property Declaration and Counts |
| 4 | `switch-statements.md` | Switch Indentation and Fallthrough |
| 4 | `enum-cases.md` | Case per Line, Indirect, Empty Parens |
| 4 | `trailing-closures.md` | Syntax, Ambiguity, Multiple Closures |
| 4 | `trailing-commas.md` | Required for Multi-line Literals |
| 4 | `numeric-literals.md` | Underscore Digits Grouping |
| 4 | `attributes.md` | Parameterized/Unparameterized Attributes |
| 5 | `naming-conventions.md` | Types, Variables, Enum Cases, Access Control |
| 5 | `delegate-methods.md` | Naming Patterns for Delegates |
| 6 | `compiler-warnings.md` | Clean Compilation Requirement |
| 6 | `initializers.md` | Param Naming, Coercions, Synthesized Init |
| 6 | `shorthand-names.md` | Array, Dict, Optional Shorthand, Void |
| 6 | `optional-types.md` | Sentinels, Nil Comparison, Force Unwrap/Cast |
| 6 | `error-types.md` | Force-Try! Forbidden, Throwing Rules |
| 6 | `access-levels.md` | Extension Levels, Nesting, Namespacing |
| 6 | `guard-statements.md` | Early Exit Rationale and Pyramid of Doom |
| 6 | `loops.md` | for-where Loops |
| 6 | `pattern-matching.md` | Binding Placement, Omitting Labels |
| 6 | `tuple-patterns.md` | Unlabeled Assignment Only |
| 6 | `arithmetic-operators.md` | Trapping vs Masking |
| 6 | `custom-operators.md` | Custom/Overloaded Operator Rules |
| 6 | `playground-literals.md` | Forbidden in Production Code |

## How to Use

Refer to the specific rule file in `rules/` for detailed explanations and examples. For the complete guide, consult the original Google Swift Style Guide.
