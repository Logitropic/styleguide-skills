# Properties

Local variables are declared close to the point at which they are first used
(within reason) to minimize their scope.

With the exception of tuple destructuring, every `let` or `var` statement
(whether a property or a local variable) declares exactly one variable.

**GOOD**
```swift
var a = 5
var b = 10

let (quotient, remainder) = divide(100, 9)
```

**BAD**
```swift
var a = 5, b = 10
```

### Properties (from Programming Practices)

The `get` block for a read-only computed property is omitted and its body is
directly nested inside the property declaration.

**GOOD**
```swift
var totalCost: Int {
  return items.sum { $0.cost }
}
```

**BAD**
```swift
var totalCost: Int {
  get {
    return items.sum { $0.cost }
  }
}
```
