[patterns.pdf](patterns.pdf)
# Patterns
_3-part rule expressing relation between context, problem, and solution._
* **Algorithm**s are defined sequence for solving problem. v. **Pattern**: general core of solution.
* **Pattern**s are knowledge to solve problems, acquired from failures and empirical research (observation & data).
**Coding patterns**: Typing, Abstraction, Coupling, Polymorphism, Binding, Delegation.
**Categorization**
- Idiom (Coding Pattern): low-level, language-specific.
- Design Pattern: mid-level, context-specific, but language-agnostic.
- Architectural Pattern: high-level, fundamental.
# Design Patterns
_Resuable design generalised from existing systems, provide shared vocabulary._
**go4 patterns** (Gang of Four, 23 patterns)
- structural: reduce coupling, enable extension, encapsulate.
- behavioral: enable dynamic choice, responsibility, simplify complex control flow.
- creational: simplified creation, independence from object handling.
## Structural
**Adapter**. _multiple existing systems need to be connected_. rewriting infeasible, avoid temporary connector code in existing systems. <u>use adapter, inheritance then delegation.</u>
**Bridge**: *interface with multiple options (at design-/runtime)*. don't know how many options, avoid multiple hard-to-maintain IFs. <u>use bridge, delegation then inheritance.</u>
**Proxy**: *similar objects in multiple places.* Large, already on-system, unavailable, otherwise infeasible objects. <u>separate protected information, use proxy to load basics, inheritance to make proxy and real interchangeable.</u> (cache, substitute, access control)
**Composite**: *tree-structure of nested objects.* nesting is recursive with similar objects, dry, unknown nesting depth. <u>explicit nesting via recursivity, inheritance outlines all possible objects, extra subclass contains children of super.</u> (graphic->primitive & container with children, for example)
## Behavioral
**Observer**: *frequently changing object.* dependency on object, maintaining consistency. <u>explicit observer/subscriber list, inheritance enforces observer structure, notification by subject/publisher, sometimes also pull by observers.</u>
1. push/push: all observers receive updated state changes.
2. push/pull: all observers receive update. must pull in new state.
3. pull: observer requests state.
**Strategy**: *many algorithm options for implementation.* system must decide itself at runtime. <u>interchangeable algorithms, picked by client-defined policy, delegation to invoke, inheritance for interchangeability.</u>
**Template**: *repeating functionality.* differing implementation details, new context/situation requires exact steps. <u>abstract class with functionality, inheritance for structure, parent is responsible.</u>
## Creational
**Factory**: *consistently create similar objects.* varying init states, tight coupling of creation and further manipulation. <u>separate object creation with factory, delegate creation, inheritance forces common structure.</u>
**Abstract Factory**: *consistently create similar objects.* extends factory for different objects, enforce combination maintainably. <u>abstract factory calls many factory classes, delegate to astract factory, single object creation process.</u>
# Documentation Patterns
*Material produced for sharing knowledge of sofware with target human group.*
**Landscape**: tutorials, how-to guides, explanation, reference (diátaxis framework).
**Model Cards** (Mitchell et al.): standard framework for AI documentation.
## Content
*Taxonomies provide standard vocabulary, organize, and help evaluate quality of docs.*
**Knowledge types in API docs**: functionality & behavior, concepts, directives, purpose & rationale, quality attributes, control-flow, structure, patterns, examples, environment, references, non-information.
**Other types** (Sillito et al.): finding focus points, expanding focus points, understanding a subgraph, questions over groups of subgraphs.
**More** (Beyer et al.): api usage, discrepancy, errors, review, conceptual, api change, learning.
## Format
*Format is as important as content. Especially consider interactive tools.*
mutable page layout: multiple programming languages, for example.
runnable code example: CSS animation demo, for example.
adapt content to user input: Select environment, for example.
casdoc (interactive annotated code): inline docs.
# Architectural Patterns
*Result of consistent principles/techniques applied through all project phases, resilient in change, guidance through product lifetime.*
**Components**: computational units, subsystems (databases, filters, layers, objects).
**Connectors**: interactions between subsystems (method calls, pipes, events, shared data).
**Distributed Systems**: communication required. pros: economics, scalability, performance, reliability.
**Peer-to-peer**: clients can be servers and vice-versa.
## Layers
*Technical partitioning into layers.*
**Closed** (opaque) layering: only access layer directly below. flexibility and maintainability.
**Open** (transparent) layering: access all layers below. runtime efficiency.
**System design**: define abstraction criterion, determine number of layers, name the layers and assign tasks, specify the services, refine the layering.
**Object desig**n: interface (black-box: facade pattern, white-box: visible components), structure (bridge, strategy, partitioning), communication (push: n to n-1, pull: n-1 to n), decoupling (closed, callbacks with command pattern), error-handling (lowest possible layer, translate to more general errors for upper layers).
**OSI 7 layers**: application (protocols for common activites), presentation (structure information and add semantics), session (dialog control and sync), transport (messages>packets and delivery guarentee), network (routing), data link (errors in bit sequences), physical (transmit bits).
**Pros**: reusability of layers, standardization, low coupling, improved testability
**Cons**: lower layer changes may propagate to higher layers, lower efficiency.
## Repository/Blackboard
*independent systems cooperate on common data structure. blackboard uses passive, opportunistic, decoupled knowledge sources which sync through the blackboard data.*
**Realisation**: define problem, define solution space, identify knowledge sources, define blackboard, define control, implement knowledge sources.
**Pros**: problem solving support, changeability and maintainability, faul tolerance and robustness.
**Cons**: difficult to test, no guarenteed solution, difficult control strategy, high development effort.
## Model View Controller
*user interface system with decoupled data access and presentation.*
**Subsystems**: view (data presentation), model (data access), controller (mediator).
**Compound pattern**: strategy, composite, factory, observer, mediator.
## Client-Dispatcher-Server
*Client-server, but use a name server for communication (decoupling servers and clients).*
**Steps**: identify subsystems that act as clients and servers. decide on communication mechanisms. specify interaction protocols. decide on naming scheme. implement dispatcher. implement client/server.
**Uses**: RPC by Sun, CORBA, UDDI.
## Broker
*Broker is responsible for communication and invokes remote services.*
**Design goals**: location transparency, programming language independence, client/server decoupling, service/communication mechanism decoupling, runtime extensibiilty.
**Core components**: client (accesses remote services), server (provides remote services via interface, eg, in JSON), broker (transmits requests/responses between client/server).
**Local v. remote**: on client machine v. remote machine (eg, name server).
**Proxies**: client-side (makes remote object appear local, hides communication details, marshalling/serialization of parameters/results). server-side (receive broker requests, hide communication details, unmarshalling/deseralization of parameters/results, call server services).
**Bridge**: hide implementation details between two interoperating brokers.
Steps: define object model, decide interoperability level, specify broker API, proxies for client/server access, design broker component (parallel to steps 3/4), define interface.
# Testing Patterns

# More Patterns
## Quality Patterns
## Collaboration Patterns
## UX Patterns