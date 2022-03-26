## Facade Pattern

The Facade defines a higher-level interface that makes the subsystem easier zu use.

```plantuml
@startuml Facade
skinparam nodesep 50
skinparam ranksep 50
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
skinparam package {
    Style rectangle
}

hide circle
hide fields
hide members

class "  Facade  " as Facade 

client1 --> Facade
client2 --> Facade
client3 --> Facade

package "subsystem classes" as subsystem {
    together {
        class "                   " as a1 
        class "                   " as a2 extends a1
        class "                   " as a3 extends a1
    }
    together {
        class "                   " as b1 
        class "                   " as b2 extends b1
    }    
    together {
        class "                   " as c1
        class "                   " as c2
        c1 --[hidden] c2
        b1 -- c2
    }
}
Facade -> a2
Facade -> b2
Facade --> c1
Facade --> c2
@enduml
```

Used nomenclature for Facade is:

* **Facade**
  * knows the subsystem classes and which are responsible for a request
  * delegate request to the appropriate subsystem objects
* **subsystem classes**
  * implement subsystem functionality
  * handle the work by the Facade object.
  * have no knowledge of the Facade

### Usage

Use the Facade pattern when

* provide simple interface for complex subsystems.
* reduce the complexity of the interaction in the subsystem for clients
* reduce the dependencies between client and and the subsystem
* when layer different subsystems

#### Advantages

* shields the complexity of subsystems from the client
* promote weaker coupling between clients and subsystem

#### Disadvantages

* does not protect the application to use the subsystem directly without the Facade
* Facade can become a "god" class or difficult to test if the subsystems is huge.
