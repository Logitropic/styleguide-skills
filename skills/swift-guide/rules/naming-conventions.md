# Naming Conventions

## Naming

### Apple's API Style Guidelines

Apple's
[official Swift naming and API design guidelines](https://swift.org/documentation/api-design-guidelines/)
hosted on swift.org are considered part of this style guide and are followed as
if they were repeated here in their entirety.

### Naming Conventions Are Not Access Control

Restricted access control (`internal`, `fileprivate`, or `private`) is preferred
for the purposes of hiding information from clients, rather than naming
conventions.

Naming conventions (such as prefixing a leading underscore) are only used in
rare situations when a declaration must be given higher visibility than is
otherwise desired in order to work around language limitations&mdash;for
example, a type that has a method that is only intended to be called by other
parts of a library implementation that crosses module boundaries and must
therefore be declared `public`.

### Identifiers

In general, identifiers contain only 7-bit ASCII characters. Unicode identifiers
are allowed if they have a clear and legitimate meaning in the problem domain
of the code base (for example, Greek letters that represent mathematical
concepts) and are well understood by the team who owns the code.

**GOOD**
```swift
let smile = "😊"
let deltaX = newX - previousX
let Δx = newX - previousX
```

**BAD**
```swift
let 😊 = "😊"
```

### Static and Class Properties

Static and class properties that return instances of the declaring type are
_not_ suffixed with the name of the type.

**GOOD**
```swift
public class UIColor {
  public class var red: UIColor {                // GOOD.
    // ...
  }
}

public class URLSession {
  public class var shared: URLSession {          // GOOD.
    // ...
  }
}
```

**AVOID**
```swift
public class UIColor {
  public class var redColor: UIColor {           // AVOID.
    // ...
  }
}

public class URLSession {
  public class var sharedSession: URLSession {   // AVOID.
    // ...
  }
}
```

When a static or class property evaluates to a singleton instance of the
declaring type, the names `shared` and `default` are commonly used. This style
guide does not require specific names for these; the author should choose a name
that makes sense for the type.

### Global Constants

Like other variables, global constants are `lowerCamelCase`. Hungarian notation,
such as a leading `g` or `k`, is not used.

**GOOD**
```swift
let secondsPerMinute = 60
```

**BAD**
```swift
let SecondsPerMinute = 60
let kSecondsPerMinute = 60
let gSecondsPerMinute = 60
let SECONDS_PER_MINUTE = 60
```
