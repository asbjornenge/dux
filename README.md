# Dux

> DANGER: Novice at work! Incomplete nonsense.

Dux is a service oriented architecture for [Docker](https://www.docker.com/) inspired by [Flux](https://facebook.github.io/flux/). Dux is both a design and a reference implementation. The design is not tied to Docker, but the reference implementation uses Docker as it's component model. 

## Core Components

At it's core Dux has a **StateStore**, a **Dispatcher**, a **Scheduler** and a **ServiceDiscovery** component.

![core](core.mermaid.png)

There is no technical distinction between Dux components and application components, they are all made from the same mold.

### StateStore

The [StateStore]() is a fundamental part of Dux. It declaratively holds the state for your services. Whenever some state changes the StateStore will trigger events notifying all subscribing servies that this state has changed. New services can also request any current state.

With a nice UI on top, the StateStore can act as a editable configuration store for your cluster.

Examples of state:

* Hosts
* Containers
* DNS
* Secrets

### Dispatcher

The [Dispatcher]() is responsible for distributing messages from publishers to subscribers. Any service can act as publisher or subscriber to any message channel. This flexibility allows the design to grow dynamically. Application components are free to 
