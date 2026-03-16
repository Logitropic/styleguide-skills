## Comments and documentation

#### JSDoc versus comments

There are two types of comments, JSDoc (`/** ... */`) and non-JSDoc ordinary comments (`// ...` or `/* ... */`).

- Use `/** JSDoc */` comments for documentation, i.e. comments a user of the code should read.
- Use `// line comments` for implementation comments, i.e. comments that only concern the implementation of the code itself.

JSDoc comments are understood by tools (such as editors and documentation generators), while ordinary comments are only for other humans.

#### Multi-line comments

Multi-line comments are indented at the same level as the surrounding code. They *must* use multiple single-line comments (`//`-style), not block comment style (`/* */`).

```ts
// This is
// fine
```

```ts
/*
 * This should
 * use multiple
 * single-line comments
 */

/* This should use // */
```

Comments are not enclosed in boxes drawn with asterisks or other characters.

### JSDoc general form

The basic formatting of JSDoc comments is as seen in this example:

```ts
/**
 * Multiple lines of JSDoc text are written here,
 * wrapped normally.
 * @param arg A number to do something to.
 */
function doSomething(arg: number) { … }
```

or in this single-line example:

```ts
/** This short jsdoc describes the function. */
function doSomething(arg: number) { … }
```

If a single-line comment overflows into multiple lines, it *must* use the multi-line style with `/**` and `*/` on their own lines.

Many tools extract metadata from JSDoc comments to perform code validation and optimization. As such, these comments *must* be well-formed.
