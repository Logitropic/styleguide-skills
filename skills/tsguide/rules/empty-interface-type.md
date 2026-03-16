### `{}` Type

The `{}` type, also known as an empty interface type, represents a interface with no properties. An empty interface type has no specified properties and therefore any non-nullish value is assignable to it.

```ts
let player: {};

player = {
  health: 50,
}; // Allowed.

console.log(player.health) // Property 'health' does not exist on type '{}'.
```

```ts
function takeAnything(obj:{}) {

}

takeAnything({});
takeAnything({ a: 1, b: 2 });
```

Google3 code **should not** use `{}` for most use cases. `{}` represents any non-nullish primitive or object type, which is rarely appropriate. Prefer one of the following more-descriptive types:

- `unknown` can hold any value, including `null` or `undefined`, and is generally more appropriate for opaque values.
- `Record<string, T>` is better for dictionary-like objects, and provides better type safety by being explicit about the type `T` of contained values (which may itself be `unknown`).
- `object` excludes primitives as well, leaving only non-nullish functions and objects, but without any other assumptions about what properties may be available.
