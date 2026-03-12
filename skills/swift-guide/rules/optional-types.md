# Optional Types

Sentinel values are avoided when designing algorithms (for example, an "index"
of &minus;1 when an element was not found in a collection). Sentinel values can
easily and accidentally propagate through other layers of logic because the type
system cannot distinguish between them and valid outcomes.

`Optional` is used to convey a non-error result that is either a value or the
absence of a value. For example, when searching a collection for a value, not
finding the value is still a **valid and expected** outcome, not an error.

**GOOD**
```swift
func index(of thing: Thing, in things: [Thing]) -> Int? {
  // ...
}

if let index = index(of: thing, in: lotsOfThings) {
  // Found it.
} else {
  // Didn't find it.
}
```

**BAD**
```swift
func index(of thing: Thing, in things: [Thing]) -> Int {
  // ...
}

let index = index(of: thing, in: lotsOfThings)
if index != -1 {
  // Found it.
} else {
  // Didn't find it.
}
```

`Optional` is also used for error scenarios when there is a single, obvious
failure state; that is, when an operation may fail for a single domain-specific
reason that is clear to the client. (The domain-specific restriction is meant to
exclude severe errors that are typically out of the user's control to properly
handle, such as out-of-memory errors.)

For example, converting a string to an integer would fail if the
string does not represent a valid integer that fits into the type's bit width:

**GOOD**
```swift
struct Int17 {
  init?(_ string: String) {
    // ...
  }
}
```

Conditional statements that test that an `Optional` is non-`nil` but do not
access the wrapped value are written as comparisons to `nil`. The following
example is clear about the programmer's intent:

**GOOD**
```swift
if value != nil {
  print("value was not nil")
}
```

This example, while taking advantage of Swift's pattern matching and binding
syntax, obfuscates the intent by appearing to unwrap the value and then
immediately throw it away.

**BAD**
```swift
if let _ = value {
  print("value was not nil")
}
```

### Force Unwrapping and Force Casts

Force-unwrapping and force-casting are often code smells and are strongly
discouraged. Unless it is extremely clear from surrounding code why such an
operation is safe, a comment should be present that describes the invariant that
ensures that the operation is safe. For example,

**GOOD**
```swift
let value = getSomeInteger()

// ...intervening code...

// This force-unwrap is safe because `value` is guaranteed to fall within the
// valid enum cases because it came from some data source that only permits
// those raw values.
return SomeEnum(rawValue: value)!
```

> **Exception:** Force-unwraps are allowed in unit tests and test-only code
> without additional documentation. This keeps such code free of unnecessary
> control flow. In the event that `nil` is unwrapped or a cast operation is to
> an incompatible type, the test will fail which is the desired result.

### Implicitly Unwrapped Optionals

Implicitly unwrapped optionals are inherently unsafe and should be avoided
whenever possible in favor of non-optional declarations or regular `Optional`
types. Exceptions are described below.

User-interface objects whose lifetimes are based on the UI lifecycle instead of
being strictly based on the lifetime of the owning object are allowed to use
implicitly unwrapped optionals. Examples of these include `@IBOutlet`
properties connected to objects in a XIB file or storyboard, properties that are
initialized externally like in the `prepareForSegue` implementation of a calling
view controller, and properties that are initialized elsewhere during a class's
life cycle, like views in a view controller's `viewDidLoad` method. Making such
properties regular optionals can put too much burden on the user to unwrap them
because they are guaranteed to be non-nil and remain that way once the objects
are ready for use.

**GOOD**
```swift
class SomeViewController: UIViewController {
  @IBOutlet var button: UIButton!

  override func viewDidLoad() {
    populateLabel(for: button)
  }

  private func populateLabel(for button: UIButton) {
    // ...
  }
}
```

Implicitly unwrapped optionals can also surface in Swift code when using
Objective-C APIs that lack the appropriate nullability attributes. If possible,
coordinate with the owners of that code to add those annotations so that the
APIs are imported cleanly into Swift. If this is not possible, try to keep the
footprint of those implicitly unwrapped optionals as small as possible in your
Swift code; that is, do not propagate them through multiple layers of your own
abstractions.

Implicitly unwrapped optionals are also allowed in unit tests. This is for
reasons similar to the UI object scenario above&mdash;the lifetime of test
fixtures often begins not in the test's initializer but in the `setUp()` method
of a test so that they can be reset before the execution of each test.
