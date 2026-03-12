# Trailing Commas

Trailing commas in array and dictionary literals are _required_ when each
element is placed on its own line. Doing so produces cleaner diffs when items
are added to those literals later.

**GOOD**
```swift
let configurationKeys = [
  "bufferSize",
  "compression",
  "encoding",                                    // GOOD.
]
```

**AVOID**
```swift
let configurationKeys = [
  "bufferSize",
  "compression",
  "encoding"                                     // AVOID.
]
```
