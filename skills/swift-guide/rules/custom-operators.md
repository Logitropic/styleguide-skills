# Custom Operators

### Defining New Operators

When used unwisely, custom-defined operators can significantly reduce the
readability of code because such operators often lack the historical context of
the more common ones built into the standard library.

In general, defining custom operators should be avoided. However, it is allowed
when an operator has a clear and well-defined meaning in the problem domain
and when using an operator significantly improves the readability of the code
when compared to function calls. For example, since `*` is the only
multiplication operator defined by Swift (not including the masking version), a
numeric matrix library may define additional operators to support other
operations like cross product and dot product.

An example of a prohibited use case is defining custom `<~~` and `~~>` operators
to decode and encode JSON data. Such operators are not native to the problem
domain of processing JSON and even an experienced Swift engineer would have
difficulty understanding the purpose of the code without seeking out
documentation of those operators.

If you must use third-party code of unquestionable value that provides an API
only available through custom operators, you are **strongly encouraged** to
consider writing a wrapper that defines more readable methods that delegate to
the custom operators. This will significantly reduce the learning curve required
to understand how such code works for new teammates and other code reviewers.

### Overloading Existing Operators

Overloading operators is permitted when your use of the operator is semantically
equivalent to the existing uses in the standard library. Examples of permitted
use cases are implementing the operator requirements for `Equatable` and
`Hashable`, or defining a new `Matrix` type that supports arithmetic operations.

If you wish to overload an existing operator with a meaning other than its
natural meaning, follow the guidance in
[Defining New Operators](#defining-new-operators) to determine whether this is
permitted. In other words, if the new meaning is well-established in the problem
domain and the use of the operator is a readability improvement over other
syntactic constructs, then it is permitted.

An example of a prohibited case of operator repurposing would be to overload `*`
and `+` to build an ad hoc regular expression API. Such an API would not provide
strong enough readability benefits compared to simply representing the entire
regular expression as a string.
