## Prototype

Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this Prototype

```plantuml
@startuml Prototype
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


class Client {
    Operation ()
}
note left of Client::Operation
p = Prototype->Clone ()
end note

together {
    interface Prototype {
        Clone()
    }
    together {
        class ConcretePrototype1 extends Prototype {
            Clone()
        }
        class ConcretePrototype2 extends Prototype {
            Clone()
        }

        note bottom of ConcretePrototype1
        return copy of self
        end note
        note bottom of ConcretePrototype2
        return copy of self
        end note
    }
}
Client -> Prototype : "Prototype"

@enduml
```

## Usage

Use Prototype pattern when a system should be independent of how products are created, composed and presented; and

* when the classes to instantiate are specified at run-time, e.g by dynamic loading
* when building the classes of factories parallels the class hierachy of products
* when instances of a class can have one of few combination states. Therefore using prototypes can reduce the overhead of instanciating the classes manually.
* when coping of a class depends on it's state.
