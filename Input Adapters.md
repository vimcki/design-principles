# Input Adapters(Hexagonal Architecture)

## Information

Input Adapters are implementation of the entry points of the application like HTTP/gRPC handlers, UI, or tests. They are responsible for initiating interactions with the [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md) using [ports](https://github.com/vimcki/design-principles/blob/master/Port.md), often translating requests from the outside world into [Domain Objects](https://github.com/vimcki/design-principles/blob/master/Domain%20Objects.md). 

Often used input adapters:

1. server - http, grpc, websockets, graphQL, ...
1. queue workers - kafka, rabbitmq, ...
1. tests,
1. console commands,
1. UI.

Input Adapters are kind of [Adapter](https://github.com/vimcki/design-principles/blob/master/Adapter.md). They are part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md).

## Examples

### HTTP handler

HTTP handler for graph translation:

```golang
func (h *Handler) Translate(rw http.ResponseWriter, req *http.Request){
	inputGraph, err := h.converter.Convert(req.Body)
	if err ...

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

### Console command

Console command for graph translation:

```golang
// main
...
data, err := os.ReadFile(cfg.GraphPath)
if err ...

var inputGraph domain.InputGraph

err := json.Unmarshal(data, &inputGraph)
if err ...


outputGraph, err := translator.Translate(inputGraph)
if err ...

fmt.Prinln(outputGraph)
```

### Tests

Part of a [behavioural testing](https://github.com/vimcki/design-principles/blob/master/Behavioural%20tests.md) suite responsible for creating mocks and running the Consume [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md):

```golang
//bdd_test.go
func (f *apiFeature) iProcessTheMessage() error {
	dpRepoMock, segmentRepoMock := createMocks(...)

	set := build.FlexibleSet(
	    f.cfg, dpRepoMock, segmentRepoMock,
	)

	message := attribute.AttrChangeMsg{}

	err := json.Unmarshal([]byte(f.message), &message)
	if err ...

	return set.Consumer.Consume(message)
}
```

## Resources

- its a part of [Hexagonal Architecture](https://github.com/vimcki/design-principles/blob/master/Hexagonal%20Architecture.md), so look there
