# Architecture

the architecture should serve its users, and hence must be adapted first to the skills and needs of the programmers actually working with it.

## General

define error processing:
- corrective (try to continue) / detective (fail)
- active (plausibility checks) / passive (fail if no way to continue)
- propagation (fail at first invalid input or after checking all)
- consistent error messages

be aware of the stability of the environment and take precautions (experimental technologies need a time buffer to account for bugs in tooling).

define code style, tool chain, testing approach (TDD or similar) and definition of done. use conventions to prevent religious wars.

## Subsystems

abstracts messy details from common types of subproblems away from the other modules.

common subsystems include business rules (laws, regulation, prices), UI (GUI / command line), I/O access (database), system dependencies (syscalls, exec calls)

## Domain driven design

eases the development by introducing knowledge about the business process in the application naming / class concept, down to the database.

Entities are transformed to fit the domain they are using in (for example, while accounting needs the address of a person, the authentication only needs username/password).

A developer now only needs to understand the domain he is currently working in, and can ignore the other parts of the application. Naming of variables and hierarchic structures can be adjusted to the business case. At the same time, other parts of the application can evolve easily in their respective domain, as their changes (like new fields, objects) need not to be propagated into other domains.

The downsides include the maintenance of the transformation logic and alignment efforts when business terminology changes.

## Microservices

decouples parts of the application in separate services connected via a REST interface.

The services expose a REST interface to be accessed by the other services. Internally, the services may differ in architecture, database, technology, ...

This setup eases updates, as single services can be replaced one after another. If a service of a specific type is behind a load balancer, it is also possible to use more or less instances of said service depending on the demand.

The downsides include that services may never be able to change their interface once specified, as they do not know which services use it.

## Event sourcing

formulate all changes in event. interested parties listen to specific events and update their local state accordingly.

all events are saved, and can be replayed to reproduce bugs or recalculate state after a bugfix.

## CQRS (command query responsibility segregation)

separate the command and query model, unlocking the ability to optimize each model for their specific use cases.

the command model updates the database according to user commands.

the query model gather data from the database for display.

## Command / Event separation

separate commands (actions which modify state) and events (results of such actions) to ease scalability.

Commands are created to perform changes in the database or execute other actions. The command handler, upon completion, publishes events with the result of the modification which are received by all interested parties.

This setup allows to separate applications/components which modify state (those who execute the business logic attached to a specific command) from application which only need to process state (those who display to the user or evaluate data).

The commands can also be stored for auditing purposes, effectively giving a chain of actions executed by a user independent of the origin of such a command.

It eases domain driven design, as the event handlers which contain the new state are the perfect access point to transform the received entities from possible other parts of the application to the structure the active domain fits best.

The downsides include similar problems than with most distributed systems; reordering of events or consistency issues if an event is lost or not processed fully yet (one command may provokes multiple different events, which themselves have again side effects the user has to wait for). Similar to services, it is also unclear (by design!) which components consume the events and commands.

To battle the downsides, carefully design how the events/commands transfer is setup, for example using a message queue which provides the required properties. Avoid complex events/commands and exposing domain-private information to avoid having to propagate changes inside the domain to others.

## Onion

use layers to separate different kind of logic (presentation, business, domain).

The Domain layer is the innermost layer, containing entities and, if DDD is used, some of the logic to apply changes to those entities. The next outer layer is the domain service layer, providing together with the application service layer the business features. The outermost layer contains the IO, like presentation or database access.

If strict layering is used, then the outer layer may only access the next inner layer. If loose layering is used, then an outer layers may access any inner layer. It is never allowed to reverse the call chain; if logic from the outside is needed, an interface implementation can be requested by the inner layer.

This design eases separation of concern, ease testing and makes it easier to replace a layer if necessary. The strict layering makes these advantages even more strict.

The downsides include that mapping efforts may increase substantially; the same entity may exist in multiple layers and needs to be mapped each time it is passed to an inner layer (as this layer is not allowed to access the outer source).

To battle the downsides, allow loose layering (at the cost that it is easier for an outer layer to access/modify something from an inner layer it is not supposed to). 

## Hexagonal (adapter & ports)

structure the application around use cases which fully define how they interact with the environment (both in- and output).

The business logic sits inside the "hexagon". It defines interfaces to interact with the outside. These touch points with the outside are composed of ports (an interface) and adapters (an implementation of that interface). As the inside defines the interfaces, it does not have any dependency to the outside.

Advantages of that approach include that a use case can be separated cleanly from others, and makes structuring the application by use case easy. It is easily testable as dependencies from a single use cases can be mocked simply. To replace dependencies from a single use cases is easy, hence even larger technology migrations can be done incrementally without touching the business logic.

The downsides include that for each hexagon, many potentially similar entities (and hence mappings) need to be created. Also, many very specific interfaces need to be implemented.

To battle the downsides, you may include multiple similar use cases in the same hexagon. If abstracted properly pure technicalities may also be shared by multiple hexagons.
