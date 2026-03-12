# Delegate Methods

Methods on delegate protocols and delegate-like protocols (such as data sources)
are named using the linguistic syntax described below, which is inspired by
Cocoa's protocols.

> The term "delegate's source object" refers to the object that invokes methods
> on the delegate. For example, a `UITableView` is the source object that
> invokes methods on the `UITableViewDelegate` that is set as the view's
> `delegate` property.

All methods take the delegate's source object as the first argument.

For methods that take the delegate's source object as their **only** argument:

* If the method returns `Void` (such as those used to notify the delegate that
  an event has occurred), then the method's base name is the **delegate's
  source type** followed by an **indicative verb phrase** describing the
  event. The argument is **unlabeled.**

  **GOOD**
  ```swift
  func scrollViewDidBeginScrolling(_ scrollView: UIScrollView)
  ```

* If the method returns `Bool` (such as those that make an assertion about the
  delegate's source object itself), then the method's name is the **delegate's
  source type** followed by an **indicative or conditional verb phrase**
  describing the assertion. The argument is **unlabeled.**

  **GOOD**
  ```swift
  func scrollViewShouldScrollToTop(_ scrollView: UIScrollView) -> Bool
  ```

* If the method returns some other value (such as those querying for
  information about a property of the delegate's source object), then the
  method's base name is a **noun phrase** describing the property being
  queried. The argument is **labeled with a preposition or phrase with a
  trailing preposition** that appropriately combines the noun phrase and the
  delegate's source object.

  **GOOD**
  ```swift
  func numberOfSections(in scrollView: UIScrollView) -> Int
  ```

For methods that take **additional** arguments after the delegate's source
object, the method's base name is the delegate's source type **by itself** and
the first argument is **unlabeled.** Then:

* If the method returns `Void`, the second argument is **labeled with an
  indicative verb phrase** describing the event that has the argument as its
  **direct object or prepositional object,** and any other arguments (if
  present) provide further context.

  **GOOD**
  ```swift
  func tableView(
    _ tableView: UITableView,
    willDisplayCell cell: UITableViewCell,
    forRowAt indexPath: IndexPath)
  ```

* If the method returns `Bool`, the second argument is **labeled with an
  indicative or conditional verb phrase** that describes the return value in
  terms of the argument, and any other arguments (if present) provide further
  context.

  **GOOD**
  ```swift
  func tableView(
    _ tableView: UITableView,
    shouldSpringLoadRowAt indexPath: IndexPath,
    with context: UISpringLoadedInteractionContext
  ) -> Bool
  ```

* If the method returns some other value, the second argument is **labeled
  with a noun phrase and trailing preposition** that describes the return
  value in terms of the argument, and any other arguments (if present) provide
  further context.

  **GOOD**
  ```swift
  func tableView(
    _ tableView: UITableView,
    heightForRowAt indexPath: IndexPath
  ) -> CGFloat
  ```

Apple's documentation on
[delegates and data sources](https://developer.apple.com/library/content/documentation/General/Conceptual/CocoaEncyclopedia/DelegatesandDataSources/DelegatesandDataSources.html)
also contains some good general guidance about such names.
