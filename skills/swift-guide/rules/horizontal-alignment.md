# Horizontal Alignment

> **Terminology note:** _Horizontal alignment_ is the practice of adding a
> variable number of additional spaces in your code with the goal of making
> certain tokens appear directly below certain other tokens on previous lines.

Horizontal alignment is forbidden except when writing obviously tabular data
where omitting the alignment would be harmful to readability. In other cases
(for example, lining up the types of stored property declarations in a `struct`
or `class`), horizontal alignment is an invitation for maintenance problems if a
new member is introduced that requires every other member to be realigned.

**GOOD**
```swift
struct DataPoint {
  var value: Int
  var primaryColor: UIColor
}
```

**BAD**
```swift
struct DataPoint {
  var value:        Int
  var primaryColor: UIColor
}
```
