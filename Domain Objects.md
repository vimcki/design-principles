# Domain Objects

## Information

Domain objects are objects passed around and operated on by [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md). They should be defined in [abstract](https://github.com/vimcki/design-principles/blob/master/Abstraction.md) modules.

## Example

Simple user struct

```golang
type User struct {
  ID int64
  Name string
  Email string
  Password string
  CreatedAt time.Time
  UpdatedAt time.Time
}
```
