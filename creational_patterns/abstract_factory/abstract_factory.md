## Abstract Factory

An abstract factory combines the responsibilities of "summarizing object generation in one place", "Separate the responsibility of creation and usage of an object" and "possibility for abstract constructors".

```plantuml
@startuml AbstractFactory
left to right direction
skinparam ranksep 50
skinparam nodesep 50
skinparam class {
  FontSize 13
  AttributeFontSize 13
  FontStyle bold
  BackgroundColor transparent
  BorderColor black
}
skinparam arrow {
  Color black
  FontColor black
  Thickness 2
}
skinparam note {
  BackgroundColor transparent
  BorderColor black
}
hide circle
hide fields
hide members

interface AbstractFactory {
  CreateProductA()
  CreateProductB()
}
show AbstractFactory members

class ConcreteFactory1 extends AbstractFactory{
  CreateProductA()
  CreateProductB()
}
show ConcreteFactory1 members

class ConcreteFactory2 extends AbstractFactory {
  CreateProductA()
  CreateProductB()
}
show ConcreteFactory2 members

together {
  class AbstractProductA
  class ProductA1 
  class ProductA2 
  AbstractProductA <|--- ProductA1 
  AbstractProductA <|--- ProductA2 

}
together {
  class AbstractProductB
  class ProductB1 
  class ProductB2
  AbstractProductB <|--- ProductB1 
  AbstractProductB <|--- ProductB2 
}
    
class client
client --> AbstractFactory
client --> AbstractProductA
client --> AbstractProductB

ConcreteFactory1::CreateProductA ..> ProductA1 
ConcreteFactory1::CreateProductB ..> ProductB1
ConcreteFactory2::CreateProductA ..> ProductA2
ConcreteFactory2::CreateProductB ..> ProductB2
@enduml
```

### Usage

The abstract factory is used when

* a system should work independently on how its products are created, composed and represented.
* a system should be configured with one or more product families.
* a group of products is designed to be used together, and not needed to enforced this constraints
* the interfaces of products are to be provided in a class library without their implementation.

#### Advantages

* the client is isolated from concrete classes
* the exchange of product families is possible in a simple manner

#### Disadvantage

* using concrete functions it is difficult to add new product types as changes have to be made in all concrete factories.

> The disadvantage can be reduced in some cases by decoupling the concrete creation functions with a single one. This decouples the creation process even more, since the decision rests entirely with the factory. However, this only makes sense if the offered interface is sufficient for the consumer.
