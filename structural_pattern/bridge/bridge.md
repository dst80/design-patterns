## Bridge Pattern

Bridges decouple the Abstraction from its implementation so that the two can vary independently.


```plantuml
@startuml bridge
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

class Client
hide Client members
together {
  interface Abstraction {
      Operation()
  }
  class RefinedAbstraction extends Abstraction
}
hide RefinedAbstraction members

together {
  interface Implementor {
      OperationImpl()
  }
  class ConcreteImplementorA extends Implementor {
      OperationImpl()
  }

  class ConcreteImplementorB extends Implementor {
      OperationImpl()
  }
}
note left of Abstraction::Operation
    Operation -> OperationImpl ()
end note

Client --> Abstraction
Abstraction *-> Implementor : impl

@enduml
```

Used nomenclature for bridges are:

* **Abstraction**
  * defines the Abstraction interface
  * maintaines a reference to an object of type *Implementation*
* **Refined Abstraction**
  * extends the interface defined by the *Abstraction*
* **Implementor**
  * defines the interface for implementation classes. This interface doesn't have to correspond exactly *Abstraction* interface. Typically the *Implementator* interface provides only primitive operations, and Abstraction defines higher-level operations based on these primitives
* **ConcreateImplementor**
  * implementation the *Implementor* interface and defines its concrete implementation.

### Usage

Bridges can be used when

* a permanent binding between an Abstraction and its implementation should be avoided. For example, to switch or replace the implementation during runtime.
* both the abstractions and their implementations are to be subclassable. The bridge pattern allows different abstractions and implementations to be combined and expanded independently of one another.
* changes in the implementation of an Abstraction should habe no impact to the Client
* the implementation on an actraction should be completely hidden for the Client (e.g. c++)

#### Advantages

* Decoupling interface and implementation, so that implementation is no longer bound to the interface itself.
* interface and implementation can very independently.
* improved extensibility
* hiding the implementation details from the client.

#### Disadvantages

* additional layer of abstraction can make it difficult for developers to follow the chain of execution.
