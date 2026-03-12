# Enum Cases

In general, there is only one `case` per line in an `enum`. The comma-delimited
form may be used only when none of the cases have associated values or raw
values, all cases fit on a single line, and the cases do not need further
documentation because their meanings are obvious from their names.

**GOOD**
```swift
public enum Token {
  case comma
  case semicolon
  case identifier
}

public enum Token {
  case comma, semicolon, identifier
}

public enum Token {
  case comma
  case semicolon
  case identifier(String)
}
```

**BAD**
```swift
public enum Token {
  case comma, semicolon, identifier(String)
}
```

When all cases of an `enum` must be `indirect`, the `enum` itself is declared
`indirect` and the keyword is omitted on the individual cases.

**GOOD**
```swift
public indirect enum DependencyGraphNode {
  case userDefined(dependencies: [DependencyGraphNode])
  case synthesized(dependencies: [DependencyGraphNode])
}
```

**BAD**
```swift
public enum DependencyGraphNode {
  indirect case userDefined(dependencies: [DependencyGraphNode])
  indirect case synthesized(dependencies: [DependencyGraphNode])
}
```

When an `enum` case does not have associated values, empty parentheses are never
present.

**GOOD**
```swift
public enum BinaryTree<Element> {
  indirect case node(element: Element, left: BinaryTree, right: BinaryTree)
  case empty  // GOOD.
}
```

**AVOID**
```swift
public enum BinaryTree<Element> {
  indirect case node(element: Element, left: BinaryTree, right: BinaryTree)
  case empty()  // AVOID.
}
```

The cases of an enum must follow a logical ordering that the author could
explain if asked. If there is no obviously logical ordering, use a
lexicographical ordering based on the cases' names.

In the following example, the cases are arranged in numerical order based on the
underlying HTTP status code and blank lines are used to separate groups.

**GOOD**
```swift
public enum HTTPStatus: Int {
  case ok = 200

  case badRequest = 400
  case notAuthorized = 401
  case paymentRequired = 402
  case forbidden = 403
  case notFound = 404

  case internalServerError = 500
}
```

The following version of the same enum is less readable. Although the cases are
ordered lexicographically, the meaningful groupings of related values has been
lost.

**BAD**
```swift
public enum HTTPStatus: Int {
  case badRequest = 400
  case forbidden = 403
  case internalServerError = 500
  case notAuthorized = 401
  case notFound = 404
  case ok = 200
  case paymentRequired = 402
}
```
