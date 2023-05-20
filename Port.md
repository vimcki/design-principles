# Port

## Information

Port is entry/exit point to/from [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md). It is a set of interfaces that define the operations the application needs to perform. Ports are a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md)

## Examples

In examples there is package called domain used to emphesize that arguments and return values are domain objects. In practice they probably should be defined in the same module as ports.

Entry points:

```golang
type Translator interface{
	Translate(domain.InputGraph) (domain.OutputGraph, error)
}
```
```golang
type Bidder interface{
	Bid(domain.BidRequest) (domain.BidResponse, error)
}
```
```golang
type Updater interface{
	Update(domain.UpdateRequest) (domain.User, error)
}
```

Exit points:

```golang
type Repository interface{
	GetUser(id string) (domain.User, error)
}
```
```golang
type Search interface{
	Search(query domain.Query) (domain.Result, error)
}
```
