# Trailing Closures

Functions should not be overloaded such that two overloads differ _only_ by the
name of their trailing closure argument. Doing so prevents using trailing
closure syntax&mdash;when the label is not present, a call to the function with
a trailing closure is ambiguous.

Consider the following example, which prohibits using trailing closure syntax to
call `greet`:

**BAD**
```swift
func greet(enthusiastically nameProvider: () -> String) {
  print("Hello, \(nameProvider())! It's a pleasure to see you!")
}

func greet(apathetically nameProvider: () -> String) {
  print("Oh, look. It's \(nameProvider()).")
}

greet { "John" }  // error: ambiguous use of 'greet'
```

This example is fixed by differentiating some part of the function name other
than the closure argument&mdash;in this case, the base name:

**GOOD**
```swift
func greetEnthusiastically(_ nameProvider: () -> String) {
  print("Hello, \(nameProvider())! It's a pleasure to see you!")
}

func greetApathetically(_ nameProvider: () -> String) {
  print("Oh, look. It's \(nameProvider()).")
}

greetEnthusiastically { "John" }
greetApathetically { "not John" }
```

If a function call has multiple closure arguments, then _none_ are called using
trailing closure syntax; _all_ are labeled and nested inside the argument
list's parentheses.

**GOOD**
```swift
UIView.animate(
  withDuration: 0.5,
  animations: {
    // ...
  },
  completion: { finished in
    // ...
  })
```

**BAD**
```swift
UIView.animate(
  withDuration: 0.5,
  animations: {
    // ...
  }) { finished in
    // ...
  }
```

If a function has a single closure argument and it is the final argument, then
it is _always_ called using trailing closure syntax, except in the following
cases to resolve ambiguity or parsing errors:

1. As described above, labeled closure arguments must be used to disambiguate
   between two overloads with otherwise identical arguments lists.
1. Labeled closure arguments must be used in control flow statements where the
   body of the trailing closure would be parsed as the body of the control flow
   statement.

**GOOD**
```swift
Timer.scheduledTimer(timeInterval: 30, repeats: false) { timer in
  print("Timer done!")
}

if let firstActive = list.first(where: { $0.isActive }) {
  process(firstActive)
}
```

**BAD**
```swift
Timer.scheduledTimer(timeInterval: 30, repeats: false, block: { timer in
  print("Timer done!")
})

// This example fails to compile.
if let firstActive = list.first { $0.isActive } {
  process(firstActive)
}
```

When a function called with trailing closure syntax takes no other arguments,
empty parentheses (`()`) after the function name are _never_ present.

**GOOD**
```swift
let squares = [1, 2, 3].map { $0 * $0 }
```

**BAD**
```swift
let squares = [1, 2, 3].map({ $0 * $0 })
let squares = [1, 2, 3].map() { $0 * $0 }
```
