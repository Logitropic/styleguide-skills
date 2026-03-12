# Playground Literals

The graphically-rendered playground literals `#colorLiteral(...)`,
`#imageLiteral(...)`, and `#fileLiteral(...)` are forbidden in non-playground
production code. They are permitted in playground sources.

**GOOD**
```swift
let color = UIColor(red: 1.0, green: 1.0, blue: 1.0, alpha: 1.0)
```

**BAD**
```swift
let color = #colorLiteral(red: 1.0, green: 1.0, blue: 1.0, alpha: 1.0)
```
