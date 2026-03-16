### Make comments that actually add information

For non-exported symbols, sometimes the name and type of the function or parameter is enough. Code will *usually* benefit from more documentation than just variable names though!

- Avoid comments that just restate the parameter name and type, e.g.

```ts
/** @param fooBarService The Bar service for the Foo application. */
```

- Because of this rule, `@param` and `@return` lines are only required when they add information, and *may* otherwise be omitted.

```ts
/**
 * POSTs the request to start coffee brewing.
 * @param amountLitres The amount to brew. Must fit the pot size!
 */
brew(amountLitres: number, logger: Logger) {
  // ...
}
```

#### Comments when calling a function

“Parameter name” comments should be used whenever the method name and parameter value do not sufficiently convey the meaning of the parameter.

Before adding these comments, consider refactoring the method to instead accept an interface and destructure it to greatly improve call-site readability.

"Parameter name" comments go before the parameter value, and include the parameter name and a `=` suffix:

```ts
someFunction(obviousParam, /* shouldRender= */ true, /* name= */ 'hello');
```

Existing code may use a legacy parameter name comment style, which places these comments ~after~ the parameter value and omits the `=`. Continuing to use this style within the file for consistency is acceptable.

```ts
someFunction(obviousParam, true /* shouldRender */, 'hello' /* name */);
```
