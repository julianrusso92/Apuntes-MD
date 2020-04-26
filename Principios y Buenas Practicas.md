# Principios y buenas practicas

## Don't repeart yourself (DRY)

## SOLID

- Single Responsability
- Open/Closed
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

### Single Responsability Principle

> There should never be more than one reason  for a class to change. - Robert Martin

### Open/ClosePrinciple

> States that software entities (classes, modules, functions, ...) should be open for extension, but closed for modification.

- **Open to Extension:** New behavior can be added in the future.
- **Closed to Modification:** Changes to sources or binary code are not required.

### Liskov Substitution Principle

> States that subtypes must be substitutable for their base type.

#### Common Refactorings

- Collapse Hierarchy
- Pull Up / Push Down Field
- Pull Up / Push Down Method

### Interface Segregation Principle

> State that Clients should not be forced to depend on method they do not use.

#### Common Refactorings

- Extract Interface

### Dependency Inversion Principle

> Hight-level modules should not depend on low-level modules. Both should depend on abstractions.
> Abstractions shoud not depend on details. Details should depend on abstraction.

- **Depend on Abstractions**: Interfaces, not concrete types.
- **Inject dependencies** into classes.
- **Structure Solution so Dependencies flow toward Core.**

#### Common Refactorings

- Extract class
- Extract Interfaces / Apply Strategy Pattern
- Extract Method
- Introduce Service Locator / Container

