# Abstraction

## Information

Abstraction is contract between implementations. It consists of

1. interfaces,
1. structures used by interfaces, 
1. errors that functions in interfaces return,
1. enums/consts that are a part of interfaces.

No logic should be implemented on the abstraction level. Specifically, this implies that no functions should be defined on structures(with receiver) used in interfaces.
