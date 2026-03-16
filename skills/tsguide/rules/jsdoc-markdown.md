### Markdown

JSDoc is written in Markdown, though it *may* include HTML when necessary.

This means that tooling parsing JSDoc will ignore plain text formatting, so if you did this:

```ts
/**
 * Computes weight based on three factors:
 *   items sent
 *   items received
 *   last timestamp
 */
```

it will be rendered like this:

```
Computes weight based on three factors: items sent items received last timestamp
```

Instead, write a Markdown list:

```ts
/**
 * Computes weight based on three factors:
 *
 * - items sent
 * - items received
 * - last timestamp
 */
```
