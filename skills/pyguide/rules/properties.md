<a id="s2.13-properties"></a>
<a id="213-properties"></a>

<a id="properties"></a>
### 2.13 Properties 

Properties may be used to control getting or setting attributes that require
trivial computations or logic. Property implementations must match the general
expectations of regular attribute access: that they are cheap, straightforward,
and unsurprising.

<a id="s2.13.1-definition"></a>
<a id="2131-definition"></a>

<a id="properties-definition"></a>
#### 2.13.1 Definition 

A way to wrap method calls for getting and setting an attribute as a standard
attribute access.

<a id="s2.13.2-pros"></a>
<a id="2132-pros"></a>

<a id="properties-pros"></a>
#### 2.13.2 Pros 

*   Allows for an attribute access and assignment API rather than
    [getter and setter](#getters-and-setters) method calls.
*   Can be used to make an attribute read-only.
*   Allows calculations to be lazy.
*   Provides a way to maintain the public interface of a class when the
    internals evolve independently of class users.

<a id="s2.13.3-cons"></a>
<a id="2133-cons"></a>

<a id="properties-cons"></a>
#### 2.13.3 Cons 

*   Can hide side-effects much like operator overloading.
*   Can be confusing for subclasses.

<a id="s2.13.4-decision"></a>
<a id="2134-decision"></a>

<a id="properties-decision"></a>
#### 2.13.4 Decision 

Properties are allowed, but, like operator overloading, should only be used when
necessary and match the expectations of typical attribute access; follow the
[getters and setters](#getters-and-setters) rules otherwise.

For example, using a property to simply both get and set an internal attribute
isn't allowed: there is no computation occurring, so the property is unnecessary
([make the attribute public instead](#getters-and-setters)). In comparison,
using a property to control attribute access or to calculate a *trivially*
derived value is allowed: the logic is simple and unsurprising.

Properties should be created with the `@property`
[decorator](#s2.17-function-and-method-decorators). Manually implementing a
property descriptor is considered a [power feature](#power-features).

Inheritance with properties can be non-obvious. Do not use properties to
implement computations a subclass may ever want to override and extend.
