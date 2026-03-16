### Import and export type

#### Import type

You may use `import type {...}` when you use the imported symbol only as a type. Use regular imports for values:

```ts
import type {Foo} from './foo';
import {Bar} from './foo';

import {type Foo, Bar} from './foo';
```

Why?

The TypeScript compiler automatically handles the distinction and does not insert runtime loads for type references. So why annotate type imports?

The TypeScript compiler can run in 2 modes:

- In development mode, we typically want quick iteration loops. The compiler transpiles to JavaScript without full type information. This is much faster, but requires `import type` in certain cases.
- In production mode, we want correctness. The compiler type checks everything and ensures `import type` is used correctly.

Note: If you need to force a runtime load for side effects, use `import '...';`. See

#### Export type

Use `export type` when re-exporting a type, e.g.:

```ts
export type {AnInterface} from './foo';
```

Why?

`export type` is useful to allow type re-exports in file-by-file transpilation. See `isolatedModules` docs.

`export type` might also seem useful to avoid ever exporting a value symbol for an API. However it does not give guarantees, either: downstream code might still import an API through a different path. A better way to split & guarantee type vs value usages of an API is to actually split the symbols into e.g. `UserService` and `AjaxUserService`. This is less error prone and also better communicates intent.

#### Use modules not namespaces

TypeScript supports two methods to organize code: *namespaces* and *modules*, but namespaces are disallowed. That is, your code *must* refer to code in other files using imports and exports of the form `import {foo} from 'bar';`

Your code *must not* use the `namespace Foo { ... }` construct. `namespace`s *may* only be used when required to interface with external, third party code. To semantically namespace your code, use separate files.

Code *must not* use `require` (as in `import x = require('...');`) for imports. Use ES6 module syntax.

```ts
// Bad: do not use namespaces:
namespace Rocket {
  function launch() { ... }
}

// Bad: do not use <reference>
/// <reference path="..."/>

// Bad: do not use require()
import x = require('mydep');
```

> NB: TypeScript `namespace`s used to be called internal modules and used to use the `module` keyword in the form `module Foo { ... }`. Don't use that either. Always use ES6 imports.
