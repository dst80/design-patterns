## Factory Pattern

Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantioation to subclasses.

```plantuml
@startuml factory
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

skinparam nodesep 25
skinparam ranksep 50
class ProductConsumer

class Factory {
    CreateProduct()
}
show Factory members
hide Factory fields

ProductConsumer -d-> Factory : " invoke"


note right of ProductConsumer
Product product = factory.CreateProduct ()
end note

note right of Factory::CreateProduct
return new ConcreteProduct ()
end note

interface Product
class ConcreteProduct extends Product

Factory -l-> ConcreteProduct : create


@enduml
```

### Usage

Use Factory Method pattern when

* a class can't anticipate the class of objects it must create
* a class wants its subclasses to specify the objects it creates
* classes delegate responsibility to one of several helper subclasses, and want to localize the khnowledge of which helper subclass is the delegate.

#### Advantages

* more separation of responsibility (way to SRP and DI)
* unify the generation of objects (for all consumers)
* creation knowlegde should be stored at one place
* changes in object generation only should effect the factory but not the consumers.

#### Disadvantages

* more code to write
* Creation process is slower
