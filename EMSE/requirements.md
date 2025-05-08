[[requirements.pdf]]
# Motivation
_difficult to elicit good requirements, but fixing problems early is cheap._
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
# Requirements Elicitation

* **Soft skills**: analytics thinking, empathy, communication, conflict resolution, moderation, confidence, persuasiveness.
* Discover needs and acquire knowledge about: stakeholders, expectations, current state, domain, tasks, system/context.
* **Sources**: Stakeholders, documents, systems in production.
## Stakeholders
_Involved in and affected by our project._
* **Characteristics**: expectations, importance, their requirements.
* **Population sampling**: non-probability (specific selection), probability (equal chance), convenience (easy access), sequential (iterative), snowball (subjects recommend subjects).
## Methods
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