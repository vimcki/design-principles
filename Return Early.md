# Return Early

## Information

When writing functions make sure to return early. This will help you avoid deeply nested if statements and make your code easier to read. Which makes it easier to [maintain](https://github.com/vimcki/design-principles/blob/master/Ready%20for%20Change.md).

## Example

Good:
```go
func doSomething(a string) (string, error) {
	x, err := doSomethingElse(a)
  err != nil {
		return "", err
	}

	y, err := doAnotherThing(x)
  if err != nil {
		return "", err
	}
	z := doSomethingElseAgain(y)

	return z, nil
}
```
Bad:
```go
func doSomething(a string) (string, error) {
	x, err := doSomethingElse(a)
	if err == nil {
		y, err := doAnotherThing(x)
		if err == nil {
			z := doSomethingElseAgain(y)
			return z, nil
		}
	}

	return "", err
}
```
