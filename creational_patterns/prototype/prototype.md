## Prototype

Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype

```plantuml
@startuml prototype
!theme plain

skinparam nodesep 50
skinparam ranksep 40
hide circle
hide fields

class "**Client**" as client {
    Operation ()
}
note left of client::Operation
 p = prototype->Clone ()
end note

together {
    interface "**Prototype**" as prototype {
        Clone()
    }
    together {
        class "**ConcretePrototype1**" as concrete_prototype_1 {
            Clone()
        }
        class "**ConcretePrototype2**" as concrete_prototype_2 {
            Clone()
        }

        note bottom of concrete_prototype_1
            return copy of self
        end note
        note bottom of concrete_prototype_2
            return copy of self
        end note
    }
    prototype <|-- concrete_prototype_1
    prototype <|-- concrete_prototype_2
}
client -> prototype : "prototype"

@enduml
```

## Usage

Use Prototype pattern when a system should be independent of how products are created, composed and presented; and

* when the classes to instantiate are specified at run-time, e.g by dynamic loading
* when building the classes of factories parallels the class hierachy of products
* when instances of a class can have one of few combination states. Therefore using prototypes can reduce the overhead of instanciating the classes manually.
* when coping of a class depends on it's state.

