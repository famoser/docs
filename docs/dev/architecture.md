# Architecture

How to structure a program to be developed, used and maintained by many?

## Domain driven design

eases the development by introducing knowledge about the business process in the application naming / class concept, down to the database.

Entities are transformed to fit the domain they are using in (for example, while accounting needs the address of a person, the authentication only needs username/password).

A developer now only needs to understand the domain he is currently working in, and can ignore the other parts of the application. Naming of variables and hierarchic structures can be adjusted to the business case. At the same time, other parts of the application can evolve easily in their respective domain, as their changes (like new fields, objects) need not to be propagated into other domains.

The downsides include the maintenance of the transformation logic.

## Microservice architecture

decouples parts of the application in separate services connected via a REST interface.

The services expose a REST interface to be accessed by the other services. Internally, the services may differ in architecture, database, technology, ...

This setup eases updates, as single services can be replaced one after another. If a service of a specific type is behind a load balancer, it is also possible to use more or less instances of said service depending on the demand.

The downsides include that services may never be able to change their interface once specified, as they do not know which services use it.

## Event sourcing

separates commands (actions which modify state) and events (results of such actions) to ease scalability.

Commands are created to perform changes in the database or execute other actions. The command handler, upon completion, publishes events with the result of the modification which are received by all interested parties.

This setup allows to separate applications/components which modify state (those who execute the business logic attached to a specific command) from application which only need to process state (those who display to the user or evaluate data).

The commands can also be stored for auditing purposes, effectively giving a chain of actions executed by a user independent of the origin of such a command.

It eases domain driven design, as the event handlers which contain the new state are the perfect access point to transform the received entities from possible other parts of the application to the structure the active domain fits best.

The downsides include similar problems than with most distributed systems; reordering of events or consistency issues if an event is lost or not processed fully yet (one command may provokes multiple different events, which themselves have again side effects the user has to wait for). Similar to services, it is also unclear (by design!) which components consume the events and commands.

To battle the downsides, carefully design how the events/commands transfer is setup, for example using a message queue which provides the required properties. Avoid complex events/commands and exposing domain-private information to avoid having to propagate changes inside the domain to others.