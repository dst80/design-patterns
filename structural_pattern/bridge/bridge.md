## Bridge

Bridges decouple the abstraction from its implementation so that the two can vary independently.

Used nomenclature for bridges are:

* **Abstraction**
  * defines the abstraction interface
  * maintaines a reference to an object of type *Implementation*
* **Refined Abstraction**
  * extends the interface defined by the *Abstraction*
* **Implementor**
  * defines the interface for implementation classes. This interface doesn't have to correspond exactly *Abstraction* interface. Typically the *Implementator* interface provides only primitive operations, and Abstraction defines higher-level operations based on these primitives
* **ConcreateImplementor**
  * implementation the *Implementor* interface and defines its concrete implementation.

---

```plantuml
@startuml bridge
!theme plain
skinparam nodesep 50
skinparam ranksep 50
hide circle
hide fields

class "**Client**" as client
hide client members
together {

interface "**Abstraction**" as abstraction {
    Operation()
}


class "**Refines Abstraction**" as refined_abstraction
}
hide refined_abstraction members

together {
interface "**Implementor**" as implementor {
    OperationImpl()
}
class "**Concrete Implementor A**" as concrete_implementor_A {
    OperationImpl()
}

class "**Concrete Implementor B**" as concrete_implementor_B {
    OperationImpl()
}
implementor <|-- concrete_implementor_A
implementor <|-- concrete_implementor_B
}
note left of abstraction::Operation
    Operation -> OperationImpl ()
end note

client --> abstraction
abstraction <|-- refined_abstraction
abstraction *-> implementor : impl

@enduml
```

---

### Usage

Bridges can be used when

* a permanent binding between an abstraction and its implementation should be avoided. For example, to switch or replace the implementation during runtime.
* both the abstractions and their implementations are to be subclassable. The bridge pattern allows different abstractions and implementations to be combined and expanded independently of one another.
* changes in the implementation of an abstraction should habe no impact to the client
* the implementation on an actraction should be completely hidden for the client (e.g. c++)
 
