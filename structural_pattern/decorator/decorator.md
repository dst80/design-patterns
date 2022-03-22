## Decorator
The decorator pattern offers the possibility to dynamically attach additional functionalities and responsibilities to an object. The function of the original object is not extended by subclassing, but by passing the object as a component to the decorator, which contains the additional functionality.

---

```plantuml
@startuml decorator
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
hide circle
hide fields

interface Component {
    Operation()
}
class ConcreteComponent extends Component {
    Operation()
}
abstract Decorator extends Component {
    Operation()
}

ConcreteComponent -r[hidden] Decorator

class ConcreteDecoratorB extends Decorator {
    Operation()
    AddedBahavior()
}
class ConcreteDecoratorA extends Decorator {
    Operation()
    addedState
}
show ConcreteDecoratorA fields

ConcreteDecoratorA -r[hidden] ConcreteDecoratorB

Component <--o Decorator

note right of Decorator::Operation
    component->Operation ()
end note

note right of ConcreteDecoratorB::Operation
    component->Operation ()
    AddedBahavior ()
end note
@enduml
```

Used nomenclature for decorator are:

* **Component**
  * defines the interface for objects that can have functionality/responsiblity attached dynamically
* **ConcreteComponent**
  * defines an object where additional functionality/responsiblity can be attached
* **Decorator**
  * maintains a ref
erence to a *Component* object and has the *Component* interface, so that it can be used as Component  
* **ConcreateDecorator**
  * adds functionality/resonsibility to the *Component*

---

### Usage

Decorator are used to

* add functionality/responsiblity to existing individual objects dynamically without affecting other objects.
* for functionality/responsiblity, which can be withdrawn from objects
* when extension by subclassing is impractial.
* for adding the same functionality/responsiblity to different Components, without extending them all.

#### Advantages

* higher flexibitity than static inheritance, because the functionality can be added at runtime, without destroying and recreating the object with its function.
* avoids feature overloading classes high up in the hierarchy
* properties can be added multiple times to an object. 
* the decorator responsibitity can be reduced to one property of an object.
  
#### Disadvantages

* Decorator and it's Component are not equal. So the identification which object is decorated becomes complex, because from a object point of view the seen object is the decorator, not the "decorated object." Therefore, the use of the decorator pattern in systems that are based on object recognition does not make sense or is difficult to use.

* When using a lot of decorator classes, it becomes difficult to track the order of adding and removel of the decorators.

* If many decorator classes are created for an object, it becomes difficult to test all possible combinations for possible interactions.