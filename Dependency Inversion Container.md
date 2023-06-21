# Dependency Inversion Container

## Information

Dependency Inversion Container is a [Facade](https://github.com/vimcki/design-principles/blob/master/Facade.md) between executables and internal modules of an application. It is a step of a runtime when implementations of interfaces are selected based on configuration of application. It happens before launching real processing.

This step allows for [feature switching](https://github.com/vimcki/design-principles/blob/master/Feature%20Switch.md) without modifying the code and rebuilding it.

For more information about Dependency Injection see [Dependency Inversion Principle](https://github.com/vimcki/design-principles/blob/master/Dependency%20Inversion%20Principle.md).

## Example

Set of components used in executable:
```go
type Set struct {
  Service domain.Service
  DebugRepo func() ([]byte, error)
}
```

Executable that uses Set of components to create a web server:
```go
func main() {
  cfg := ...

  set := components.Build(cfg)

  ...

  router.POST("/api/v1/service", set.Service.HttpHandler)
  router.POST("/debug/get_all", asHttpHandler(set.DebugRepo))

  ...
}
```

Implementation of the container:
```go
func Build(cfg Config) Set {
  ...

  postgresRepo := postgres.NewRepository(...)
  ...

  var searcher FullTextSearcher

  switch cfg.Searcher {
    case: "elasticsearch":
      searcher = elastic.NewSearcher(...)
    case: "solr":
      searcher = solr.NewSearcher(...)

  service := serviceimplementation.NewService(searcher, repository)

  return Set{
    Service: service,
    DebugRepo: postgresRepo.GetAll,
  }
}
```
Here we can see that the implementation of the searcher is selected based on the configuration of the application, we can:

1. do AB tests,
1. easily turn off features that depend on unstable backing services during outages,
1. rollback to non experimental and more stable implementation,
1. deploy application for different business clients with different backing services,
1. run the application with mocks/logs for debugging or testing.

## Resources 

- [Inversion of Control Containers and the Dependency Injection pattern - Martin Fowler](https://martinfowler.com/articles/injection.html)
