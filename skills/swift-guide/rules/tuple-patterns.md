# Tuple Patterns

Assigning variables through a tuple pattern (sometimes referred to as a _tuple
shuffle_) is only permitted if the left-hand side of the assignment is
unlabeled.

**GOOD**
```swift
let (a, b) = (y: 4, x: 5.0)
```

**BAD**
```swift
let (x: a, y: b) = (y: 4, x: 5.0)
```

Labels on the left-hand side closely resemble type annotations, and can lead to
confusing code.

**BAD**
```swift
// This declares two variables, `Int`, which is a `Double` with value 5.0, and
// `Double`, which is an `Int` with value 4.
// `x` and `y` are not variables.
let (x: Int, y: Double) = (y: 4, x: 5.0)
```
