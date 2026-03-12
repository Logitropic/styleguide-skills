# Pattern Matching

The `let` and `var` keywords are placed individually in front of _each_ element
in a pattern that is being matched. The shorthand version of `let`/`var` that
precedes and distributes across the entire pattern is forbidden because it can
introduce unexpected behavior if a value being matched in a pattern is itself a
variable.

**GOOD**
```swift
enum DataPoint {
  case unlabeled(Int)
  case labeled(String, Int)
}

let label = "goodbye"

// `label` is treated as a value here because it is not preceded by `let`, so
// the pattern below matches only data points that have the label "goodbye".
switch DataPoint.labeled("hello", 100) {
case .labeled(label, let value):
  // ...
}

// Writing `let` before each individual binding clarifies that the intent is to
// introduce a new binding (shadowing the local variable within the case) rather
// than to match against the value of the local variable. Thus, this pattern
// matches data points with any string label.
switch DataPoint.labeled("hello", 100) {
case .labeled(let label, let value):
  // ...
}
```

In the example below, if the author's intention was to match using the value of
the `label` variable above, that has been lost because `let` distributes across
the entire pattern and thus shadows the variable with a binding that applies to
any string value:

**BAD**
```swift
switch DataPoint.labeled("hello", 100) {
case let .labeled(label, value):
  // ...
}
```

Labels of tuple arguments and `enum` associated values are omitted when binding
a value to a variable with the same name as the label.

**GOOD**
```swift
enum BinaryTree<Element> {
  indirect case subtree(left: BinaryTree<Element>, right: BinaryTree<Element>)
  case leaf(element: Element)
}

switch treeNode {
case .subtree(let left, let right):
  // ...
case .leaf(let element):
  // ...
}
```

Including the labels adds noise that is redundant and lacking useful
information:

**BAD**
```swift
switch treeNode {
case .subtree(left: let left, right: let right):
  // ...
case .leaf(element: let element):
  // ...
}
```
