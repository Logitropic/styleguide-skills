# Agent Skills

A collection of skills for AI coding agents. Skills are packaged instructions and scripts that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

## Available Skills

### pyguide

Google Python Style Guide implementation guidelines. Contains 36 rules across 21 categories, covering both Python Language Rules (Section 2) and Python Style Rules (Section 3).

**Use when:**
- Writing new Python code
- Reviewing Python code for style and correctness
- Refactoring existing Python code
- Setting up Python projects with linting and type checking

**Section 2: Python Language Rules**
- Lint
- Imports & Packages
- Exceptions
- Mutable Global State
- Nested/Local/Inner Classes and Functions
- Comprehensions & Generator Expressions
- Default Iterators and Operators
- Generators
- Lambda Functions
- Conditional Expressions
- Default Argument Values
- Properties
- True/False Evaluations
- Lexical Scoping
- Function and Method Decorators
- Threading
- Power Features
- Modern Python: from __future__ imports
- Type Annotated Code

**Section 3: Python Style Rules**
- Semicolons
- Line length
- Parentheses
- Indentation
- Blank Lines
- Whitespace
- Comments and Docstrings
- Strings
- Files, Sockets, and similar Stateful Resources
- TODO Comments
- Imports formatting
- Statements
- Getters and Setters
- Naming
- Main
- Function length
- Type Annotations

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

## Skill Structure

Each skill contains:
- `SKILLS.md` - Instructions for the agent
- `rules/` - Individual rule files with detailed explanations and examples

## License

Apache-2.0
