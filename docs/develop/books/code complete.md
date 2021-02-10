# Software development process

construction site analogy

- skyscraper needs different approach than simple shed
- to rebuild a house with a different architecture is expensive
- to move a wall to another place is expensive due to the labour it requires, not due to the materials
- prebuilt components like dishwashers are bought or expensively reinvented
- planning and building can be done in stages (like foundation and interior details)
- changes to a load bearing wall are much more expensive than to a simple room divider
- if a skyscraper is build, some precautions / safety margins have to be made to reduce risk
- there are many different ways to build a house so it needs to be clearly defined how its supposed to look like
- quality is nearly invisible, but saves much money in the long run
- continuous maintenance avoids having to reconstruct the whole house after 10 years

to start a software project you need a clear vision about what problem will be solved.
this helps the team to align, enables "common sense" and generates a multitude of solution.

## work effective

work in iteration that are as small as possible while still providing some business benefit.  
the reduced complexity speeds up exponentially and the focus can shift much quicker.  
reduce iteration size further with high risk, complex applications, inexperienced team and changing circumstances.

scaling is not linear; it is much less efficient. people write less code with more error in more time. construction activity decreases and instead design, integration, architecture & testing need more effort.

encourage good coding by letting a though leader set standards, best practices or guidelines- ensure at least two people work on the same code, review all changes and ensure collective ownership of code & responsibility is take seriously.

products need to be polished more than simple tools, systems need to have more careful interfaces than products.
as more people work on the same, more potential connections need to be made & more potential conflicts need to be resolved & the need for more formal documentation increases.

effectiveness changes due to setup (documentation, tools), people (skills, experience, continuity), product (complexity, speed & storage constrains, size of data), project management (early failure detection effectiveness, customer relationship, quality/clarity of requirements, risk management).

orders of magnitude are between a top programmer and an underperforming one (1:10 and more). bad teams need 3.5 times more time than good ones, and attract even more bad programmers (and vice-versa). a quiet, private, interruption-free and big office doubles productivity.

scaling tips:

- use trunk based development to avoid merging hell  
- limit WIP to detect & resolve bottlenecks  
- use central test data management for easier e2e test setup

## iteration

define specific, verifiable goals to get close to the vision.  
analyze the risks with the goals to archive.  
define the required quality of user interaction, design and architecture (experimental, MVP, market-ready?).  
gather first use cases and analyze how to introduce, maintain and sunset the tool.  

work out high level specification with wireframes to align how these goals should be reached.  
structure the project to reduce the risks early.  
choose concrete approaches to reach the required quality.  
sketch deployment pipeline, organize support and continuous maintenance.

estimate the time needed to implement and the requirements and align with availabilities.  
adjust the development practices according to the scale of the project.

scale utilities:

- code reviews
- clear responsibilities
- architecture planning
- design reviews
- more rigid requirements
- formal change control
- requirement reviews
- deployment procedure
- test planning
- different QA team

## requirements engineering

requirements as a whole should produce a ready-to-use product (use cases, inputs, outputs), not conflict with each other and in a language/granularity that is consistent and understood by users / third parties.
they may also contain non-functional requirements as response time, error recovery, maintainability.
each requirement should be relevant to the problem, technically feasible and testable.

explicit requirements can be approved by users (rather than chosen by the programmer), avoid arguments and can detect conceptual issues early.
but they may also prevent taking a shorter path to the target detected while implementing (for example a different export format which is easier to implement).

requirements can change anytime, but the changing business value, cost and schedule have to be considered wisely.
if requirements change often, introduce formal procedure to make process transparent and scalable.

## estimation

estimate duration at low level (few hours) and take the time to do it properly. multiply with factor depending on unknowns, but minimally x1.2. use appropriate unit to communicate accuracy of whole estimation.

prioritize according to (sum of business value + risk reduction + opportunity enabler factor) / duration.

for easier estimates, ask someone who has done it before, work in iterations or use relative estimation between all available items.

## design

use believable test data to increase understandability (hence avoid lorem ipsum).

## develop

relax; only publish solid, tested code under any circumstance, never lower the bar of minimal quality, especially not under error-prone, high-pressure situations: short-term benefits are not worth the risk and cost of the long-term.

if tests are needed, write them as soon as the public interface is ready.

for non-obvious bugs, always advance using hypothesis (not blindly bruteforcing), list things to try and always work on most promising one, check code that has changed recently/often, discuss with someone else or simply take a break.

for low-level performance improvements, order case statements by frequency, create lookup array instead of if/else constructs for multiple deciding factors, simplify loops (take if/else outside), combine loops that iterate over same data, unroll loops (take multiple steps in same iteration), use faster arithmetic, remove method calls, choose different data types/structures, reduce array dimensions, reduce array/object accesses, use caching & precompute expensive calculations.

document surprises (like performance improvements, workarounds) and what can not be expressed by code (like special math operations), focusing on the why not the how.

## quality assurance

formally define the prioritization of the quality objectives, and use guidelines/best practices, informal/formal reviews & external audits to implement it. while quality assurance needs more time upfront, it does not increase the total cost because it leads to software with fewer defects (less time spent on support).

external quality metrics (user perceived) are correctness, integrity (access control & data sanity), usability, reliability (few failures), efficiency, adaptability (fit for different purposes), accuracy (fit for purpose) & robustness (functioning under invalid input).

internal quality metrics (developer perceived) are understandability (high-level structure), maintainability, testability, readability (statement level), reusability, flexibility & portability.

use a combination of prototyping, design/code reviews, unit/integration/e2e testing & regression/system testing to archive acceptable fault levels. 

use pair programming, formal reviews (discuss code using clear roles including reviewer, scribe, moderator, author), walk through (present code/concept by the author) and code reviews to educate authors & propagate knowledge and experience.

https://github.com/google/eng-practices for help how to do a PR review

## testing

for unit testing, create test cases according to statement, branch, definition/use pair, loop (0, 1, any) or boundary (min, any, max) coverage (white-box approach). include test cases for dirty (erroneous) cases by using too much, too few or wrongly typed data.

for integration testing, focus on the interaction of the components but avoid to retest the guarantees established by the unit tests (black-box approach).

for e2e testing, focus on complete user interactions representing sensible use cases but avoid to increase coupling.

document for errors how much time they needed to be found, where they are located and what the root cause was (off-by-one, nullRef). bugs tends to be concentrated on specific parts of the software; find those and minimize the impact with refactorings & common-cases-checklists. 
