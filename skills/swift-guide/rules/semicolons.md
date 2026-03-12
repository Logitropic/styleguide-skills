# Semicolons

Semicolons (`;`) are **not used**, either to terminate or separate statements.

In other words, the only location where a semicolon may appear is inside a
string literal or a comment.

**GOOD**
```swift
func printSum(_ a: Int, _ b: Int) {
  let sum = a + b
  print(sum)
}
```

**BAD**
```swift
func printSum(_ a: Int, _ b: Int) {
  let sum = a + b;
  print(sum);
}
```
