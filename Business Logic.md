# Business Logic

## Information

Business Logic is the part of an application that models the real-world business rules that determine how data can be created, stored and changed. The other part of an application consists of [adapters](https://github.com/vimcki/design-principles/blob/master/Adapter.md). Entry and exit points to Business Logic are called [ports](https://github.com/vimcki/design-principles/blob/master/Port.md). Business logic operates on [Domain Objects](https://github.com/vimcki/design-principles/blob/master/Domain%20Objects.md).

## Example

```golang
func validateUsername(username string) bool {
	if len(username) < 3 || len(username) > 20 {
		return false
	}
	if containsSpecialCharacters(username) {
		return false
	}
	return true
}
```

## Resources

- [wiki](https://en.wikipedia.org/wiki/Business_logic)
