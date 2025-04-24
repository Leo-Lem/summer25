[[patterns.pdf]]
## Patterns
_3-part rule expressing relation between context, problem, and solution._
* **Algorithm**s are defined sequence for solving problem. v. **Pattern**: general core of solution.
* **Pattern**s are knowledge to solve problems, acquired from failures and empirical research (observation & data).
**Coding patterns**: Typing, Abstraction, Coupling, Polymorphism, Binding, Delegation.
**Categorization**
- Idiom (Coding Pattern): low-level, language-specific.
- Design Pattern: mid-level, context-specific, but language-agnostic.
- Architectural Pattern: high-level, fundamental.
### Design Patterns
_Resuable design generalised from existing systems, provide shared vocabulary._
**go4 patterns** (Gang of Four, 23 patterns)
- structural: reduce coupling, enable extension, encapsulate.
- behavioral: enable dynamic choice, responsibility, simplify complex control flow.
- creational: simplified creation, independence from object handling.
### Structural
**Adapter**. _multiple existing systems need to be connected_. rewriting infeasible, avoid temporary connector code in existing systems. <u>use adapter, inheritance then delegation.</u>
**Bridge**: *interface with multiple options (at design-/runtime)*. don't know how many options, avoid multiple hard-to-maintain IFs. <u>use bridge, delegation then inheritance.</u>
**Proxy**: *similar objects in multiple places.* Large, already on-system, unavailable, otherwise infeasible objects. <u>separate protected information, use proxy to load basics, inheritance to make proxy and real interchangeable.</u> (cache, substitute, access control)
**Composite**: *tree-structure of nested objects.* nesting is recursive with similar objects, dry, unknown nesting depth. <u>explicit nesting via recursivity, inheritance outlines all possible objects, extra subclass contains children of super.</u> (graphic->primitive & container with children, for example)
### Behavioral
**Observer**: *frequently changing object.* dependency on object, maintaining consistency. <u>explicit observer/subscriber list, inheritance enforces observer structure, notification by subject/publisher, sometimes also pull by observers.</u>
1. push/push: all observers receive updated state changes.
2. push/pull: all observers receive update. must pull in new state.
3. pull: observer requests state.
**Strategy**: *many algorithm options for implementation.* system must decide itself at runtime. <u>interchangeable algorithms, picked by client-defined policy, delegation to invoke, inheritance for interchangeability.</u>
**Template**: *repeating functionality.* differing implementation details, new context/situation requires exact steps. <u>abstract class with functionality, inheritance for structure, parent is responsible.</u>
### Creational
**Factory**: *consistently create similar objects.* varying init states, tight coupling of creation and further manipulation. <u>separate object creation with factory, delegate creation, inheritance forces common structure.</u>
**Abstract Factory**: *consistently create similar objects.* extends factory for different objects, enforce combination maintainably. <u>abstract factory calls many factory classes, delegate to astract factory, single object creation process.</u>
