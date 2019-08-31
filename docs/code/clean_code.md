# Clean code

The single most important guideline is each part of the software should have a single, minimal purpose.
This documents code by the name its method is given, prevents the need for global state, leads to a single source of truth, ensures each loop only does one thing and only a single expression per line is used.

you are doing it wrong if statements are complicated, methods long & nested, names complicated and ambiguous or changes need to be made at multiple locations for a single requirement change. you are doing it wrong if you would be doing it different if you could rewrite it from scratch.

you are doing it right if each line of code is at its single perfect location.

## Basic architecture

- Separate I/O classes (designed for persistance) from functional classes (designed for business) [13]
- Use stateful respositories to provide functional classes to the outside and process I/O classes in the inside [15, d]
- Use services to encapsulate functionality, stateless if business, possibly stateful if I/O [d]
- Use DI Container [1, 8, 17, c] or a factory to inject dependencies

## Workflow

- Continuously refactor when implementing new functionality [11, 18, c]
- Be humble (dont fight tools/framework/business/team) [16, 17, 18]
- Use the best tools available (IDE) and execute its optimization suggestions (remove unused, simplify statements)
- Reuse libraries, patterns, workflows, ...
- Do not assume behavior that is not documented in the interface [C]

improves consistent development speed & integration of all good ideas.

## Global

- single minimal purpose (fewer than 7 local variables, properties, methods, ...) [2, 3, 7, 9, 14]
- use same level of abstraction together [2, 3, 4, 7, 8, 12]
- use shortest name possible (for example do not repeat part of the namespace in class names) [A]
- higher level of abstraction uses only next lower [8, 19, b]
- the level of abstraction hides details of implementation [A, B]
- separate areas likely to change [C]

improves maintainability and reusability.

## Classes

- inheritance as means of specialization (use patterns for code-reuse) [6, a]
- inject implementation specific dependencies (like Logger, Storage) using the constructor. [1]
- stateless unless Naming / Pattern explicitly requires (`CacheService` or similar). [1]

improves high fan-in (many classes use this class) & low fan-out (the class uses itself few others).

## Methods

- use only injected dependencies of class (no global calls) & passed data (use `Payload` class if many arguments needed). [1, 12]
- if processing can not continue, throw an exception (wrap exceptions if necessary to not violate information hiding) [e]
- make parameters read-only and clearly typed (for example add the unit to variable name if not obvious)
- name like verb - object [E]
- minimize local variable lifetime (initialization & all usages) [f]
- single expression per line
- call only methods which affect the outcome (handle "early-out"s in the caller)

### loops

- do loop housekeeping at the end or the start of the loop
- prevent the need for break by factoring out the loop to a method
- prevent the need for continue by filtering the elements beforehand

### booleans

- test positives first
- test normal case first
- parentise boolean expressions
- explicitly compare falsy values
- compare in ranges; MIN < i && i < MAX
- avoid side effects while evaluating

improves testability & predictable errors.

## Properties

- may publicly expose if needed for transfer but not for decision (instead include these directly in class) [13, 14]
- name according to business domain and push modifies (like Sum, Total, ..) at the end of the name if still sensible (for example `first` must be a prefix) [E]
- omit type prefix/suffix, instead use a variable name which clearly indicates the form of the data (like `processingCompleted` which implies only `true`/`false` as value range) [E]

improves single source of truth

## Literature

Included advice
- [A] use abstraction to make a problem simpler
- [B] respect literal & semantic encapsulation (do not expose more than absolutely necessary, do not infer behaviour by looking at implementation)
- [C] separate areas likely to change (ever-changing business rules, unstable environment)
- [D] use patterns to quickly communicate design ideas
- [E] adopt consistency conventions

Included principles:
- [1] Explicit Dependencies Principle
- [2] Separation of Concerns
- [3] Once and Only Once
- [4] Single Responsibility Principle S
- [5] Open/Close Principle -> LOOK UP
- [6] Liskov Substitution Principle L
- [7] Interface Segregation Principle I
- [8] Dependency Inversion Principle D
- [9] Dont repeat yourself DRY
- [10] Tell dont ask TDA
- [11] Boy Scout Rule
- [12] Law of Demeter (only talk to immediate friends)
- [13] Tell Dont Ask
- [14] Encapsulation
- [15] Persistence Ignorance
- [16] You Aint Gonna Need It YAGNI
- [17] Inversion of Control IoC, Hollywood Principle or Dont call us, we call you (let framework dictate application flow)
- [18] Keep it simple KISS
- [19] Stable dependencies

Own principles:
- [a] no manual type checks
- [b] stateless
- [c] do not write boilerplate
- [d] separate I/O from business processing
- [e] do not hide errors
- [f] group related statements together

https://deviq.com for principles & patterns