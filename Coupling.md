# Coupling

## Information

Coupling is the degree to which one module relies on another module. High coupling between two modules might lead to changes in one affecting the other. This makes code harder to maintain. Low coupling is often a sign of a well-structured code. Its achived by using [Abstraction](https://github.com/vimcki/design-principles/blob/master/Abstraction.md) and following [Open Closed Principle](https://github.com/vimcki/design-principles/blob/master/Open%20Closed%20Principle.md). "Low Coupling, High [Cohesion](https://github.com/vimcki/design-principles/blob/master/Cohesion.md)" is often a slogan for well structured code. Less coupling is better but you have to have some coupling, so not all of it is bad, just bad coupling is bad.

## Types of Coupling

If you look on the internet there are many types of coupling. Here are some of them, from highest coupling to lowest:

1. Content Coupling: Modules are directly dependent on each other's internal implementation details, such as accessing and modifying each other's variables or data structures.

1. Common Coupling: Modules share a global data element or common resource, and any changes to that shared element can affect multiple modules. This type of coupling can make it difficult to understand and maintain the code.

1. Control Coupling: Modules communicate through passing control information, such as flags or status variables, to indicate the flow of execution. While control coupling is better than content coupling, it still implies some level of dependency between modules.

1. Stamp Coupling: Modules share a composite data structure, but only use a part of it. This type of coupling occurs when modules receive a large data structure but only access specific elements within it.

1. Data Coupling: Modules communicate by passing data through parameters or arguments. The dependency is limited to the data being passed, and modules do not rely on each other's internal details.

1. Message Coupling: Modules communicate by sending messages, typically using a well-defined interface. The modules are loosely coupled, as they rely on a predefined message format rather than direct knowledge of each other.

1. No Coupling: Modules are completely independent of each other and do not rely on shared data or communication. This is the ideal level of coupling, as it promotes modular, reusable, and maintainable code.

## Example

### Content Coupling

Here service package is directly dependent on mongo package.

```go
package service

import "repository/mongo"

func (s *Service) GetUsers() ([]User, error) {
	repo := mongo.NewRepo(s.host, s.username, s.password)

	users, err := repo.GetUsers()
	...
}
```

This is not good. Problems:

1. we can't change underlying service(mongo) without changing service package,
1. we can't test service package without running mongo,
1. we can't reuse service package with other database,
1. service package has to know about host, username, password,
1. if we would like to move from host, username, password to connection string we would have to change service package, we relay on mongo package implementation details.

Solution would be to use [Abstraction](https://github.com/vimcki/design-principles/blob/master/Abstraction.md), in this case repository interface and [dependency incject](https://github.com/vimcki/design-principles/blob/master/Dependency%20Inversion%20Principle.md) concrete implementation of repository.

## Resources

- [Design Principles and Design Patterns - Robert C. Martin](http://staff.cs.utu.fi/~jounsmed/doos_06/material/DesignPrinciplesAndPatterns.pdf)
- [wiki](https://en.wikipedia.org/wiki/Coupling_(computer_programming))

#value