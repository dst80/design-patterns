## Abstract Factory

An abstract factory combines the responsibilities of "summarizing object generation in one place", "Separate the responsibility of creation and usage of an object" and "possibility for abstract constructors".

```plantuml
@startuml abstract_factory
!theme plain
hide circle
hide fields
hide members

skinparam nodesep 50
skinparam ranksep 50
class "**client**" as client
together {
    interface "**Abstract Factory**" as abstract_factory {
        CreateProductA()
        CreateProductB()
    }
    show abstract_factory members
    class "**Concrete Factory 1**" as concrete_factory_1{
        CreateProductA()
        CreateProductB()
    }
    show concrete_factory_1 members
    class "**Concrete Factory 2**" as concrete_factory_2 {
        CreateProductA()
        CreateProductB()
    }
    show concrete_factory_2 members
    abstract_factory <|-- concrete_factory_1
    abstract_factory <|-- concrete_factory_2
}

together {
    together {
        class "**Abstract Product A**" as abstract_product_A
        class "**Product A1**" as product_A1
        class "**Product A2**" as product_A2
    }
    together {
        class "**Abstract Product B**" as abstract_product_B
        class "**Product B1**" as product_B1
        class "**Product B2**" as product_B2
    }
    abstract_product_A <|---- product_A1
    abstract_product_A <|--- product_A2
    abstract_product_B <|---- product_B1
    abstract_product_B <|--- product_B2
}
client --> abstract_factory
client --> abstract_product_A
client --> abstract_product_B

concrete_factory_1::CreateProductA ..> product_A1 
concrete_factory_1::CreateProductB ..> product_B1
concrete_factory_2::CreateProductA ..> product_A2
concrete_factory_2::CreateProductB ..> product_B2
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
