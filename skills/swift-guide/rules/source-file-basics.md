# Source File Basics

### File Names

All Swift source files end with the extension `.swift`.

In general, the name of a source file best describes the primary entity that it
contains. A file that primarily contains a single type has the name of that
type. A file that extends an existing type with protocol conformance is named
with a combination of the type name and the protocol name, joined with a plus
(`+`) sign. For more complex situations, exercise your best judgment.

For example,

* A file containing a single type `MyType` is named `MyType.swift`.
* A file containing a type `MyType` and some top-level helper functions is also
  named `MyType.swift`. (The top-level helpers are not the primary entity.)
* A file containing a single extension to a type `MyType` that adds conformance
  to a protocol `MyProtocol` is named `MyType+MyProtocol.swift`.
* A file containing multiple extensions to a type `MyType` that add
  conformances, nested types, or other functionality to a type can be named more
  generally, as long as it is prefixed with `MyType+`; for example,
  `MyType+Additions.swift`.
* A file containing related declarations that are not otherwise scoped under a
  common type or namespace (such as a collection of global mathematical
  functions) can be named descriptively; for example, `Math.swift`.

### File Encoding

Source files are encoded in UTF-8.

### Whitespace Characters

Aside from the line terminator, the Unicode horizontal space character
(`U+0020`) is the only whitespace character that appears anywhere in a source
file. The implications are:

* All other whitespace characters in string and character literals are
  represented by their corresponding escape sequence.
* Tab characters are not used for indentation.

### Special Escape Sequences

For any character that has a special escape sequence (`\t`, `\n`, `\r`, `\"`,
`\'`, `\\`, and `\0`), that sequence is used rather than the equivalent Unicode
(e.g., `\u{000a}`) escape sequence.

### Invisible Characters and Modifiers

Invisible characters, such as the zero width space and other control characters
that do not affect the graphical representation of a string, are always written
as Unicode escape sequences.

Control characters, combining characters, and variation selectors that _do_
affect the graphical representation of a string are not escaped when they are
attached to a character or characters that they modify. If such a Unicode scalar
is present in isolation or is otherwise not modifying another character in the
same string, it is written as a Unicode escape sequence.

The strings below are well-formed because the umlauts and variation selectors
associate with neighboring characters in the string. The second example is in
fact composed of _five_ Unicode scalars, but they are unescaped because the
specific combination is rendered as a single character.

**GOOD**
```swift
let size = "Übergröße"
let shrug = "🤷🏿‍️"
```

In the example below, the umlaut and variation selector are in strings by
themselves, so they are escaped.

**GOOD**
```swift
let diaeresis = "\u{0308}"
let skinToneType6 = "\u{1F3FF}"
```

If the umlaut were included in the string literally, it would combine with
the preceding quotation mark, impairing readability. Likewise, while most
systems may render a standalone skin tone modifier as a block graphic, the
example below is still forbidden because it is a modifier that is not modifying
a character in the same string.

**BAD**
```swift
let diaeresis = "̈"
let skinToneType6 = "🏿"
```

### String Literals

Unicode escape sequences (`\u{????}`) and literal code points (for example, `Ü`)
outside the 7-bit ASCII range are never mixed in the same string.

More specifically, string literals are either:

* composed of a combination of Unicode code points written literally and/or
  single character escape sequences (such as `\t`, but _not_ `\u{????}`), or
* composed of 7-bit ASCII with any number of Unicode escape sequences and/or
  other escape sequences.

The following example is correct because `\n` is allowed to be present among
other Unicode code points.

**GOOD**
```swift
let size = "Übergröße\n"
```

The following example is allowed because it follows the rules above, but it is
_not preferred_ because the text is harder to read and understand compared to
the string above.

**GOOD**
```swift
let size = "\u{00DC}bergr\u{00F6}\u{00DF}e\n"
```

The example below is forbidden because it mixes code points outside the 7-bit
ASCII range in both literal form and in escaped form.

**BAD**
```swift
let size = "Übergr\u{00F6}\u{00DF}e\n"
```

> **Aside:** Never make your code less readable simply out of fear
> that some programs might not handle non-ASCII characters properly. If that
> should happen, those programs are broken and must be fixed.
