# Don't Repeat Yourself

## Information

The DRY principle states that "Every piece of knowledge must have a single, unambiguous, authoritative representation within a system". This goes for anything:
1. [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md),
1. Documentation,
1. Build scripts,
1. Database schema,
1. Tests.

Sometimes 2 pieces of knowledge have the same representation, its just a coincidence, don't combine them into one if you see "the same" code in 2 places.

## Example

### Two pieces of knowledge with the same implementation(coincidence)

When you have 2 pieces of knowledge for example a username and a post title validations, and they both have the same implementation, but they are not related, don't combine them into one.

Username:

```go
func validateUsername(username string) error {
	if len(username) < 3 || len(username) > 20 {
		return errors.New("username must be ...")
	}
	if !alphanumericRegex.MatchString(username) {
		return errors.New("username must only ...")
	}
	return nil
}
```

Post title:

```go
func validatePostTitle(postTitle string) error {
	if len(postTitle) < 3 || len(postTitle) > 20 {
		return errors.New("post title must be ...")
	}
	if !aplhanumericRegex.MatchString(postTitle) {
		return errors.New("post title must only ...")
	}
	return nil
}
```

If you would combine them and later you buisness rules change, you would have to split them back again or add logic to the function which would make it less readable.

### Breaking DRY principle

```go
// ValidateUsername checks if username length 
// is between 3 and 20 characters and if it 
// contains only alphanumeric characters
func ValidateUsername(username string) error {
	if len(username) < 3 || len(username) > 20 {
		return errors.New("username must be ...")
	}
	if !alphanumericRegex.MatchString(username) {
		return errors.New("username must only ...")
	}
	return nil
}
```

Here we repeat the same piece of knowledge, comment and code both describe user validation. Here its easy to update code if [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md) needs updateing, and forget about updating the comment. Imagine later on someone reads the comment and doesn't read the code...

## Resources

- [Wikipedia](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
- [The Pragmatic Programmer](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-20th-anniversary-edition/)

#principle

metadata=Learn about the DRY (Don't Repeat Yourself) principle and its importance in software development. Understand how every piece of knowledge should have a single, unambiguous representation within a system, including business logic, documentation, build scripts, database schema, and tests. Explore examples illustrating the concept of coincidental similarities and the risks of breaking the DRY principle. Discover the potential pitfalls and benefits of adhering to this principle in your codebase.
