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

metadata=Explore the role of Domain Objects in software design, particularly as the entities used by Business Logic. Understand the recommendation to define these objects in abstract modules. View a practical example of a simple User struct, a common type of Domain Object in many applications.
