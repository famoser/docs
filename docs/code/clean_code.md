# Clean code

## Basic architecture

- Separate I/O classes (designed for persistance) from functional classes (designed for business) [13]
- Use stateful respositories to provide functional classes to the outside and process I/O classes in the inside [15, d]
- Use services to encapsulate functionality, stateless if business, possibly stateful if I/O [d]
- Use DI Container [1, 8, 17, c] or a factory to inject dependencies

## Workflow

- Continuously refactor when implementing new functionality [11, 18, c]
- Be humble (dont fight tools/framework/business/team) [16, 17, 18]

## Global

- single minimal purpose [2, 3, 7, 9, 14]
- same level of abstraction [2, 3, 4, 7, 8, 12]
- higher level of abstraction uses next lower (never the other way) [8, 19, b]

## Classes

- inheritance as means of specialization (use patterns for code-reuse) [6, a]
- inject implementation specific dependencies (like Logger, Storage) using the constructor. [1]
- no state unless Naming / Pattern explicitly requires (`CacheService` or similar). [1]

## Methods

- use only injected dependencies of class (no global calls) & passed data (use `Payload` class if many arguments needed). [1, 12]

## Properties

- expose only properties needed for transfer, not for decisions (instead include decisions directly in class) [13, 14]

## Literature 

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

https://deviq.com for principles & patterns