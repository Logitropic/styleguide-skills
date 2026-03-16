### Classes

#### Class declarations

Class declarations *must not* be terminated with semicolons:

```ts
class Foo {
}
```

```ts
class Foo {
}; // Unnecessary semicolon
```

In contrast, statements that contain class expressions *must* be terminated with a semicolon:

```ts
export const Baz = class extends Bar {
  method(): number {
    return this.x;
  }
}; // Semicolon here as this is a statement, not a declaration
```

```ts
exports const Baz = class extends Bar {
  method(): number {
    return this.x;
  }
}
```

It is neither encouraged nor discouraged to have blank lines separating class declaration braces from other class content:

```ts
// No spaces around braces - fine.
class Baz {
  method(): number {
    return this.x;
  }
}

// A single space around both braces - also fine.
class Foo {

  method(): number {
    return this.x;
  }

}
```

#### Class method declarations

Class method declarations *must not* use a semicolon to separate individual method declarations:

```ts
class Foo {
  doThing() {
    console.log("A");
  }
}
```

```ts
class Foo {
  doThing() {
    console.log("A");
  }; // <-- unnecessary
}
```

Method declarations should be separated from surrounding code by a single blank line:

```ts
class Foo {
  doThing() {
    console.log("A");
  }

  getOtherThing(): number {
    return 4;
  }
}
```

```ts
class Foo {
  doThing() {
    console.log("A");
  }
  getOtherThing(): number {
    return 4;
  }
}
```

##### Overriding toString

The `toString` method may be overridden, but must always succeed and never have visible side effects.

Tip: Beware, in particular, of calling other methods from toString, since exceptional conditions could lead to infinite loops.

#### Static methods

##### Avoid private static methods

Where it does not interfere with readability, prefer module-local functions over private static methods.

##### Do not rely on dynamic dispatch

Code *should not* rely on dynamic dispatch of static methods. Static methods *should* only be called on the base class itself (which defines it directly). Static methods *should not* be called on variables containing a dynamic instance that may be either the constructor or a subclass constructor (and *must* be defined with `@nocollapse` if this is done), and *must not* be called directly on a subclass that doesn’t define the method itself.

Disallowed:

```ts
// Context for the examples below (this class is okay by itself)
class Base {
  /** @nocollapse */ static foo() {}
}
class Sub extends Base {}

// Discouraged: don't call static methods dynamically
function callFoo(cls: typeof Base) {
  cls.foo();
}

// Disallowed: don't call static methods on subclasses that don't define it themselves
Sub.foo();

// Disallowed: don't access this in static methods.
class MyClass {
  static foo() {
    return this.staticField;
  }
}
MyClass.staticField = 1;
```

##### Avoid static `this` references

Code *must not* use `this` in a static context.

JavaScript allows accessing static fields through `this`. Different from other languages, static fields are also inherited.

```ts
class ShoeStore {
  static storage: Storage = ...;

  static isAvailable(s: Shoe) {
    // Bad: do not use `this` in a static method.
    return this.storage.has(s.id);
  }
}

class EmptyShoeStore extends ShoeStore {
  static storage: Storage = EMPTY_STORE;  // overrides storage from ShoeStore
}
```

Why?

This code is generally surprising: authors might not expect that static fields can be accessed through the this pointer, and might be surprised to find that they can be overridden - this feature is not commonly used.

This code also encourages an anti-pattern of having substantial static state, which causes problems with testability.

#### Constructors

Constructor calls *must* use parentheses, even when no arguments are passed:

```ts
const x = new Foo;
```

```ts
const x = new Foo();
```

Omitting parentheses can lead to subtle mistakes. These two lines are not equivalent:

```js
new Foo().Bar();
new Foo.Bar();
```

It is unnecessary to provide an empty constructor or one that simply delegates into its parent class because ES2015 provides a default class constructor if one is not specified. However constructors with parameter properties, visibility modifiers or parameter decorators *should not* be omitted even if the body of the constructor is empty.

```ts
class UnnecessaryConstructor {
  constructor() {}
}
```

```ts
class UnnecessaryConstructorOverride extends Base {
    constructor(value: number) {
      super(value);
    }
}
```

```ts
class DefaultConstructor {
}

class ParameterProperties {
  constructor(private myService) {}
}

class ParameterDecorators {
  constructor(@SideEffectDecorator myService) {}
}

class NoInstantiation {
  private constructor() {}
}
```

The constructor should be separated from surrounding code both above and below by a single blank line:

```ts
class Foo {
  myField = 10;

  constructor(private readonly ctorParam) {}

  doThing() {
    console.log(ctorParam.getThing() + myField);
  }
}
```

```ts
class Foo {
  myField = 10;
  constructor(private readonly ctorParam) {}
  doThing() {
    console.log(ctorParam.getThing() + myField);
  }
}
```

#### Class members

##### No #private fields

Do not use private fields (also known as private identifiers):

```ts
class Clazz {
  #ident = 1;
}
```

Instead, use TypeScript's visibility annotations:

```ts
class Clazz {
  private ident = 1;
}
```

Why?

Private identifiers cause substantial emit size and performance regressions when down-leveled by TypeScript, and are unsupported before ES2015. They can only be downleveled to ES2015, not lower. At the same time, they do not offer substantial benefits when static type checking is used to enforce visibility.

##### Use readonly

Mark properties that are never reassigned outside of the constructor with the `readonly` modifier (these need not be deeply immutable).

##### Parameter properties

Rather than plumbing an obvious initializer through to a class member, use a TypeScript parameter property.

```ts
class Foo {
  private readonly barService: BarService;

  constructor(barService: BarService) {
    this.barService = barService;
  }
}
```

```ts
class Foo {
  constructor(private readonly barService: BarService) {}
}
```

If the parameter property needs documentation, use an `@param` JSDoc tag.

##### Field initializers

If a class member is not a parameter, initialize it where it's declared, which sometimes lets you drop the constructor entirely.

```ts
class Foo {
  private readonly userList: string[];

  constructor() {
    this.userList = [];
  }
}
```

```ts
class Foo {
  private readonly userList: string[] = [];
}
```

Tip: Properties should never be added to or removed from an instance after the constructor is finished, since it significantly hinders VMs’ ability to optimize classes' "shape". Optional fields that may be filled in later should be explicitly initialized to `undefined` to prevent later shape changes.

##### Properties used outside of class lexical scope

Properties used from outside the lexical scope of their containing class, such as an Angular component's properties used from a template, *must not* use `private` visibility, as they are used outside of the lexical scope of their containing class.

Use either `protected` or `public` as appropriate to the property in question. Angular and AngularJS template properties should use `protected`, but Polymer should use `public`.

TypeScript code *must not* use `obj['foo']` to bypass the visibility of a property.

Why?

When a property is `private`, you are declaring to both automated systems and humans that the property accesses are scoped to the methods of the declaring class, and they will rely on that. For example, a check for unused code will flag a private property that appears to be unused, even if some other file manages to bypass the visibility restriction.

Though it might appear that `obj['foo']` can bypass visibility in the TypeScript compiler, this pattern can be broken by rearranging the build rules, and also violates optimization compatibility.

##### Getters and setters

Getters and setters, also known as accessors, for class members *may* be used. The getter method *must* be a pure function (i.e., result is consistent and has no side effects: getters *must not* change observable state). They are also useful as a means of restricting the visibility of internal or verbose implementation details (shown below).

```ts
class Foo {
  constructor(private readonly someService: SomeService) {}

  get someMember(): string {
    return this.someService.someVariable;
  }

  set someMember(newValue: string) {
    this.someService.someVariable = newValue;
  }
}
```

```ts
class Foo {
  nextId = 0;
  get next() {
    return this.nextId++; // Bad: getter changes observable state
  }
}
```

If an accessor is used to hide a class property, the hidden property *may* be prefixed or suffixed with any whole word, like `internal` or `wrapped`. When using these private properties, access the value through the accessor whenever possible. At least one accessor for a property *must* be non-trivial: do not define "pass-through" accessors only for the purpose of hiding a property. Instead, make the property public (or consider making it `readonly` rather than just defining a getter with no setter).

```ts
class Foo {
  private wrappedBar = '';
  get bar() {
    return this.wrappedBar || 'bar';
  }

  set bar(wrapped: string) {
    this.wrappedBar = wrapped.trim();
  }
}
```

```ts
class Bar {
  private barInternal = '';
  // Neither of these accessors have logic, so just make bar public.
  get bar() {
    return this.barInternal;
  }

  set bar(value: string) {
    this.barInternal = value;
  }
}
```

Getters and setters *must not* be defined using `Object.defineProperty`, since this interferes with property renaming.

##### Computed properties

Computed properties may only be used in classes when the property is a symbol. Dict-style properties (that is, quoted or computed non-symbol keys) are not allowed (see rationale for not mixing key types. A `[Symbol.iterator]` method should be defined for any classes that are logically iterable. Beyond this, `Symbol` should be used sparingly.

Tip: be careful of using any other built-in symbols (e.g. `Symbol.isConcatSpreadable`) as they are not polyfilled by the compiler and will therefore not work in older browsers.

#### Visibility

Restricting visibility of properties, methods, and entire types helps with keeping code decoupled.

- Limit symbol visibility as much as possible.
- Consider converting private methods to non-exported functions within the same file but outside of any class, and moving private properties into a separate, non-exported class.
- TypeScript symbols are public by default. Never use the `public` modifier except when declaring non-readonly public parameter properties (in constructors).

```ts
class Foo {
  public bar = new Bar();  // BAD: public modifier not needed

  constructor(public readonly baz: Baz) {}  // BAD: readonly implies it's a property which defaults to public
}
```

```ts
class Foo {
  bar = new Bar();  // GOOD: public modifier not needed

  constructor(public baz: Baz) {}  // public modifier allowed
}
```

See also export visibility.

#### Disallowed class patterns

##### Do not manipulate `prototype`s directly

The `class` keyword allows clearer and more readable class definitions than defining `prototype` properties. Ordinary implementation code has no business manipulating these objects. Mixins and modifying the prototypes of builtin objects are explicitly forbidden.

**Exception**: Framework code (such as Polymer, or Angular) may need to use `prototype`s, and should not resort to even-worse workarounds to avoid doing so.
