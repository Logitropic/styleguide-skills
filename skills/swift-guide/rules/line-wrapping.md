# Line-Wrapping

> Terminology note: **Line-wrapping** is the activity of dividing code into
> multiple lines that might otherwise legally occupy a single line.

For the purposes of Google Swift style, many declarations (such as type
declarations and function declarations) and other expressions (like function
calls) can be partitioned into **breakable** units that are separated by
**unbreakable** delimiting token sequences.

As an example, consider the following complex function declaration, which needs
to be line-wrapped:

**BAD**
```swift
public func index<Elements: Collection, Element>(of element: Element, in collection: Elements) -> Elements.Index? where Elements.Element == Element, Element: Equatable {
  // ...
}
```

This declaration is split as follows.

```swift
public func index< // Unbreakable
Elements: Collection, Element // Breakable
>( // Unbreakable
of element: Element, in collection: Elements // Breakable
) -> // Unbreakable
Elements.Index? // Breakable
where // Unbreakable
Elements.Element == Element, Element: Equatable // Breakable
{
  // ...
}
```

1. The **unbreakable** token sequence up through the open angle bracket (`<`)
   that begins the generic argument list.
1. The **breakable** list of generic arguments.
1. The **unbreakable** token sequence (`>(`) that separates the generic
   arguments from the formal arguments.
1. The **breakable** comma-delimited list of formal arguments.
1. The **unbreakable** token-sequence from the closing parenthesis (`)`) up
   through the arrow (`->`) that precedes the return type.
1. The **breakable** return type.
1. The **unbreakable** `where` keyword that begins the generic constraints list.
1. The **breakable** comma-delimited list of generic constraints.

Using these concepts, the cardinal rules of Google Swift style for line-wrapping
are:

1. If the entire declaration, statement, or expression fits on one line, then do
   that.
1. Comma-delimited lists are only laid out in one direction: horizontally or
   vertically. In other words, all elements must fit on the same line, or each
   element must be on its own line. A horizontally-oriented list does not
   contain any line breaks, even before the first element or after the last
   element. Except in control flow statements, a vertically-oriented list
   contains a line break before the first element and after each element.
1. A continuation line starting with an unbreakable token sequence is indented
   at the same level as the original line.
1. A continuation line that is part of a vertically-oriented comma-delimited
   list is indented exactly +2 from the original line.
1. When an open curly brace (`{`) follows a line-wrapped declaration or
   expression, it is on the same line as the final continuation line unless that
   line is indented at +2 from the original line. In that case, the brace is
   placed on its own line, to avoid the continuation lines from blending
   visually with the body of the subsequent block.

   **GOOD**
   ```swift
   public func index<Elements: Collection, Element>(
     of element: Element,
     in collection: Elements
   ) -> Elements.Index?
   where
     Elements.Element == Element,
     Element: Equatable
   {  // GOOD.
     for current in elements {
       // ...
     }
   }
   ```

   **AVOID**
   ```swift
   public func index<Elements: Collection, Element>(
     of element: Element,
     in collection: Elements
   ) -> Elements.Index?
   where
     Elements.Element == Element,
     Element: Equatable {  // AVOID.
     for current in elements {
       // ...
     }
   }
   ```

For declarations that contain a `where` clause followed by generic constraints,
additional rules apply:

1. If the generic constraint list exceeds the column limit when placed on the
   same line as the return type, then a line break is first inserted **before**
   the `where` keyword and the `where` keyword is indented at the same level as
   the original line.
1. If the generic constraint list still exceeds the column limit after inserting
   the line break above, then the constraint list is oriented vertically with a
   line break after the `where` keyword and a line break after the final
   constraint.

Concrete examples of this are shown in the relevant subsections below.

This line-wrapping style ensures that the different parts of a declaration are
_quickly and easily identifiable to the reader_ by using indentation and line
breaks, while also preserving the same indentation level for those parts
throughout the file. Specifically, it prevents the zig-zag effect that would be
present if the arguments are indented based on opening parentheses, as is common
in other languages:

**AVOID**
```swift
public func index<Elements: Collection, Element>(of element: Element,  // AVOID.
                                                 in collection: Elements) -> Elements.Index?
    where Elements.Element == Element, Element: Equatable {
  doSomething()
}
```

#### Function Declarations

The following structure shows breakable units:

```swift
modifiers func name(formal arguments) { ... }

modifiers func name(formal arguments) -> result { ... }

modifiers func name<generic arguments>(formal arguments) throws -> result { ... }

modifiers func name<generic arguments>(formal arguments) throws -> result where generic constraints { ... }
```

Applying the rules above from left to right gives us the following
line-wrapping:

**GOOD**
```swift
public func index<Elements: Collection, Element>(
  of element: Element,
  in collection: Elements
) -> Elements.Index? where Elements.Element == Element, Element: Equatable {
  for current in elements {
    // ...
  }
}
```

Function declarations in protocols that are terminated with a closing
parenthesis (`)`) may place the parenthesis on the same line as the final
argument **or** on its own line.

**GOOD**
```swift
public protocol ContrivedExampleDelegate {
  func contrivedExample(
    _ contrivedExample: ContrivedExample,
    willDoSomethingTo someValue: SomeValue)
}

public protocol ContrivedExampleDelegate {
  func contrivedExample(
    _ contrivedExample: ContrivedExample,
    willDoSomethingTo someValue: SomeValue
  )
}
```

If types are complex and/or deeply nested, individual elements in the
arguments/constraints lists and/or the return type may also need to be wrapped.
In these rare cases, the same line-wrapping rules apply to those parts as apply
to the declaration itself.

**GOOD**
```swift
public func performanceTrackingIndex<Elements: Collection, Element>(
  of element: Element,
  in collection: Elements
) -> (
  Element.Index?,
  PerformanceTrackingIndexStatistics.Timings,
  PerformanceTrackingIndexStatistics.SpaceUsed
) {
  // ...
}
```

However, `typealias`es or some other means are often a better way to simplify
complex declarations whenever possible.

#### Type and Extension Declarations

The examples below apply equally to `class`, `struct`, `enum`, `extension`, and
`protocol`.

Structure:
```swift
modifiers class Name { ... }

modifiers class Name: superclass and protocols { ... }

modifiers class Name<generic arguments>: superclass and protocols { ... }

modifiers class Name<generic arguments>: superclass and protocols where generic constraints { ... }
```

**GOOD**
```swift
class MyClass:
  MySuperclass,
  MyProtocol,
  SomeoneElsesProtocol,
  SomeFrameworkProtocol
{
  // ...
}

class MyContainer<Element>:
  MyContainerSuperclass,
  MyContainerProtocol,
  SomeoneElsesContainerProtocol,
  SomeFrameworkContainerProtocol
{
  // ...
}

class MyContainer<BaseCollection>:
  MyContainerSuperclass,
  MyContainerProtocol,
  SomeoneElsesContainerProtocol,
  SomeFrameworkContainerProtocol
where BaseCollection: Collection {
  // ...
}

class MyContainer<BaseCollection>:
  MyContainerSuperclass,
  MyContainerProtocol,
  SomeoneElsesContainerProtocol,
  SomeFrameworkContainerProtocol
where
  BaseCollection: Collection,
  BaseCollection.Element: Equatable,
  BaseCollection.Element: SomeOtherProtocolOnlyUsedToForceLineWrapping
{
  // ...
}
```

#### Function Calls

When a function call is line-wrapped, each argument is written on its own line,
indented +2 from the original line.

As with function declarations, if the function call terminates its enclosing
statement and ends with a closing parenthesis (`)`) (that is, it has no trailing
closure), then the parenthesis may be placed **either** on the same line as the
final argument **or** on its own line.

**GOOD**
```swift
let index = index(
  of: veryLongElementVariableName,
  in: aCollectionOfElementsThatAlsoHappensToHaveALongName)

let index = index(
  of: veryLongElementVariableName,
  in: aCollectionOfElementsThatAlsoHappensToHaveALongName
)
```

If the function call ends with a trailing closure and the closure's signature
must be wrapped, then place it on its own line and wrap the argument list in
parentheses to distinguish it from the body of the closure below it.

**GOOD**
```swift
someAsynchronousAction.execute(withDelay: howManySeconds, context: actionContext) {
  (context, completion) in
  doSomething(withContext: context)
  completion()
}
```

#### Control Flow Statements

When a control flow statement (such as `if`, `guard`, `while`, or `for`) is
wrapped, the first continuation line is indented to the same position as the
token following the control flow keyword. Additional continuation lines are
indented at that same position if they are syntactically parallel elements, or
in +2 increments from that position if they are syntactically nested.

The open brace (`{`) preceding the body of the control flow statement can either
be placed on the same line as the last continuation line or on the next line,
at the same indentation level as the beginning of the statement. For `guard`
statements, the `else {` must be kept together, either on the same line or on
the next line.

**GOOD**
```swift
if aBooleanValueReturnedByAVeryLongOptionalThing() &&
   aDifferentBooleanValueReturnedByAVeryLongOptionalThing() &&
   yetAnotherBooleanValueThatContributesToTheWrapping() {
  doSomething()
}

if aBooleanValueReturnedByAVeryLongOptionalThing() &&
   aDifferentBooleanValueReturnedByAVeryLongOptionalThing() &&
   yetAnotherBooleanValueThatContributesToTheWrapping()
{
  doSomething()
}

if let value = aValueReturnedByAVeryLongOptionalThing(),
   let value2 = aDifferentValueReturnedByAVeryLongOptionalThing() {
  doSomething()
}

if let value = aValueReturnedByAVeryLongOptionalThing(),
   let value2 = aDifferentValueReturnedByAVeryLongOptionalThingThatForcesTheBraceToBeWrapped()
{
  doSomething()
}

guard let value = aValueReturnedByAVeryLongOptionalThing(),
      let value2 = aDifferentValueReturnedByAVeryLongOptionalThing() else {
  doSomething()
}

guard let value = aValueReturnedByAVeryLongOptionalThing(),
      let value2 = aDifferentValueReturnedByAVeryLongOptionalThing()
else {
  doSomething()
}

for element in collection
    where element.happensToHaveAVeryLongPropertyNameThatYouNeedToCheck {
  doSomething()
}
```

#### Other Expressions

When line-wrapping other expressions that are not function calls (as described
above), the second line (the one immediately following the first break) is
indented exactly +2 from the original line.

When there are multiple continuation lines, indentation may be varied in
increments of +2 as needed. In general, two continuation lines use the same
indentation level if and only if they begin with syntactically parallel
elements. However, if there are many continuation lines caused by long wrapped
expressions, consider splitting them into multiple statements using temporary
variables when possible.

**GOOD**
```swift
let result = anExpression + thatIsMadeUpOf * aLargeNumber +
  ofTerms / andTherefore % mustBeWrapped + (
    andWeWill - keepMakingItLonger * soThatWeHave / aContrivedExample)
```

**BAD**
```swift
let result = anExpression + thatIsMadeUpOf * aLargeNumber +
    ofTerms / andTherefore % mustBeWrapped + (
        and we will - keepMakingItLonger * soThatWeHave / aContrivedExample)
```
