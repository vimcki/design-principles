# Single Responsibility Principle

## Information

Single Responsibility Principle states that a class should have only one reason to change. There should be only one potential change in the software's specification that would require a modules source code to be modified. Module should only have one job or responsibility. By ensuring that each module in a system focuses on a single task, the system can be more easily understood, maintained, and expanded. Breaking down a complex system into parts each with a single responsibility enhances modularity and makes it less fragile to changes. If a class has more than one responsibility, it becomes coupled and a change to one responsibility may affect the other, leading to unintended consequences.

This principle is subjective and for one programmer someting breaches SRP and for another it doesn't. A good example might be logging, should logging be in [Business Logic](https://github.com/vimcki/design-principles/blob/master/Business%20Logic.md)? Deciding that logging should not be in business logic leads to ability to, for example, use [Feature Switch](https://github.com/vimcki/design-principles/blob/master/Feature%20Switch.md) to turn it off in hot spots in production while keeping in on while debugging. 

## How to spot violation

There is one exception to this rule, application entrypoint (like `main.go`) where you read arguments, bind various ports, initialise metrics etc.

- single module importing libraries that are not related or on the same level of abstraction, for example `import os` and `import pkg/prometheus`
- module using not related concepts like files, calculating user balances or graph algorithms

## Resources

- just google it, I don't have anything good to share

#principle
