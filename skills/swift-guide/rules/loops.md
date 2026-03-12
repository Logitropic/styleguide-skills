# `for`-`where` Loops

When the entirety of a `for` loop's body would be a single `if` block testing a
condition of the element, the test is placed in the `where` clause of the `for`
statement instead.

**GOOD**
```swift
for item in collection where item.hasProperty {
  // ...
}
```

**BAD**
```swift
for item in collection {
  if item.hasProperty {
    // ...
  }
}
```
