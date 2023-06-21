# Hexagonal Architecture

## Information

Hexagonal Architecture, also known as Ports and Adapters is a design pattern that encourages separation of concerns in an application. The core logic of the application also known as [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md), or the "domain", is placed at the center, and is isolated from external systems (like databases, UI, third-party services) using [ports](https://github.com/vimcki/design-principles/blob/master/Port.md) and [adapters](https://github.com/vimcki/design-principles/blob/master/Adapter.md). This architecture provides a layer of abstraction between [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md) and external systems, enabling the application to be flexible, easy to maintain, and facilitating the independent testing of each component.

By isolating these external interactions in separate adapters, the core [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md) remains clean, and changes in external technologies have minimal impact on the core.

![Hexagonal Architecture](/images/hex.svg)

## Resources

- [wiki](https://en.wikipedia.org/wiki/Hexagonal_architecture_(software))
- [Ports & Adapters Architecture - @hgraca](https://herbertograca.com/2017/09/14/ports-adapters-architecture/)

#pattern
