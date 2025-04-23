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
**Adapter**: to legacy system. inheritance followed by delegation.
**Bridge**: enable multiple options at run-time. delegation followed by inheritance.
**Proxy**: defer object creation to actual time of need. cache, substitute, access control.
**Composite**: inheritance for types and subclass with superclass children (graphic->primitive & container with children)
### Behavioral

### Creational
