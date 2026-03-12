# `guard`s for Early Exits

A `guard` statement, compared to an `if` statement with an inverted condition,
provides visual emphasis that the condition being tested is a special case that
causes early exit from the enclosing scope.

Furthermore, `guard` statements improve readability by eliminating extra levels
of nesting (the "pyramid of doom"); failure conditions are closely coupled to
the conditions that trigger them and the main logic remains flush left within
its scope.

This can be seen in the following examples; in the first, there is a clear
progression that checks for invalid states and exits, then executes the main
logic in the successful case. In the second example without `guard`, the main
logic is buried at an arbitrary nesting level and the thrown errors are
separated from their conditions by a great distance.

**GOOD**
```swift
func discombobulate(_ values: [Int]) throws -> Int {
  guard let first = values.first else {
    throw DiscombobulationError.arrayWasEmpty
  }
  guard first >= 0 else {
    throw DiscombobulationError.negativeEnergy
  }

  var result = 0
  for value in values {
    result += invertedCombobulatoryFactory(of: value)
  }
  return result
}
```

**BAD**
```swift
func discombobulate(_ values: [Int]) throws -> Int {
  if let first = values.first {
    if first >= 0 {
      var result = 0
      for value in values {
        result += invertedCombobulatoryFactor(of: value)
      }
      return result
    } else {
      throw DiscombobulationError.negativeEnergy
    }
  } else {
    throw DiscombobulationError.arrayWasEmpty
  }
}
```

A `guard`-`continue` statement can also be useful in a loop to avoid increased
indentation when the entire body of the loop should only be executed in some
cases (but see also the `for`-`where` discussion below.)
