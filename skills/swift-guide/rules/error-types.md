# Error Types

Error types are used when there are multiple possible error states.

Throwing errors instead of merging them with the return type cleanly separates
concerns in the API. Valid inputs and valid state produce valid outputs in the
result domain and are handled with standard sequential control flow. Invalid
inputs and invalid state are treated as errors and are handled using the
relevant syntactic constructs (`do`-`catch` and `try`). For example:

**GOOD**
```swift
struct Document {
  enum ReadError: Error {
    case notFound
    case permissionDenied
    case malformedHeader
  }

  init(path: String) throws {
    // ...
  }
}

do {
  let document = try Document(path: "important.data")
} catch Document.ReadError.notFound {
  // ...
} catch Document.ReadError.permissionDenied {
  // ...
} catch {
  // ...
}
```

Such a design forces the caller to consciously acknowledge the failure case by:

* wrapping the calling code in a `do`-`catch` block and handling error cases to
  whichever degree is appropriate,
* declaring the function in which the call is made as `throws` and letting the
  error propagate out, or
* using `try?` when the specific reason for failure is unimportant and only the
  information about whether the call failed is needed.

In general, with exceptions noted below, force-`try!` is forbidden; it is
equivalent to `try` followed by `fatalError` but without a meaningful message.
If an error outcome would mean that the program is in such an unrecoverable
state that immediate termination is the only reasonable action, it is better to
use `do`-`catch` or `try?` and provide more context in the error message to
assist debugging if the operation does fail.

> **Exception:** Force-`try!` is allowed in unit tests and test-only code. It is
> also allowed in non-test code when it is unmistakably clear that an error
> would only be thrown because of **programmer** error; we specifically define
> this to mean a single expression that could be evaluated without context in
> the Swift REPL. For example, consider initializing a regular expression from a
> a string literal:
>
> **GOOD**
> ```swift
> let regex = try! NSRegularExpression(pattern: "a*b+c?")
> ```
>
> The `NSRegularExpression` initializer throws an error if the regular
> expression is malformed, but when it is a string literal, the error would only
> occur if the programmer mistyped it. There is no benefit to writing extra
> error handling logic here.
>
> If the pattern above were not a literal but instead were dynamic or derived
> from user input, `try!` should **not** be used and errors should be handled
> gracefully.
