# Types with Shorthand Names

Arrays, dictionaries, and optional types are written in their shorthand form
whenever possible; that is, `[Element]`, `[Key: Value]`, and `Wrapped?`. The
long forms `Array<Element>`, `Dictionary<Key, Value>`, and `Optional<Wrapped>`
are only written when required by the compiler; for example, the Swift parser
requires `Array<Element>.Index` and does not accept `[Element].Index`.

**GOOD**
```swift
func enumeratedDictionary<Element>(
  from values: [Element],
  start: Array<Element>.Index? = nil
) -> [Int: Element] {
  // ...
}
```

**BAD**
```swift
func enumeratedDictionary<Element>(
  from values: Array<Element>,
  start: Optional<Array<Element>.Index> = nil
) -> Dictionary<Int, Element> {
  // ...
}
```

`Void` is a `typealias` for the empty tuple `()`, so from an implementation
point of view they are equivalent. In function type declarations (such as
closures, or variables holding a function reference), the return type is always
written as `Void`, never as `()`. In functions declared with the `func` keyword,
the `Void` return type is omitted entirely.

Empty argument lists are always written as `()`, never as `Void`. (In fact,
the function signature `Void -> Result` is an error in Swift because function
arguments must be surrounded by parentheses, and `(Void)` has a different
meaning: an argument list with a single empty-tuple argument.)

**GOOD**
```swift
func doSomething() {
  // ...
}

let callback: () -> Void
```

**BAD**
```swift
func doSomething() -> Void {
  // ...
}

func doSomething2() -> () {
  // ...
}

let callback: () -> ()
```
