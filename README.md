# Dux

> DANGER: Novice at work! Incomplete nonsense.

Dux is an architecture for distributed systems inspired by [Flux](https://facebook.github.io/flux/). Dux is both a design and a reference implementation. The reference implementation uses [Docker](https://www.docker.com/) as it's component model. 

In Dux, a **component** is an isolated bucket of bits; our building blocks. A **service** is a logical unit of one or more components. Expect these terms to be used inconsistently with this definition. 

## Core Services 

At it's core Dux has a **StateStore**, a **Dispatcher**, a **Scheduler** and a **Discovery** service.

![core](core.mermaid.png)

There is no technical distinction between Dux components and application components, they are all made from the same mold. It is important to note that while these services drive Dux itself, they are also intended for use by your applications. 

### StateStore

The [StateStore](/) is a fundamental part of Dux. It declaratively holds the state for your services. Whenever some state changes the StateStore will trigger events notifying all subscribing services that this state has changed. New services can also request any current state.

With a nice UI on top, the StateStore can serve as a editable configuration store for your cluster.

Examples of state:

* Hosts
* Containers
* DNS
* Secrets

### Dispatcher

The [Dispatcher](/) is responsible for distributing messages from publishers to subscribers. Any component can act as publisher or subscriber to any message channel. Messages will be broadcast to all subscribes of that channel. This flexibility allows the system to grow dynamically.

### Scheduler

The [Scheduler](/) is responsible for managing components. It gets a list of *components* and *hosts* from the StateStore and makes decisions about where to run those components. It can both add and remove components.

### Discovery

The [Discovery]() service is there to facilitate components discovering each other. There is a multitude of ways to implement service discovery. The reference implementation of Dux uses a [DNS](http://en.wikipedia.org/wiki/Domain_Name_System) based service discovery solution. This has the benefit that most current software (and us humans) are accustomed to using DNS for service discovery.
