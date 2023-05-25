# Interface Segregation Principle

## Information

Interface Segregation Principle(ISP) states that when implementation depends upon interface it should use all of its functions.

## Example

In the code below there is a violation of ISP, Service depends on user.Repository but doesn't use Delete function.

```go 
// abstration
package user

type Repository interface {
	Get(id string) (User, error)
	Delete(id string) error
}
```

```go
// service implementation
type Service strutct {
	repo user.Repository
}

// all of the services functions
func (s *Service) Get (...) (...){
	// some business logic
	...
	return s.repo.Get(id)
}
```

And if we split Repository into two Service stops depending on Delete function that it doesn't use

```go 
// abstration
package user

type GetRepository interface {
	Get(id string) (User, error)
}

type DeleteRepo interface{
	Delete(id string) error
}

```
```go
// service implementation
type Service strutct {
	repo user.GetRepository
}

// all of the services functions
func (s *Service) Get (...) (...){
	// some business logic
	...
	return s.repo.Get(id)
}
```

## Resources

- [wiki](https://en.wikipedia.org/wiki/Interface_segregation_principle)
