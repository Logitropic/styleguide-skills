# Vertical Whitespace

A single blank line appears in the following locations:

1. Between consecutive members of a type: properties, initializers, methods,
   enum cases, and nested types, **except that**:

   1. A blank line is optional between two consecutive stored properties or two
      enum cases whose declarations fit entirely on a single line. Such blank
      lines can be used to create _logical groupings_ of these declarations.
   1. A blank line is optional between two extremely closely related properties
      that do not otherwise meet the criterion above; for example, a private
      stored property and a related public computed property.

1. _Only as needed_ between statements to organize code into logical
   subsections.
1. _Optionally_ before the first member or after the last member of a type
   (neither is encouraged nor discouraged).
1. Anywhere explicitly required by other sections of this document.

_Multiple_ blank lines are permitted, but never required (nor encouraged). If
you do use multiple consecutive blank lines, do so consistently throughout your
code base.
