# Open Closed Principle

## Information

The Open-Closed Principle (OCP) is a software design principle that suggests that classes, modules, and functions should be open for extension but closed for modification. This means that you should be able to add new features or behaviors to your software without changing the existing code.

You should make sure that it is easy to add new functionality without having to modify the existing code. This allows you to add new features or behaviors to your software without introducing bugs or breaking existing functionality.

The OCP encourages developers to create code that is easy to maintain and update over time. By following this principle, you will make your code more [ready for change](https://github.com/vimcki/design-principles/blob/master/Ready%20for%20Change.md) and [reusable](https://github.com/vimcki/design-principles/blob/master/Reusability.md). 

[Dependency Inversion Principle](https://github.com/vimcki/design-principles/blob/master/Dependency%20Inversion%20Principle.md) describes a way to achieve OCP.

## How to spot violation

1. [Abstraction](https://github.com/vimcki/design-principles/blob/master/Abstraction.md) and implementations are in same module
1. Importing anything other than abstraction or external stuff(`/pkg`, libraries) inside of implementations in `/internal`
1. Switch statements are suspicious, are you absolutely sure that you wont need to add new case in the future? Switches can be replaced with map lookups, which are more extensible and make code more data-driven

## Resources

- [Design Principles and Design Patterns - Robert C. Martin](http://staff.cs.utu.fi/~jounsmed/doos_06/material/DesignPrinciplesAndPatterns.pdf)

#principle
