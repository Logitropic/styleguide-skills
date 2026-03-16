---
name: google-typescript-styleguide
description: Google TypeScript Style Guide implementation guidelines. This skill should be used when writing, reviewing, or refactoring TypeScript code to ensure compliance with Google TypeScript Style Guide. Triggers on tasks involving TypeScript source files, linting, code reviews, or any TypeScript development work.
license: Apache-2.0
metadata:
  author: google
  version: "1.0.0"
---

# Google TypeScript Style Guide

Comprehensive TypeScript coding guidelines based on Google's TypeScript Style Guide. Covers source file basics, structure, language features, naming, type system, and documentation.

## When to Apply

Reference these guidelines when:
- Writing new TypeScript code
- Reviewing TypeScript code for style and correctness
- Refactoring existing TypeScript code
- Setting up TypeScript projects with linting and type checking
- Teaching TypeScript best practices

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Source File Basics | CRITICAL | `file-` |
| 2 | Imports & Exports | CRITICAL | `import-` |
| 3 | Language Features | HIGH | `feature-` |
| 4 | Classes & Functions | HIGH | `class-` |
| 5 | Naming | HIGH | `naming-` |
| 6 | Type System | HIGH | `type-` |
| 7 | Documentation | MEDIUM | `jsdoc-` |

## Quick Reference

### Source File Basics
- `file-encoding` - UTF-8 encoding and whitespace characters
- `copyright` - Copyright information in JSDoc
- `fileoverview` - @fileoverview JSDoc

### Imports & Exports
- `imports` - ES6 import variants and paths
- `exports` - Named exports, visibility, and mutable exports
- `import-export-type` - Import/export type and modules vs namespaces

### Language Features
- `local-variables` - Use const/let, one variable per declaration
- `array-literals` - Bracket notation, no Array constructor, spread, destructuring
- `object-literals` - No Object constructor, iteration, spread, computed names, destructuring
- `classes` - Declarations, methods, static methods, constructors, members, visibility
- `functions` - Terminology, declarations vs expressions, arrow functions, this, callbacks
- `this` - Usage restricted to classes and explicit this types
- `primitive-literals` - Strings, numbers, type coercion
- `control-structures` - Flow blocks, assignment, iteration, exceptions, switch, equality, assertions
- `decorators` - Restricted to framework decorators
- `disallowed-features` - Wrapper objects, ASI, const enums, debugger, with, eval

### Naming
- `identifiers` - ASCII only, descriptive names, camelCase vs UpperCamelCase
- `identifier-naming` - Rules for specific identifier types (type parameters, constants, etc.)

### Type System
- `type-inference` - Rely on inference for trivial types
- `undefined-and-null` - Use both appropriately, prefer optional fields
- `structural-types` - Use interfaces for structural types
- `interfaces-over-type-aliases` - Prefer interfaces for object types
- `array-type` - T[] sugar vs Array<T>
- `indexable-types` - Index signatures and Maps
- `mapped-conditional-types` - Use simple constructs when possible
- `any-type` - Avoid any, use unknown or specific types
- `empty-interface-type` - Avoid {}, use unknown or Record
- `tuple-types` - Use tuples for pairs/small collections
- `wrapper-types` - Do not use String/Boolean/Number wrapper types
- `return-type-only-generics` - Avoid return-type only generics

### Toolchain & Documentation
- `compiler` - pass type checking, no @ts-ignore
- `conformance` - follow tsetse/tsec rules
- `jsdoc-general-form` - JSDoc vs comments, multi-line style
- `jsdoc-markdown` - Markdown in JSDoc
- `jsdoc-tags` - Standard JSDoc tags
- `jsdoc-line-wrapping` - Indentation for wrapped tags
- `document-exports` - Document top-level exports
- `class-comments` - Class and constructor documentation
- `method-function-comments` - Method, parameter, and return descriptions
- `parameter-property-comments` - Documenting parameter properties
- `jsdoc-type-annotations` - Redundant in TypeScript
- `informative-comments` - Avoid redundant comments, parameter name comments
- `jsdoc-decorators` - JSDoc before decorators
- `deprecation` - @deprecated JSDoc

## Rule Files Index

| Topic | File |
|-------|------|
| File Encoding | `file-encoding.md` |
| Copyright | `copyright.md` |
| Fileoverview | `fileoverview.md` |
| Imports | `imports.md` |
| Exports | `exports.md` |
| Import/Export Type | `import-export-type.md` |
| Local Variables | `local-variables.md` |
| Array Literals | `array-literals.md` |
| Object Literals | `object-literals.md` |
| Classes | `classes.md` |
| Functions | `functions.md` |
| this | `this.md` |
| Interfaces | `interfaces.md` |
| Primitive Literals | `primitive-literals.md` |
| Control Structures | `control-structures.md` |
| Decorators | `decorators.md` |
| Disallowed Features | `disallowed-features.md` |
| Identifiers | `identifiers.md` |
| Identifier Naming | `identifier-naming.md` |
| Type Inference | `type-inference.md` |
| Undefined/Null | `undefined-and-null.md` |
| Structural Types | `structural-types.md` |
| Interfaces over Type Aliases | `interfaces-over-type-aliases.md` |
| Array Type | `array-type.md` |
| Indexable Types | `indexable-types.md` |
| Mapped/Conditional Types | `mapped-conditional-types.md` |
| any Type | `any-type.md` |
| {} Type | `empty-interface-type.md` |
| Tuple Types | `tuple-types.md` |
| Wrapper Types | `wrapper-types.md` |
| Return-type Generics | `return-type-only-generics.md` |
| Compiler | `compiler.md` |
| Conformance | `conformance.md` |
| JSDoc General | `jsdoc-general-form.md` |
| JSDoc Markdown | `jsdoc-markdown.md` |
| JSDoc Tags | `jsdoc-tags.md` |
| JSDoc Line Wrapping | `jsdoc-line-wrapping.md` |
| Document Exports | `document-exports.md` |
| Class Comments | `class-comments.md` |
| Method/Function Comments | `method-function-comments.md` |
| Parameter Property Comments | `parameter-property-comments.md` |
| JSDoc Type Annotations | `jsdoc-type-annotations.md` |
| Informative Comments | `informative-comments.md` |
| JSDoc Decorators | `jsdoc-decorators.md` |
| Deprecation | `deprecation.md` |

## How to Use

Read individual rule files for detailed explanations and code examples:

```
rules/file-encoding.md
rules/copyright.md
rules/fileoverview.md
rules/imports.md
rules/exports.md
rules/import-export-type.md
rules/local-variables.md
rules/array-literals.md
rules/object-literals.md
rules/classes.md
rules/functions.md
rules/this.md
rules/interfaces.md
rules/primitive-literals.md
rules/control-structures.md
rules/decorators.md
rules/disallowed-features.md
rules/identifiers.md
rules/identifier-naming.md
rules/type-inference.md
rules/undefined-and-null.md
rules/structural-types.md
rules/interfaces-over-type-aliases.md
rules/array-type.md
rules/indexable-types.md
rules/mapped-conditional-types.md
rules/any-type.md
rules/empty-interface-type.md
rules/tuple-types.md
rules/wrapper-types.md
rules/return-type-only-generics.md
rules/compiler.md
rules/conformance.md
rules/jsdoc-general-form.md
rules/jsdoc-markdown.md
rules/jsdoc-tags.md
rules/jsdoc-line-wrapping.md
rules/document-exports.md
rules/class-comments.md
rules/method-function-comments.md
rules/parameter-property-comments.md
rules/jsdoc-type-annotations.md
rules/informative-comments.md
rules/jsdoc-decorators.md
rules/deprecation.md
```

## Full Compiled Document

For the complete guide with all rules expanded, refer to the original Google TypeScript Style Guide at: https://google.github.io/styleguide/tsguide.html
