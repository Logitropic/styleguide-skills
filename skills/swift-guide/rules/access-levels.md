# Access Control and Namespacing

### Access Levels

Omitting an explicit access level is permitted on declarations. For top-level
declarations, the default access level is `internal`. For nested declarations,
the default access level is the lesser of `internal` and the access level of the
enclosing declaration.

Specifying an explicit access level at the file level on an extension is
forbidden. Each member of the extension has its access level specified if it is
different than the default.

**GOOD**
```swift
extension String {
  public var isUppercase: Bool {
    // ...
  }

  public var isLowercase: Bool {
    // ...
  }
}
```

**BAD**
```swift
public extension String {
  var isUppercase: Bool {
    // ...
  }

  var isLowercase: Bool {
    // ...
  }
}
```

### Nesting and Namespacing

Swift allows `enum`s, `struct`s, and `class`es to be nested, so nesting is
preferred (instead of naming conventions) to express scoped and hierarchical
relationships among types when possible. For example, flag `enum`s or error
types that are associated with a specific type are nested in that type.

**GOOD**
```swift
class Parser {
  enum Error: Swift.Error {
    case invalidToken(String)
    case unexpectedEOF
  }

  func parse(text: String) throws {
    // ...
  }
}
```

**BAD**
```swift
class Parser {
  func parse(text: String) throws {
    // ...
  }
}

enum ParseError: Error {
  case invalidToken(String)
  case unexpectedEOF
}
```

Swift does not currently allow protocols to be nested in other types or vice
versa, so this rule does not apply to situations such as the relationship
between a controller class and its delegate protocol.

Declaring an `enum` without cases is the canonical way to define a "namespace"
to group a set of related declarations, such as constants or helper functions.
This `enum` automatically has no instances and does not require that extra
boilerplate code be written to prevent instantiation.

**GOOD**
```swift
enum Dimensions {
  static let tileMargin: CGFloat = 8
  static let tilePadding: CGFloat = 4
  static let tileContentSize: CGSize(width: 80, height: 64)
}
```

**BAD**
```swift
struct Dimensions {
  private init() {}

  static let tileMargin: CGFloat = 8
  static let tilePadding: CGFloat = 4
  static let tileContentSize: CGSize(width: 80, height: 64)
}
```
