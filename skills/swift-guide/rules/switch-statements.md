# Switch Statements

Case statements are indented at the _same_ level as the switch statement to
which they belong; the statements inside the case blocks are then indented +2
spaces from that level.

**GOOD**
```swift
switch order {
case .ascending:
  print("Ascending")
case .descending:
  print("Descending")
case .same:
  print("Same")
}
```

**BAD**
```swift
switch order {
  case .ascending:
    print("Ascending")
  case .descending:
    print("Descending")
  case .same:
    print("Same")
}
```

**BAD**
```swift
switch order {
case .ascending:
print("Ascending")
case .descending:
print("Descending")
case .same:
print("Same")
}
```

### `fallthrough` in `switch` Statements

When multiple `case`s of a `switch` would execute the same statements, the
`case` patterns are combined into ranges or comma-delimited lists. Multiple
`case` statements that do nothing but `fallthrough` to a `case` below are not
allowed.

**GOOD**
```swift
switch value {
case 1: print("one")
case 2...4: print("two to four")
case 5, 7: print("five or seven")
default: break
}
```

**BAD**
```swift
switch value {
case 1: print("one")
case 2: fallthrough
case 3: fallthrough
case 4: print("two to four")
case 5: fallthrough
case 7: print("five or seven")
default: break
}
```

In other words, there is never a `case` whose body contains _only_ the
`fallthrough` statement. Cases containing _additional_ statements which then
fallthrough to the next case are permitted.
