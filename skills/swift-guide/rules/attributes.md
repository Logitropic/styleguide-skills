# Attributes

Parameterized attributes (such as `@availability(...)` or `@objc(...)`) are each
written on their own line immediately before the declaration to which they
apply, are lexicographically ordered, and are indented at the same level as the
declaration.

**GOOD**
```swift
@available(iOS 9.0, *)
public func coolNewFeature() {
  // ...
}
```

**BAD**
```swift
@available(iOS 9.0, *) public func coolNewFeature() {
  // ...
}
```

Attributes without parameters (for example, `@objc` without arguments,
`@IBOutlet`, or `@NSManaged`) are lexicographically ordered and _may_ be placed
on the same line as the declaration if and only if they would fit on that line
without requiring the line to be rewrapped. If placing an attribute on the same
line as the declaration would require a declaration to be wrapped that
previously did not need to be wrapped, then the attribute is placed on its own
line.

**GOOD**
```swift
public class MyViewController: UIViewController {
  @IBOutlet private var tableView: UITableView!
}
```
