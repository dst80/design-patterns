## Prototype

Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype

```plantuml
@startuml
!theme plain

skinparam nodesep 50
skinparam ranksep 40

object "**Client**" as Client {
    Operation ()
}
note left of Client
 p = prototype->Clone ()
end note

together {
    object "//**Prototype**//" as Prototype {
        Clone ()
    }
    together {
        object "//**ConcretePrototype1**//" as ConcretePrototype1 {
            Clone ()
        }
        object "//**ConcretePrototype2**//" as ConcretePrototype2 {
            Clone ()
        }

        note bottom of ConcretePrototype1
        return copy of self
        end note
        note bottom of ConcretePrototype2
        return copy of self
        end note
    }
    Prototype <|-- ConcretePrototype1
    Prototype <|-- ConcretePrototype2
}
Client -> Prototype : prototype

@enduml
```

## Usage

Use Prototype pattern when a system should be independent of how products are created, composed and presented; and

* when the classes to instantiate are specified at run-time, e.g by dynamic loading
* when building the classes of factories parallels the class hierachy of products
* when instances of a class can have one of few combination states. Therefore using prototypes can reduce the overhead of instanciating the classes manually.
* when coping of a class depends on it's state.

