# Creational Patterns

[[Singleton]]: Ensures a class has only one instance and provides a global point to access it.

[[Factory Method]]: Defines an interface for creating an object, but allows subclasses to alter the type of objects that will be created.

[[Abstract Factory]]: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

[[Builder]]: Separates the construction of a complex object from its representation.

[[Prototype]]: Creates new objects by copying an existing object

## Decision Tree
```mermaid
graph TD

Start[Start] --> Question1{Many optional and<br> required object fields?}

Question1 -->|Yes| Builder[Builder Pattern]
Question1 -->|No| Question2{Is only one object<br> instance allowed?}


Question2 -->|Yes| Singleton[Singleton Pattern]
Question2 -->|No| Question3{Will object type be<br>decided at runtime?}

Question3 -->|Yes| Factory[Factory Method or<br>Abstract Factory Pattern]
Question3 -->|No| Prototype[Prototype Pattern]
```
