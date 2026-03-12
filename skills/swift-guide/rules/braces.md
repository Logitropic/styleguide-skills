# Braces

In general, braces follow Kernighan and Ritchie (K&R) style for non-empty
blocks with exceptions for Swift-specific constructs and rules:

* There **is no** line break before the opening brace (`{`), **unless** required
  by application of the rules in [Line-Wrapping](#line-wrapping).
* There **is a** line break after the opening brace (`{`), except
  * in closures, where the signature of the closure is placed on the same line
    as the curly brace, if it fits, and a line break follows the `in` keyword.
  * where it may be omitted as described in
    [One Statement Per Line](#one-statement-per-line).
  * empty blocks may be written as `{}`.
* There **is a** line break before the closing brace (`}`), except where it may
  be omitted as described in [One Statement Per Line](#one-statement-per-line),
  or it completes an empty block.
* There **is a** line break after the closing brace (`}`), **if and only if**
  that brace terminates a statement or the body of a declaration. For example,
  an `else` block is written `} else {` with both braces on the same line.
