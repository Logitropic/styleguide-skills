# Parentheses

Parentheses are **not** used around the top-most expression that follows an
`if`, `guard`, `while`, or `switch` keyword.

**GOOD**
```swift
if x == 0 {
  print("x is zero")
}

if (x == 0 || y == 1) && z == 2 {
  print("...")
}
```

**BAD**
```swift
if (x == 0) {
  print("x is zero")
}

if ((x == 0 || y == 1) && z == 2) {
  print("...")
}
```

Optional grouping parentheses are omitted only when the author and the reviewer
agree that there is no reasonable chance that the code will be misinterpreted
without them, nor that they would have made the code easier to read. It is _not_
reasonable to assume that every reader has the entire Swift operator precedence
table memorized.
