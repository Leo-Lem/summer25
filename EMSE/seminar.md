 ![[assignments.png]]
## Validity
1. Internal: can observed effect be attributed to studied variables?
2. External: how well do the results generalise? (to larger population, other settings, etc.)
3. Construct: is the right thing tested/measured?
4. Conclusion: are conclusions statistically sound?
## [[3. Rahe_FSE_2025.pdf]]: Programming students' GenAI use
- **Problem**: unknown LLM practices by students -> how to work with genai in education?
* **Results**
	* Pass introductory programming course with only chatgpt? Introductory exam could not be passed when using interview-style code review.
	* Strategies when using ChatGPT? Two main strategies: knowledge gaining and generate answers.
	* Delegation and autonomous thinking with ChatGPT? Less critical thinking, often try to stupidly generate answer.
* **Threats to Validity**
	* model volatility and prompt sensitivity
	* language bias: only german
	* selection/participant bias: more confident/higher performing students
	* observer effect: change conduct under observation
	* generalisability: one university, one course
	* limited task scope
	**not addressed in the paper**:
	* tool familiarity: custom gpt interface
	* incentivization effect: more interest in reward than participation
	* assessment influence: quiz-style instead of authentic open-ended coding
	* zero-shot prompting does not fairly model student behavior. also course content like slides should be included for better comparison.
## [[4. Reich_ICSE_2023.pdf]]: Testability Refactoring
* **Problem**: Unstructured refactoring for testability -> less testability than possible.
* **Results**
	* testability PRs v. other PRs? more refactoring, specific types of refactoring.
	* Higher-level testability refactoring patterns? extract method for override/add constructor parameter, for example.
* **Threats to Validity**:
	* sample bias (java, github)
	* manual labelling by single person (60% by multiple)
	* sampling strategy: overrepresents explicit intent PRs due to keyword-search
	**not addressed**:
	* blurred line between testability and general quality PRs.
	* testability only includes unit tests (no integration, system, etc)
	* questionable causation: more refactorings in testability PRs or just generally larger/more complex.
	* unaccounted ecosystem differences (spring, android, cli tools, etc.)
## [[5. Sheth_ICSE_2014.pdf]]: Privacy across regions
* **Problem**: little information about privacy around the world and across groups -> hard to effectively prioritize privacy aspects.
* **Results**
	* Users' privacy and measure understanding? little consensus on best measure.
	* Developers v. users v. different geographic regions? significant differences between developers and geographic regions.
	* Privacy framework basis? e.g. anonymization, data usage, default encryption…
* **Threats to Validity**:
	* selection bias for privacy-interested individuals
	* survey problems: unreliable answers, limited context/depth
	**not addressed**:
	* framing/wording effects: privacy concerns in studies often overstated.
	* event influence: NSA PRISM scandal.
	* overlapping categories: users with dev experience, dev also using.
## [[6. Present]]

## [[7. Sedano_ICSE_2019.pdf]]: Product Backlog
* **Problem**: vague/informal understanding of backlog -> less effective usage.
* **Results**
	* What are product backlogs? informal model of work to be done.
	* What are their roles? boundary object between solution concepts and building software.
	* How do they emerge? sensemaking, context-solution coevolution, boundary spanning.
* **Threats to Validity**:
	* **internal**: insider bias, mitigated by co-author review
	* **external**: Pivotal specific, limited organizational scope.
	* **construct**: possible overfocus on specific roles (designers, managers, developers v. business analysts, UX researches, etc.)
	* **conclusion**: saturation reached late, possibility of underexplored categories.
## [[8. Roehm_ICSE_2012.pdf]]: Program comprehension
* **Problem**: outdated information on developers' program comprehension.
* **Results**
	* Strategies, tools, required information for program comprehension? devs put themselves in end-user role whenever possible, avoid comprehension where possible, standards and experience facilitate.
	* State of the art tools are not used.
* **Threats to Validity**:
	* **internal**: short task duration, task variety, observer bias. mostly mitigated.
	* **external**: non-random sample, but maximised diversity. variety in codebase unknown -> possibly less generalisability.
## [[9. Qiu_ICSE_2019.pdf]]: social capital impact in OSS
* **Problem**: unclear relationship of social capital and participation in OSS.
* **Results**
	* social capital effect on participation? positive, for women diversity required.
	* gender inference for asian languages? 60% min, 83% avg accuracy.
* **Threats to Validity**:
	* **internal**: no inter rater coding for qualitative data.
	* **external**: GH-only, commit only -> potential misrepresentation of divers contributors.
	* **construct**: social capital inferred via structural proxies.
	* **conclusion**: complex modelling choices.
## [[10. Discuss]]

## [[11. Bouraffa_ICSE_2023.pdf]]: Visuo-spatial mental model
* **Problem**: unclear relationship between visuo-spatial mental model and code comprehension.
* **Results**
	* Does spatial code representation influence comprehension? No significant effect.
	* Code canvas influence on comprehension activity distribution? no significant influence.
	* Visuo-spatial working memory and comprehension performance? higher memory reduces time spent on annotating and UI interactions and increases navigation time.
* **Threats to Validity**:
	* **internal**: no fine-grained interaction logging.
	* **external**: small sample size, potential lack of generalisability.
	* **construct**: task realism concerns, reliance on Corsi block test.
	* **conclusion**: acknowledged lack of statistical significance.
