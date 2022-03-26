## Memento

Without violating encapsulation, capture and externalize the internal state of objects, so that the object be restored to this state later.

```plantuml
@startuml memento
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

together {
    class Originator {
        SetMemento(ConcreteMemento)
        CreateMemento()
        state
    }

    note left of Originator::SetMemento
        state = memento.GetState()
    end note

    note left of Originator::CreateMemento
        return new Memento(state)
    end note
}

interface Memento {
    GetState()
    state
}

class ConcreteMemento extends Memento{
    SetState(state)
    GetState()
    state
}

class Caretaker {}
hide Caretaker members
hide Caretaker fields

Originator .> ConcreteMemento 
Memento <-o Caretaker
@enduml
```

Used nomenclature for Memento Pattern is:

* ***Memento***
  * Stores the internal state of the Originator, so that even the state in the Originator is changed over time the stored state can be set back.
  * protect the state against other objects than the Originator. E.g. the Caretaker see only a narrowed interface in comparison to the Originator

* ***Originator***
  * implements cooperative behavior by coordinating Colleague objects.
  * knows and maintains its colleagues.
* ***Caretaker***
  * is responsible for the memento`s safekeeping
  * never operates on or examine the content of the memento

### Usage

Use the Memento pattern when

* a snapshot of the current state of the Originator is required, so that this snapshot can be restored to a later state.

#### Advantages

* It simplifies the Originator to store its state
* Can keep track of the state of the Originator and reset the states 

#### Disadvantages

* Using Mementos might be expensive depending which states are required to store, because the state is copied every time a memento is created.
* defining narrow and wide interface can be difficult in some languages
* Hidden costs in storing and track keeping for the memento in the caretaker
