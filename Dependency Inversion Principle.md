# Dependency Inversion Principle

## Information
Dependency inversion principle(DIP) states that high-level modules should not depend on low-level modules. Both should depend on [abstractions](https://github.com/vimcki/design-principles/blob/master/Abstraction.md).

The idea is to reduce the [coupling](https://github.com/vimcki/design-principles/blob/master/Coupling.md) between modules, it leads to code being [easier to change](https://github.com/vimcki/design-principles/blob/master/Ready%20for%20Change.md).

DIP is a way to achive [Open Closed Principle](https://github.com/vimcki/design-principles/blob/master/Open%20Closed%20Principle.md)

## Example

If we have service that needs repository to work we can inject any implementation of it:
```
real repository, like mongo or postgres
mock repository for testing
logging repository for debugging without using real database
file repository for some static data
...
```

In this example we have service that needs repository to work. We can inject any implementation during [assembling of components](https://github.com/vimcki/design-principles/blob/master/Dependency%20Inversion%20Container.md)

```go
// abstract module
type Repository interface {
	...
}
```

```go
// service implementation
type Service struct {
	repository Repository
}

func NewService(repository Repository) *Service {
	return &Service{repository: repository}
}

func (s *Service) DoSomething(...) {
	s.repository.DoSomethingElse(...)
}
```

```go
func buildService(cfg Config) Service{
	var repository Repository

	swich cfg.RepositoryType {
	case "mongo":
		repository := mongo.NewRepository(cfg.MongoStuff)
	case "postgres":
		repository := postgres.NewRepository(cfg.PostgresStuff)
	case "logging":
		repository := logging.NewRepository()
	}

	return serviceimplementation.NewService(repository)
}

```

## Resources

- [Design Principles and Design Patterns - Robert C. Martin](http://staff.cs.utu.fi/~jounsmed/doos_06/material/DesignPrinciplesAndPatterns.pdf)

#principle
