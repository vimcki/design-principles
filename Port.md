# Port(Hexagonal Architecture)

## Information

Port is entry/exit point to/from [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md). Entry point ports are a set of interfaces that define the operations the application can perform. Exit point ports define external resources that application will require to work. Ports are a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md). Entry point ports are used by [input adapters](https://github.com/vimcki/design-principles/blob/master/Adapter.md). Implementations of exit poits are called [output adapters](https://github.com/vimcki/design-principles/blob/master/Adapter.md).

## Examples

Note that in the examples below, argument structs are defined in the same package as the interface.

Entry points:

```golang
type InputGraph struct{
	...
}

type OutputGraph struct{
	...
}

type Translator interface{
  Translate(InputGraph) (OutputGraph, error)
}
```

```golang
type BidRequest struct{
	...
}

type BidResponse struct{
	...
}

type Bidder interface{
  Bid(BidRequest) (BidResponse, error)
}
```

```golang
type UpdateRequest struct{
	...
}

type User struct{
	...
}

type Updater interface{
  Update(UpdateRequest) (User, error)
}
```

Exit points:

```golang
type User struct{
	...
}

type Repository interface{
  GetUser(id string) (User, error)
}
```

```golang
type Query struct{
	...
}

type Result struct{
	...
}

type Search interface{
  Search(Query) (Result, error)
}
```

## Resources

- its a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md), so look there