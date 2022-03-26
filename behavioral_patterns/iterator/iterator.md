## Iterator Pattern

Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representaion

```plantuml
@startuml interator
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
    interface Iterator {
        First()
        Next()
        Current()
        Last()
    }
    class ConcreteIterator extends Iterator {
        First()
        Next()
        Current()
        Last()
    }
}
together {
    interface Aggregate {
        GetIterator()
    }
    class ConcreteAggregate extends Aggregate {
        GetIterator()
    }
    note left of ConcreteAggregate::GetIterator
        return new ConcreteIterator ()
    end note
}

Client -l-> Aggregate
Client -r-> Iterator
ConcreteAggregate -> ConcreteIterator
ConcreteAggregate <. ConcreteIterator
@enduml
```

Used nomenclature for Iterator Pattern is:

* **Interator**
  * defines the interface for accessing and transversing elements.
* **ConcreteIterator**
  * implements the interfaceof the Iterator
  * keep track of the current position in the aggregate.
* **Aggregate**
  * defines interface for getting Iterators
* **ConcreteAggregate**
  * implements the interface of Aggregate
  * contains elements.

### Usage

Iterator pattern is used when

* accessing an aggregate object`s content without exposing its internal representaiton
* multiple traversals of aggregate objects are required or want to be supported
* provide an universal interface for different aggregate structures

#### Advantages

* Support variations in the traversal of an aggregate.
* simplify the aggregate interface
* More than one traversal can be pending on an aggregate.

#### Disadvantages

* Universal interface limits efficient algorithm for specific tasks. (e.g. search in binary and vector are different, but handled the same way using an iterator).

