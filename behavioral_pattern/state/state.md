## State

Allow an object to alter its behavior when its internal state changes. An Object will appear to change its class.

```plantuml
@startuml pull_observer
skinparam ranksep 100
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

class Context {
    Request()
    state
}

show Context fields

together {
    class State {
        Handle()
    }

    class ConcreteStateA extends State {
        Handle()
    }

    class ConcreteStateB extends State {
        Handle()
    }

    class ConcreteStateC extends State {
        Handle()
    }
}
Client -> Context
Context o-> State 
@enduml
```

the nomenclature for State Pattern is:

* ***Context***
  * defines the interface the client can use.
  * handles the request from the client based on the current concrete state it carries

* ***State***
  * defines the interface for encapsulating the behavior assosiated with a particular state of the context.
* ***ConcreteState***
  * implements the bahavior of the current state towards the state interface.

### Usage

Use State pattern when

* an object behavior depends on its state and it must change its behavior at run-time depending on that state
* operations have large, multipart conditional statements that depend on the object state.

#### Advantages

* It localizes state-specific behavior and partitions behavior for different states
  * All behaviors of one state in one object
* It makes state transitions explicit
* State objects can be shared

#### Disadvantages

* Transition encapsulation can result in unexpected behavior, Therefore should be avoided in State pattern design
* state structures can grow and become to complex. In this cases state structures should be subdivided
