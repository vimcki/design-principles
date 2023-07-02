# Abstraction

## Information

Abstraction is contract between implementations. It consists of

1. interfaces,
1. structures used by interfaces, 
1. errors that functions in interfaces return,
1. enums/consts that are a part of interfaces.

No logic should be implemented on the abstraction level. Specifically, this implies that no functions should be defined on structures(with receiver, sometimes called methods) used in functions defined by interfaces.

## Example

This example break the rules of abstraction. It defines a function on a structure used by an interface. User is no longer abstract.

```go
type User struct {
	ID string
	Name string
	Age int
}

type UserRepository interface {
	Get(id string) (User, error)
}

func (u *User) CanBuyAlcohol() bool {
	return u.Age >= 18
}
```

Problem here is that you can't dynamically choose how CanBuyAlcohol works:
1. you can't have two deployments that use different drinking checks.
1. you can't have two different implementations that are selected based on where the request comes from.

Instead you should define a function that takes a user and returns a bool, and if you need customization you can define that function on a structure that holds additional information.