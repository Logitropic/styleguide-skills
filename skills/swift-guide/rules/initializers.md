# Initializers

### Initializers (from Naming)

For clarity, initializer arguments that correspond directly to a stored property
have the same name as the property. Explicit `self.` is used during assignment
to disambiguate them.

**GOOD**
```swift
public struct Person {
  public let name: String
  public let phoneNumber: String

  // GOOD.
  public init(name: String, phoneNumber: String) {
    self.name = name
    self.phoneNumber = phoneNumber
  }
}
```

**AVOID**
```swift
public struct Person {
  public let name: String
  public let phoneNumber: String

  // AVOID.
  public init(name otherName: String, phoneNumber otherPhoneNumber: String) {
    name = otherName
    phoneNumber = otherPhoneNumber
  }
}
```

### Initializers (from Programming Practices)

For `struct`s, Swift synthesizes a non-public memberwise `init` that takes
arguments for `var` properties and for any `let` properties that lack default
values. When that initializer is suitable (that is, a `public` one is not
needed), it is used and no explicit initializer is written.

The initializers declared by the special `ExpressibleBy*Literal` compiler
protocols are never called directly.

**GOOD**
```swift
struct Kilometers: ExpressibleByIntegerLiteral {
  init(integerLiteral value: Int) {
    // ...
  }
}

let k1: Kilometers = 10                          // GOOD.
let k2 = 10 as Kilometers                        // ALSO GOOD.
```

**AVOID**
```swift
struct Kilometers: ExpressibleByIntegerLiteral {
  init(integerLiteral value: Int) {
    // ...
  }
}

let k = Kilometers(integerLiteral: 10)           // AVOID.
```

Explicitly calling `.init(...)` is allowed only when the receiver of the call is
a metatype variable. In direct calls to the initializer using the literal type
name, `.init` is omitted. (**Referring** to the initializer directly by using
`MyType.init` syntax to convert it to a closure is permitted.)

**GOOD**
```swift
let x = MyType(arguments)

let type = lookupType(context)
let x = type.init(arguments)

let x = makeValue(factory: MyType.init)
```

**BAD**
```swift
let x = MyType.init(arguments)
```
