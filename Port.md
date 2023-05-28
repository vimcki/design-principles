# Port(Hexagonal Architecture)

## Information

Port is entry/exit point to/from [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md). Entry point ports are a set of interfaces that define the operations the application can perform. Exit point ports define external resources that application will require to work. Ports are a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md). Entry point ports are used by [input adapters](https://github.com/vimcki/design-principles/blob/master/Adapter.md). Implementations of exit poits are called [output adapters](https://github.com/vimcki/design-principles/blob/master/Adapter.md).

## Examples

In examples there is package called domain used to emphesize that arguments and return values are [Domain Objects](https://github.com/vimcki/design-principles/blob/master/Domain%20Objects.md). In practice they probably should be defined in the same module as ports.

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

## Resources

- its a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md), so look there

metadata=This page dives into the concept of Ports in Hexagonal Architecture, explaining how they act as entry and exit points to and from Business Logic. It distinguishes between Entry Point Ports and Exit Point Ports, outlining their roles and usage within Input and Output Adapters. It also provides code examples to illustrate how these concepts work in practice, with emphasis on the use of Domain Objects in these operations. A must-read for anyone interested in understanding the intricacies of Hexagonal Architecture.
