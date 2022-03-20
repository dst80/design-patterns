## Abstract Factory

An abstract factory combines the responsibilities of "summarizing object generation in one place", "Separate the responsibility of creation and usage of an object" and "possibility for abstract constructors".

```plantuml
@startuml abstract_factory
!theme plain

skinparam nodesep 50
skinparam ranksep 50
object "**client**" as client
together {
object "//**Abstract Factory**//" as AbstractFactory {
    CreateProductA
    CreateProductB
}
    object "**Concrete Factory 1**" as ConcreteFactory1{
        CreateProductA
        CreateProductB
    }
    object "**Concrete Factory 2**" as ConcreteFactory2 {
        CreateProductA
        CreateProductB
    }
}
together {
    together {
        object "//**Abstract Product A**//" as AbstractProductA
        object "**Product A1**" as ProductA1
        object "**Product A2**" as ProductA2
    }
    together {
        object "//**Abstract Product B**//" as AbstractProductB
        object "**Product B1**" as ProductB1
        object "**Product B2**" as ProductB2
}
}
client --> AbstractFactory
client --> AbstractProductA
client --> AbstractProductB

AbstractFactory <|-- ConcreteFactory1
AbstractFactory <|-- ConcreteFactory2

AbstractProductA <|--- ProductA1
AbstractProductA <|--- ProductA2
AbstractProductB <|---- ProductB1
AbstractProductB <|---- ProductB2

ConcreteFactory1::CreateProductA ..> ProductA1 
ConcreteFactory1 ..> ProductB1
ConcreteFactory2::CreateProductA ..> ProductA2
ConcreteFactory2 ..> ProductB2
@enduml
```

### Usage

The abstract factory is used when

* a system should work independently on how its products are created, composed and represented.
* a system should be configured with one or more product families.
* a group of products is designed to be used together, and not needed to enforced this constraints
* the interfaces of products are to be provided in a class library without their implementation.

***Advantages:***

* the client is isolated from concrete classes
* the exchange of product families is possible in a simple manner

***Disadvantage:***

* using concrete functions it is difficult to add new product types as changes have to be made in all concrete factories.

> The disadvantage can be reduced in some cases by decoupling the concrete creation functions with a single one. This decouples the creation process even more, since the decision rests entirely with the factory. However, this only makes sense if the offered interface is sufficient for the consumer.
