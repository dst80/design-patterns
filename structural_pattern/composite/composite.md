## Composite pattern

Assembles objects into tree structures to represent part-whole hierarchies. Composite allows clients to treat individual objects and compositions of objects consistently.

* **Component**
  * declares the interface for objects in the compostion
  * implements default behavior for the interface common to all classes as appropriate
  * declares an interface for accessing and managing its child components.
  * (optional) defines an interface for accessing a component's parent in recursive structure, and implements it if that's appropiate.
* **Leaf**
  * represents leaf objects in the composition. A leaf has no problems
  * defines behavior for primitive objects in the composition
* **Composite**
  * defines behavior for components having children
  * stores child components
  * implements child-related operations in the Component interface.
* **Client**
  * manipulates objects in the composition through the Component interface.

```plantuml
@startuml composite
!theme plain
skinparam nodesep 50
skinparam ranksep 50
hide circle
hide fields
class "**Client**" as client {}
hide client members

interface "**Component**" as component {
    Operation ()
    Add (Component)
    Remove (Component)
    GetChild (int)
}
together {
    class "**Leaf**" as leaf {
        Operation()
    }
    class "**Composite**" as composite {
        Operation()
        Add(Component)
        Remove(Component)
        GetChild(int)
    }

    note right of composite::Operation
        forall g in children
            g.Operation()
    end note 

    component <|--d leaf
    component <|--d composite
}

client -r--> component
component::Operation <--o composite : children
@enduml
```

### Usage

Use the composite pattern when

* part-whole hierachies of objects should be represented
* clients should be able to ignore the difference between compositions of objects (Composite) and individual objects (Leaf). Clients will use both type of objects in a composite structure uniformly

#### Advantages

* client can be simple
* client has not to be changed when adding new Composite elements
* Compose complex objects based on simple ones
* easy to create new kinds of Composite elements
* simple and general design

#### Disadvantages

* hard to restrict composition (Composition of an object limited by a specific set of Components)
* complex objects are hard to analyse for a specific Component
* loosing type safty on compile type for the components.

> In the case of the periodic processing of components of the composite, the composite pattern has the disadvantage that each composite must first be searched for the component before the component can be processed. This can be time-consuming for large objects. It is therefore advisable to switch to the Entity Component System Pattern (ECS) for such problems. Here the component is decoubled from the entity and will be processed in the system.
