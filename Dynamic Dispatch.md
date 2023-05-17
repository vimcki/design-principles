# Dynamic Dispatch

## Information

Dynamic Dispatch is a step of a runtime when implementations of interfaces are selected based on configuration of application

This allows for [feature switching](https://github.com/vimcki/design-principles/blob/master/Feature%20Switch.md) without modyfing the code and rebuilding it

## Example

```go
func dispatch(cfg Config) Service{
	var searcher FullTextSearcher

	switch cfg.Searcher {
		case: "elasticsearch":
			searcher = NewElasticSearcher(...)
		case: "solr":
      searcher = NewSolrSearcher(...)

	return serviceimplementation.NewService(searcher)
}
```
Here we can see that the implementation of the searcher is selected based on the configuration of the application, we can:

1. do AB tests,
1. easily turn off features that depend on unstable backing services during outages,
1. rollback to non experimental and more stable implementation,
1. deploy application for different business clients with different backing services,
1. run the application with mocks/logs for debugging.


## Resources 

- [wiki](https://en.wikipedia.org/wiki/Dynamic_dispatch)
