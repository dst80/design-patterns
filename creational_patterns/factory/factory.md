## Factory Pattern

```plantuml
@startuml simple_factory
!theme plain
left to right direction
skinparam nodesep 20
skinparam ranksep 50
object "**Factory**" as Factory {
    CreateProductA
    CreateProductB
}

together {
    object ProductA
    object ProductB
}
Factory::CreateProductA ..> ProductA : create
Factory::CreateProductB ..> ProductB : create
@enduml
```

A factory is a class that generates objects through a function call instead of creating the object through a constructor. The factory serves as a rallying point for creating similar objects that can be grouped together as part of their affiliation (eg. ProductA and ProductB).

The following advantages result from the separation of the object generation and it's usage

* Unified generation of the object (for all consumers)
* Replacing the generation of the object is easy
* Changes in object generation only affect the factory, not its consumers
* Less coupling between the generated object and its comsumers

```plantuml
@startuml factory_with_interface
!theme plain
left to right direction
skinparam nodesep 20
skinparam ranksep 50
object "**Factory**" as Factory {
    IProductA CreateProductA
    IProductB CreateProductB
}

together {
    together {
        object "**//IProductA//**" as IProductA
        object "**ProductA**" as ProductA
    }
        together {
        object "**//IProductB//**" as IProductB
        object "**ProductB**" as ProductB
    }
}
Factory::CreateProductA ..> ProductA : create
Factory::CreateProductB ..> ProductB : create

IProductA <-- ProductA
IProductB <-- ProductB
@enduml
```

By introducing interfaces as returning types from the factory, the coupling can further reduced.
Using a unified CreateFunction (e.g. CreateProduct) that creates the appropriate object via a parameter (enum or string) decouples the object even more, since the decision rests entirely with the factory. However, this only makes sense if the offered interface is sufficient for the consumer.
A complete decoupling, however, can only realized with the abstraction of the factory itself "see Abstract Factory".
