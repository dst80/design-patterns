## Adapter

Converts a class's interface into another interface client expects. Adapter classes therefore allow classes that otherwise cannot work together because they have incompatible interfaces.

Adapters can be created using inheritance or using composition.


```plantuml
@startuml adapter_by_inheritance
skinparam ranksep 50
skinparam nodesep 50
skinparam Title {
  FontSize 16
  FontStyle bold
}
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

Title Adapter pattern using inheritance

class client
hide client members

class Target {
    Request()
}

class Adaptee {
    SpecificRequest ()
}

class Adapter extends Target, Adaptee {
    Request ()
    SpecificRequest ()
}

note right of Adapter::Request
    SpecificRequest ()
end note


client -> Target
@enduml
```

```plantuml
@startuml adapter_by_composition

skinparam ranksep 50
skinparam nodesep 50
skinparam Title {
  FontSize 16
  FontStyle bold
}
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

Title Adapter pattern using composition

class client
hide client members

class Target {
    Request()
}

class Adapter extends Target {
    Request ()
    adaptee
}
show Adapter fields

note right of Adapter::Request
    adaptee.SpecificRequest ()
end note

class Adaptee {
    SpecificRequest ()
}

client -r--> Target
Adaptee <--o Adapter : adaptee
@enduml
```

The nomenclature is

* **Target**
  * defines the domain specific interface that *Client* use
* **Client**
  * collaborates with objects conforming to the *Target* interface
* **Adaptee**
  * defines exising interface that need adapting
* **Adapter**
  * adapts the interface of the *Target* with the interface of the *Adaptee*

### Usage

Use Adapter pattern when

* when an existing class is to be used, but the interface of the class does not match the required interface.
* to create a reusable class that interoperates with unrelated or unexpected classes, that is, classes that don't necessarily have compatible interfaces.
* multiple existing subclasses will need to be used, but it is impractical to customize the interface by subclassing all of them. An object Adapter can customize the interface to its parent class.

#### Advantages

Class Adapter:

* Adapter can override some of Adaptee`s behavior
* No pointer indirections because Class Adapter requires a concrete adapter as member.

Object Adapter:

* A single adapter can handle Adaptee`s subclassing

#### Disadvantages

Class Adapter:

* Adapter for each Adaptee subclass is required.

Object Adapter:

* Overriding some of Adaptee`s behavior becomes hard, because it will influence all Adaptees implementations
* Pointer indirections
