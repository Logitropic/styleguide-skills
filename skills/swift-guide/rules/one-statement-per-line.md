# One Statement Per Line

There is **at most** one statement per line, and each statement is followed by a
line break, except when the line ends with a block that also contains zero
or one statements.

**GOOD**
```swift
guard let value = value else { return 0 }

defer { file.close() }

switch someEnum {
case .first: return 5
case .second: return 10
case .third: return 20
}

let squares = numbers.map { $0 * $0 }

var someProperty: Int {
  get { return otherObject.property }
  set { otherObject.property = newValue }
}

var someProperty: Int { return otherObject.somethingElse() }

required init?(coder aDecoder: NSCoder) { fatalError("no coder") }
```

Wrapping the body of a single-statement block onto its own line is always
allowed. Exercise best judgment when deciding whether to place a conditional
statement and its body on the same line. For example, single line conditionals
work well for early-return and basic cleanup tasks, but less so when the body
contains a function call with significant logic. When in doubt, write it as a
multi-line statement.
