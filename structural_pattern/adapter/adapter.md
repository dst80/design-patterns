## Adapter

Converts a class's interface into another interface client expects. Adapter classes therefore allow classes that otherwise cannot work together because they have incompatible interfaces.

Adapters can be created using inheritance or using composition. The nomenclature is

* **Target**
  * defines the domain specific interface that *Client* use
* **Client**
  * collaborates with objects conforming to the *Target* interface
* **Adaptee**
  * defines exising interface that need adapting
* **Adapter**
  * adapts the interface of the *Target* with the interface of the *Adaptee*

---

***Adapter pattern using inheritance***

```plantuml
@startuml adapter_by_inheritance
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

---
***Adapter pattern using composition***

```plantuml
@startuml adapter_by_composition
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

---

### Usage

Use Adapter pattern when

* when an existing class is to be used, but the interface of the class does not match the required interface.
* to create a reusable class that interoperates with unrelated or unexpected classes, that is, classes that don't necessarily have compatible interfaces.
* multiple existing subclasses will need to be used, but it is impractical to customize the interface by subclassing all of them. An object Adapter can customize the interface to its parent class.