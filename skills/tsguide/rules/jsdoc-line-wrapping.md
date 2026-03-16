### Line wrapping

Line-wrapped block tags are indented four spaces. Wrapped description text *may* be lined up with the description on previous lines, but this horizontal alignment is discouraged.

```ts
/**
 * Illustrates line wrapping for long param/return descriptions.
 * @param foo This is a param with a particularly long description that just
 *     doesn't fit on one line.
 * @return This returns something that has a lengthy description too long to fit
 *     in one line.
 */
exports.method = function(foo) {
  return 5;
};
```

Do not indent when wrapping a `@desc` or `@fileoverview` description.
