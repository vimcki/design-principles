# Feature Switch

## Information

Feature switch, also known as feature flag or feature toggle, is a technique in software development that turns certain features of your application on or off at runtime. This enables developers to modify system behavior without changing code, and it is often used for A/B testing, canary releases, or to safely roll out features to specific user groups or environments. Feature switches allow for greater control and risk mitigation during software release processes.

## Example

In this example we have a repository that fetches articles from a database. We want to add a cache to this repository. We can use a feature switch to enable or disable the cache at runtime.

```go
package main

...

func main() {
	// load configuration from file or env vars	
	cfg := configuration.Load()

	...

	var repo repository.Article

	repo = mongo.NewArticleRepository(...)

	// based on configuration we either use a cache or not
	if cfg.CacheEnabled { 
		repo = cache.NewRepository(repo, cfg.CacheExpiration)
	}

	// here repo is either a mongo repo or a cache
	// repo wrapping a mongo repo

	...

```

## Resources

- [Feature Toggles (aka Feature Flags) - Martin Fowler](https://martinfowler.com/articles/feature-toggles.html)
- [wiki](https://en.wikipedia.org/wiki/Feature_toggle)
