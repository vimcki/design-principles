
# Output Adapters(Hexagonal Architecture)

## Information

Output Adapters, also known as driven or secondary, manage interactions of the application with outside world, that is databases, queues, requests, external APIs, etc. Their job is to translate [Domain Objects](https://github.com/vimcki/design-principles/blob/master/Domain%20Objects.md) into external format, for example into database model. Then they do the interaction, and lastly they translate results back into [Domain Objects](https://github.com/vimcki/design-principles/blob/master/Domain%20Objects.md). Output adapters implement exit point [ports](https://github.com/vimcki/design-principles/blob/master/Port.md)

By isolating these external interactions in separate adapters, the core business logic remains clean, and changes in external technologies have minimal impact on the core.

Output Adapters are kind of [Adapter](https://github.com/vimcki/design-principles/blob/master/Adapter.md) and they are part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md).

## Example

In this example [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md) needs to update user data. It uses [Port](https://github.com/vimcki/design-principles/blob/master/Port.md) to do so. 

```golang
// some business logic package
type Updater struct {
  repo repository.User
}

func (u *Updater) Update(ud domain.UpdateData) (domain.User, error) {

  // do some business logic
  // for example validate ud

  return p.repo.Update(ud)
}
```

And this is how [Port](https://github.com/vimcki/design-principles/blob/master/Port.md) looks like:

```golang
package repository

type User interface {
  Update(domain.UpdateData) (domain.User, error)
}
```


Here we have output adapters for mongo, it implements interface above:

```golang
package mongo

func (r *Repo) Update(ud domain.UpdateData) (domain.User, error){
  query, err := generateQuery(ud)
  if err ...

  userModel, err := r.client.Do(query)
  if err ...

  return toDomain(userModel)
}
```

But we can implement any other output adapter, for example one that prints data to stdout for debugging or reduction in infrastructure requirements for development. Other reason we might implement this before real database adapter is that we want to push deciding which database we want to use to later stages of development.

```golang
package stdout

type Repo struct {}

func (r *Repo) Update(ud domain.UpdateData) (domain.User, error){
  fmt.Println(ud)

  return domain.User{}, nil
}
```

## Resources

- its a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md), so look there
