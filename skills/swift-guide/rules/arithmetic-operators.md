# Trapping vs. Overflowing Arithmetic

The standard (trapping-on-overflow) arithmetic and bitwise operators (`+`, `-`,
`*`, `<<`, and `>>`) are used for most normal operations, rather than the
masking operations (preceded by `&`). Trapping on overflow is safer because it
prevents bad data from propagating through other layers of the system.

**GOOD**
```swift
// GOOD. Overflow will not cause the balance to go negative.
let newBankBalance = oldBankBalance + recentHugeProfit
```

**AVOID**
```swift
// AVOID. Overflow will cause the balance to go negative if the summands are
// large.
let newBankBalance = oldBankBalance &+ recentHugeProfit
```

Masking operations are comparatively rare but are permitted (and in fact
necessary for correctness) in problem domains that use modular arithmetic, such
as cryptography, big-integer implementations, hash functions, and so forth.

**GOOD**
```swift
var hashValue: Int {
  // GOOD. What matters here is the distribution of the bit pattern rather than
  // the actual numeric value.
  return foo.hashValue &+ 31 * (bar.hashValue &+ 31 &* baz.hashValue)
}
```

**INCORRECT**
```swift
var hashValue: Int {
  // INCORRECT. This will trap arbitrarily and unpredictably depending on the
  // hash values of the individual terms.
  return foo.hashValue + 31 * (bar.hashValue + 31 * baz.hashValue)
}
```

Masking operations are also permitted in performance-sensitive code where the
values are already known to not cause overflow (or where overflow is not a
concern). In this case, comments should be used to indicate why the use of
masking operations is important. Additionally, consider adding debug
preconditions to check these assumptions without affecting performance of
optimized builds.
