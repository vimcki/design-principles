# Input Adapters(Hexagonal Architecture)

## Information

Input Adapters, also known as driving or secondary, are implementation of the entry points of the application like HTTP/gRPC handlers, UI, or tests. They are responsible for calling [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md) using [ports](https://github.com/vimcki/design-principles/blob/master/Port.md), often translating requests from the outside world into [Domain Objects](https://github.com/vimcki/design-principles/blob/master/Domain%20Objects.md). 

Often used input adapters:

1. server - http, grpc, websockets, graphQL, ...
1. queue workers - kafka, rabbitmq, ...
1. tests,
1. console commands,
1. UI.

Input Adapters are kind of [Adapter](https://github.com/vimcki/design-principles/blob/master/Adapter.md) and they are part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md).

![Hexagonal Architecture](/images/hex.svg)

## Examples

All examples below are implementations of input adapters.

### Server

HTTP handler for graph translation:

```golang
func (h *Handler) Translate(rw http.ResponseWriter, req *http.Request){
  inputGraph, err := h.converter.Convert(req.Body)
  if err ...

	// calling into Business Logic using port(interface)
  outputGraph, err := h.translator.Translate(inputGraph)
  if err ...

  writeResponse(rw, outputGraph)
}
```

```golang
// main
handler := handlerTranslator.New(...)
router.POST("/translate", handler.Translate)
```

### Command

Console command for graph translation:

```golang
// main
...
data, err := os.ReadFile(cfg.GraphPath)
if err ...

var inputGraph domain.InputGraph

err := json.Unmarshal(data, &inputGraph)
if err ...


// calling into Business Logic using port(interface)
outputGraph, err := translator.Translate(inputGraph)
if err ...

fmt.Prinln(outputGraph)
```

### Tests

This is part of a testing suite responsible for creating mocks and running the Consume [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md):

```golang
func (f *apiFeature) processTheMessage() error {
  dpRepoMock, segmentRepoMock := createMocks(...)

  set := build.FlexibleSet(
      f.cfg, dpRepoMock, segmentRepoMock,
  )

  message := attribute.AttrChangeMsg{}

  err := json.Unmarshal([]byte(f.message), &message)
  if err ...

	// calling into Business Logic using port(interface)
  return set.Consumer.Consume(message)
}
```

## Resources

- its a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md), so look there
