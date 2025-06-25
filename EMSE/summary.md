[requirements](requirements.pdf)
*difficult to elicit good requirements, but fixing problems early is cheap.*
# Requirements
### Types
* functional: supported user tasks, system behaviour, interactions with environment.
* & non-functional: properties of system or domain.
	* constraints: imposed by customer or environment.
	* & quality (ISO-IEC 25010): suitability, performance, compatibility, usability, reliability, security, maintainability, portability.
**Questions are core**: users, hardware/performance, interfaces, quality, environment, resources, data.
## Engineering (RE)
_Desired properties/constraints and goals of the software, assumptions about environment._
* **Views**: engineering (systematic & repeatable techniques), lifecycle (discovery, documentation, analysis, communication, implementation), knowledge (making hard decisions).
* **Activities**: elicitation, analysis, specification, verification, management.
* **Process**: formulate, document, maintain.
* **Elicitation**: customer perspective, natural language. v. **Analysis**: developer perspective, formalised.
* **Types of RE**: greenfield (user-needs), reengineering (technology enabler), interface engineering (new environment, technology enabler or new market needs)
* **Challenges**: developer-user gap (application- v. solution domain knowledge), identifying appropriate system, ambiguous specification, unintended features, system boundary definition.
## Management
_schedule, negotiate, coordinate, document._
* **Requirements Quality**: correctness, completeness, consistency, clarity, realism, traceability.
* **Priority Aspects**: importance, cost, risk, time, financial, penalty.
## Requirements Elicitation

* **Soft skills**: analytics thinking, empathy, communication, conflict resolution, moderation, confidence, persuasiveness.
* Discover needs and acquire knowledge about: stakeholders, expectations, current state, domain, tasks, system/context.
* **Sources**: Stakeholders, documents, systems in production.
### Stakeholders
_Involved in and affected by our project._
* **Characteristics**: expectations, importance, their requirements.
* **Population sampling**: non-probability (specific selection), probability (equal chance), convenience (easy access), sequential (iterative), snowball (subjects recommend subjects).
### Methods
_Interview/Survey, observation, scenario, use case, mockup_
* **qualitative**: interviews, workshops, focus groups, case studies, observations.
	* **interview**: use templates, iterate, dry runs, don't influence, scoped, active listening.
		* **smells**: irrelevant questions, multiple concepts, too long questions, confusing/misleading questions, too technical questions.
		* **topics**: start, interviewee, current status, problems, solutions, stakeholders, qualities/trade offs, environment, legal/compliance, priorities/timing/cost, summary.
	* **workshop**: structured meeting, group of stakeholders.
	* **focus group**: representative group of users (either same group, e.g., dev only, or different group, dev, manager, etc.)
* **quantitative**: surveys, observations, experiments, data analysis, content analysis, simulation.
	* **questionnaires**: iterate, describe objective, short, exclude non-serious, incentives, meaningful abbreviation for analysis, statistical tests, quasi-experimentation instead of summary.
	* **observation**: report what you observe at least twice, talk with peers, iterate.
* **question types**: exploratory (existence, description/classification, comparative), baserate (frequency/distribution, process), correlation (relationship), design, causal (causality, causality-comparative).
* **empirical methods and questions**: experiment (how, why), survey (who, what, where, how many, how much), content analysis (who, what, where, how many, how much), history (how, why), field study (how, why), interview (how, why how much, what, where), observation (who, what, where, how many, how much).
# Prototyping
*Externalizing and concretizing a design idea for evaluation.*
**Fidelity**: closeness to actual product. evaluated in terms of content, interactivity, design.
**Techniques** (low to high fidelity): sketches, wireframes, mockups, prototype.
**Why**? deal with complexity, explore solution domain, communicate, feedback, concretize.
**Perspectives**: requirements improvement, design exploration, communication.
**Criteria**: stakeholder, speed, medium, fidelity, stage of project, style, cost, longevity.
**Tools**: Figma, sketch, lucidchart, Xd, …
## Dimensions
**Horizontal**: broad view of system. Externalize, explore and assess system.
**Vertical**: Proof of concept, specific functionality through all layers. clarify feasibility, test specific tooling, estimate effort.
## Types
**Throwaway**: not maintained. to answer questions, resolve uncertainties, improve requirements. build as quickly and cheaply as possible.
**Evolutionary**: provide solid architectural foundation, improve incrementally with requirements. build for quality, design for growth and enhancement.
## Evaluation
*related to usability testing.*
**Observation**: watch users work with prototype.
**Interview/survey**: ask users for opinions.
**Sampling**: include various experience level users.
**Controlled experiments**: evaluate with stakeholders.
### Experiment design
**Independent variables**: input variables (factors) that are manipulated.
**Dependent variables**: output variables which are observed.
**Treatments**: combination of input values.
**Subjects**: human participants.
**Disproving H0**: H0 means theory does not apply, assume to be true, unless data says otherwise. then experiment suggests H1 is correct.
**Within- v. between-subjects**: each subject tries all treatments v. different subjects try different treatments. challenge is increased learning effects v. increased confounding factors. mitigated by balancing (varying order) for symmetric effects v. blocking (group subjects equally) for measurable factors.
**Positivist and reductionist**: assume we can reduce complex phenomena to few variables. critical variables might be ignored.
**Interaction effects**: variables together have effect that none has on its own.
# User Involvement
*Improve understanding of user needs, users as productive resource, and give voice/avoid frustration.*
**Principles**: early focus on users and tasks, empirical measurement, iterative design.
**User classes**: favoured (main users, admins, …) v. disfavoured (hackers, …) v. indirect (website integration, …).
**Product champions** handle: planning, requirements, validation, user aids, change management.
**Personas**: fictional representative of user class.
## Crowdsourcing requirements
*revolutionise role of users, dissolve boundaries to SE, make processes and tools social.*
**Socialness**: degree of involvement of users and communities in software lifecycle.
- Community Involvement: size, activity, interweaving, attractiveness.
- User involvement: quality, explicitness, time, means.
Challenges: scalability, quality, authenticity, conflicts.
**Liquid democracy**: combine direct and representative democracy with choice per vote (choose or be represented).
**User voice**: limited number of votes, prioritise requests.
**SNAIL** (break down into smaller and smaller parts.): user and community observation, proactive feedback, systematic analysis, engineering decision, update.
## User Feedback
**Types**: explicit (reviews, social media, …), implicit (interaction data, …).
**Topics**: requirements, community, rating, user experience.
**Use ML for automatic mining**: filter, allocate/assign, compare, track over time.
# Requirements Modeling
**To better understand, communicate, explore, and reuse.**
**Model**: abstract representation of reality.
**Languages**: Natural (Gellish, …), semi-formal (UML, i*, …), formal (Z, VDM, …).
**Perspectives**: structural -integration> functional -integration> behavioural -integration> …
## Functional Modelling
**Scenario**: concrete, focused, informal feature description (series of use cases).
- As-is: current situation.
- Visionary: future system.
- Evaluation: compare alternatives.
- …
**Use case**: document specific functionality (planned or existing). diagram (UML).
- Diagram (UML): actors and (inter)actions
- Phrasing: verb phrase for use case title. not more than 1 page but complete. active voice. causal relationship. clear system boundaries.
## Object Modelling
**Find important abstractions iteratively.**
**Find objects**
1. identify classes: application domain (experts), syntactic (base on use cases), design patterns (apply design knowledge), component-based (existing solutions).
	- Abbott's Technique: map grammatical structure to UML elements (proper noun>object, improper noun>class, …)
2. identify attributes
3. identify operations
4. identify associations
**Identify class types**
- Entity: real world entities (e.g., customer, toy).
- Control: real world procedures (e.g., shopping, recommendation).
- Boundary: interface artefacts (e.g., shop).
## Dynamic Modeling
_Describe components with interesting dynamic behaviour._
**Sequence diagrams**: interaction between objects.
- Elements: object, lifeline, activation box, actor, messages.
- Detect operations: flow of events in use case. Find sender and receiver for event.
- Fork diagram: usually control object, knows all other objects and uses them.
- Stair diagram: each object delegates to other objects, only knows a few others.
- Identify temporal relationships.
**State diagrams**: one for each interesting class.
- State machines: Moore and Mealy.
- Elements: state, event connectors with guards.
- State: particular condition at a specific time.
- Identify changes to individual object over time.
## Validation and Verification
**Validation** (what): building right system? stakeholders agree?
- Goal analysis: use cases satisfy requirements?
- Robustness analysis: class model satisfies use cases?
- Consistency checking: code corresponds to model?
- Techniques and tools: completeness, consistency, refinement, model checking.
- Review: correct? complete? consistent? unambiguous? realistic?
**Verification** (how): building system right? design/implementation meet requirements?
## Requirements Specification
**Software requirements specification** (SRS) is document that describes what and how.
- introduction: purpose, scope, definitions, references, overview.
- overall description: product, function, users, constraints, assumptions.
- specific requirements.
**Requirements patterns**: for multiple projects, similar contexts, different units of same company, strict standards
- **Rupp's templates**: autonomous, user interaction, system interface
	- {when?}
	- the system
	1. shall {process} (legally binding)
	2. should provide {whom?} with the ability to {process} (strongly recommended)
	3. will be able to {process} (used in future)
	- {object}
	- {object details}
 - **easy approach requirements syntax EARS templates**: 
	 - ubiquitous: The {system} shall {response}.
	 - event-driven: WHEN {trigger} {optional precondition} the {system} shall {response}.
	 - unwanted: IF {unwanted condition}, THEN the {system} shall {response}.
	 - state-driven: WHILE {state}, the {system} shall {response}.
	 - optional: WHERE {feature}, the {system} shall {response}.
	 - complex: combinations.
#
---
[patterns](patterns.pdf)
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
# Testing & Quality Patterns
## Quality Patterns
*Quality cannot be defined formally.*
**Errors**: made by developers (syntax, grammar, algorithmic).
**Fault**: can cause improper functioning of the system.
**Failure**: fault that becomes observable.
**Smells**: Low level design problems, quick to identify, not always problematic.
**Refactoring**: changes that do not change observable behaviour. depends on tests.
**SOLID**: Single Responsibility, Open-Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.
### Continuous Integration
*merge working copies regularly, automatedly and enable continuous deployment.*
**Build Patterns**: when? (for every change), how granular? (task-level), recognise? (tag/label).
**Build Management patterns**: efficiency? (automate), automate? (scripts).
**Build Quality Patterns**: baseline? (automated tests), stable? (smoke tests), not stable? (fail on project rule violation, notify).
**Metrics**: code-level (object-oriented, static code attributes, churn metrics), business-level (cost/schedule, user satisfaction).
Continuous Quality: Potential bugs, coding rules, duplications, complexity, test coverage, architecture/design, comments.
## Testing Patterns
### Unit Testing
*Developers confirm that individual component works as expected.*
Concepts
- **Software under test** (SUT): unit of interest.
- **Test case**: description of test to be performed. Includes input data and oracle mechanism (pass/fail).
- **Test harness**: framework for running tests under varying conditions and monitoring. Includes test driver and reporting.
**FIRST**: fast, independent, repeatable, self-validating, thorough.
**AAA**: arrange, act, assert.
**for MVC**: view-state test and model-state test.
**JUnit**: Java testing framework.
**Mock Object Pattern**: Observability and controllability difficult due to dependencies $\to$ Mocking.
**Dependency Injection**: low coupling but high cohesion.
**Test-driven development**: write test before implementation, fail the test, write code, pass the test, refactor.
1. Red bar patterns
- starter test: first test should be trivial.
- one step test: next test should teach something.
- learning test: write test for new external API.
- regression test: smallest possible test to verify a bug.
- child test: break large test into smaller test. learning: why was it too big?
1. Green bar patterns
- fake it: return a constant as first implementation.
- triangulation abstract only when you have two or more examples.
- obvious implementation: just implement if you know how.
### System Testing
*Developers confirm that interfaces among subsystems work as expected.*
### Integration Testing
*Developers confirm system meets the (non-)functional requirements.*
### Acceptance Testing
*Clients confirm system meets the requirements and is ready to use.*
**User stories** as communication means. Can also be broken down into scenarios.
**GWT template**: given when then.
Behaviour driven development: focus on simple language across teams and on when/who.
# More Patterns
## Collaboration Patterns
## UX Patterns