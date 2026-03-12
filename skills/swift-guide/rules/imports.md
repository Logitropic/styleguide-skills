# Import Statements

A source file imports exactly the top-level modules that it needs; nothing more
and nothing less. If a source file uses definitions from both `UIKit` and
`Foundation`, it imports both explicitly; it does not rely on the fact that some
Apple frameworks transitively import others as an implementation detail.

Imports of whole modules are preferred to imports of individual declarations or
submodules.

> There are a number of reasons to avoid importing individual members:
>
> * There is no automated tooling to resolve/organize imports.
> * Existing automated tooling (such as Xcode's migrator) are less likely to
>   work well on code that imports individual members because they are
>   considered corner cases.
> * The prevailing style in Swift (based on official examples and community
>   code) is to import entire modules.

Imports of individual declarations are permitted when importing the whole module
would otherwise pollute the global namespace with top-level definitions (such as
C interfaces). Use your best judgment in these situations.

Imports of submodules are permitted if the submodule exports functionality that
is not available when importing the top-level module. For example,
`UIKit.UIGestureRecognizerSubclass` must be imported explicitly to expose the
methods that allow client code to subclass `UIGestureRecognizer`&mdash;those are
not visible by importing `UIKit` alone.

Import statements are not line-wrapped.

Import statements are the first non-comment tokens in a source file. They are
grouped in the following fashion, with the imports in each group ordered
lexicographically and with exactly one blank line between each group:

1. Module/submodule imports not under test
1. Individual declaration imports (`class`, `enum`, `func`, `struct`, `var`)
1. Modules imported with `@testable` (only present in test sources)

**GOOD**
```swift
import CoreLocation
import MyThirdPartyModule
import SpriteKit
import UIKit

import func Darwin.C.isatty

@testable import MyModuleUnderTest
```
