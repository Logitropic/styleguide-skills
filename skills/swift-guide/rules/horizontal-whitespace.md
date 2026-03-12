# Horizontal Whitespace

> **Terminology note:** In this section, _horizontal whitespace_ refers to
> _interior_ space. These rules are never interpreted as requiring or forbidding
> additional space at the start of a line.

Beyond where required by the language or other style rules, and apart from
literals and comments, a single Unicode space also appears in the following
places **only**:

1. Separating any reserved word starting a conditional or switch statement (such
   as `if`, `guard`, `while`, or `switch`) from the expression that follows it
   if that expression starts with an open parenthesis (`(`).

   **GOOD**
   ```swift
   if (x == 0 && y == 0) || z == 0 {
     // ...
   }
   ```

   **BAD**
   ```swift
   if(x == 0 && y == 0) || z == 0 {
     // ...
   }
   ```

1. Before any closing curly brace (`}`) that follows code on the same line,
   before any open curly brace (`{`), and after any open curly brace (`{`) that
   is followed by code on the same line.

   **GOOD**
   ```swift
   let nonNegativeCubes = numbers.map { $0 * $0 * $0 }.filter { $0 >= 0 }
   ```

   **BAD**
   ```swift
   let nonNegativeCubes = numbers.map { $0 * $0 * $0 } .filter { $0 >= 0 }
   let nonNegativeCubes = numbers.map{$0 * $0 * $0}.filter{$0 >= 0}
   ```

1. _On both sides_ of any binary or ternary operator, including the
   "operator-like" symbols described below, with exceptions noted at the end:

   1. The `=` sign used in assignment, initialization of variables/properties,
      and default arguments in functions.

      **GOOD**
      ```swift
      var x = 5

      func sum(_ numbers: [Int], initialValue: Int = 0) {
        // ...
      }
      ```

      **BAD**
      ```swift
      var x=5

      func sum(_ numbers: [Int], initialValue: Int=0) {
        // ...
      }
      ```

   1. The ampersand (`&`) in a protocol composition type.

      **GOOD**
      ```swift
      func sayHappyBirthday(to person: NameProviding & AgeProviding) {
        // ...
      }
      ```

      **BAD**
      ```swift
      func sayHappyBirthday(to person: NameProviding&AgeProviding) {
        // ...
      }
      ```

   1. The operator symbol in a function declaring/implementing that operator.

      **GOOD**
      ```swift
      static func == (lhs: MyType, rhs: MyType) -> Bool {
        // ...
      }
      ```

      **BAD**
      ```swift
      static func ==(lhs: MyType, rhs: MyType) -> Bool {
        // ...
      }
      ```

   1. The arrow (`->`) preceding the return type of a function.

      **GOOD**
      ```swift
      func sum(_ numbers: [Int]) -> Int {
        // ...
      }
      ```

      **BAD**
      ```swift
      func sum(_ numbers: [Int])->Int {
        // ...
      }
      ```

   1. **Exception:** There is no space on either side of the dot (`.`) used to
      reference value and type members.

      **GOOD**
      ```swift
      let width = view.bounds.width
      ```

      **BAD**
      ```swift
      let width = view . bounds . width
      ```

   1. **Exception:** There is no space on either side of the `..<` or `...`
      operators used in range expressions.

      **GOOD**
      ```swift
      for number in 1...5 {
        // ...
      }

      let substring = string[index..<string.endIndex]
      ```

      **BAD**
      ```swift
      for number in 1 ... 5 {
        // ...
      }

      let substring = string[index ..< string.endIndex]
      ```

1. After, but not before, the comma (`,`) in parameter lists and in
   tuple/array/dictionary literals.

   **GOOD**
   ```swift
   let numbers = [1, 2, 3]
   ```

   **BAD**
   ```swift
   let numbers = [1,2,3]
   let numbers = [1 ,2 ,3]
   let numbers = [1 , 2 , 3]
   ```

1. After, but not before, the colon (`:`) in

   1. Superclass/protocol conformance lists and generic constraints.

      **GOOD**
      ```swift
      struct HashTable: Collection {
        // ...
      }

      struct AnyEquatable<Wrapped: Equatable>: Equatable {
        // ...
      }
      ```

      **BAD**
      ```swift
      struct HashTable : Collection {
        // ...
      }

      struct AnyEquatable<Wrapped : Equatable> : Equatable {
        // ...
      }
      ```

   1. Function argument labels and tuple element labels.

      **GOOD**
      ```swift
      let tuple: (x: Int, y: Int)

      func sum(_ numbers: [Int]) {
        // ...
      }
      ```

      **BAD**
      ```swift
      let tuple: (x:Int, y:Int)
      let tuple: (x : Int, y : Int)

      func sum(_ numbers:[Int]) {
        // ...
      }

      func sum(_ numbers : [Int]) {
        // ...
      }
      ```

   1. Variable/property declarations with explicit types.

      **GOOD**
      ```swift
      let number: Int = 5
      ```

      **BAD**
      ```swift
      let number:Int = 5
      let number : Int = 5
      ```

   1. Shorthand dictionary type names.

      **GOOD**
      ```swift
      var nameAgeMap: [String: Int] = []
      ```

      **BAD**
      ```swift
      var nameAgeMap: [String:Int] = []
      var nameAgeMap: [String : Int] = []
      ```

   1. Dictionary literals.

      **GOOD**
      ```swift
      let nameAgeMap = ["Ed": 40, "Timmy": 9]
      ```

      **BAD**
      ```swift
      let nameAgeMap = ["Ed":40, "Timmy":9]
      let nameAgeMap = ["Ed" : 40, "Timmy" : 9]
      ```

1. At least two spaces before and exactly one space after the double slash
   (`//`) that begins an end-of-line comment.

   **GOOD**
   ```swift
   let initialFactor = 2  // Warm up the modulator.
   ```

   **BAD**
   ```swift
   let initialFactor = 2 //    Warm up the modulator.
   ```

1. Outside, but not inside, the brackets of an array or dictionary literals and
   the parentheses of a tuple literal.

   **GOOD**
   ```swift
   let numbers = [1, 2, 3]
   ```

   **BAD**
   ```swift
   let numbers = [ 1, 2, 3 ]
   ```
