# Source File Structure

### File Comments

Comments describing the contents of a source file are optional. They are
discouraged for files that contain only a single abstraction (such as a class
declaration)&mdash;in those cases, the documentation comment on the abstraction
itself is sufficient and a file comment is only present if it provides
additional useful information. File comments are allowed for files that contain
multiple abstractions in order to document that grouping as a whole.

### Type, Variable, and Function Declarations

In general, most source files contain only one top-level type, especially when
the type declaration is large. Exceptions are allowed when it makes sense to
include multiple related types in a single file. For example,

* A class and its delegate protocol may be defined in the same file.
* A type and its small related helper types may be defined in the same file.
  This can be useful when using `fileprivate` to restrict certain functionality
  of the type and/or its helpers to only that file and not the rest of the
  module.

The order of types, variables, and functions in a source file, and the order of
the members of those types, can have a great effect on readability. However,
there is no single correct recipe for how to do it; different files and
different types may order their contents in different ways.

What is important is that each file and type uses _**some** logical order,_
which its maintainer could explain if asked. For example, new methods are not
just habitually added to the end of the type, as that would yield "chronological
by date added" ordering, which is not a logical ordering.

When deciding on the logical order of members, it can be helpful for readers and
future writers (including yourself) to use `// MARK:` comments to provide
descriptions for that grouping. These comments are also interpreted by Xcode and
provide bookmarks in the source window's navigation bar. (Likewise,
`// MARK: - `, written with a hyphen before the description, causes Xcode to
insert a divider before the menu item.) For example,

~~~ swift
class MovieRatingViewController: UITableViewController {

  // MARK: - View controller lifecycle methods

  override func viewDidLoad() {
    // ...
  }

  override func viewWillAppear(_ animated: Bool) {
    // ...
  }

  // MARK: - Movie rating manipulation methods

  @objc private func ratingStarWasTapped(_ sender: UIButton?) {
    // ...
  }

  @objc private func criticReviewWasTapped(_ sender: UIButton?) {
    // ...
  }
}
~~~
{:.good}

### Overloaded Declarations

When a type has multiple initializers or subscripts, or a file/type has multiple
functions with the same base name (though perhaps with different argument
labels), _and_ when these overloads appear in the same type or extension scope,
they appear sequentially with no other code in between.

### Extensions

Extensions can be used to organize functionality of a type across multiple
"units." As with member order, the organizational structure/grouping you choose
can have a great effect on readability; you must use _**some** logical
organizational structure_ that you could explain to a reviewer if asked.
