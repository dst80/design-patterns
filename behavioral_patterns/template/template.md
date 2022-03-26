## Template (Method) Pattern

Define the skeleton of an algorithm/functionality.
The Template Method pattern deferring some steps to the algorithm/functionality to subclasses.
The Template Class uses a template object with can be replaced. For better operation the template object can have some requirements like an interface which can be implemented by subclasses.

```plantuml
@startuml template_method
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

Title Template Method
hide circle
hide fields

abstract class AbstractClass {
    TemplateMethod()
    virtual Operation1()
    virtual Operation2()
}

class ConcreteClass extends AbstractClass {
    Operation1()
    Operation2()
}

note right of AbstractClass
    ...
    Operation1()
    ...
    Operation2()
    ...
end note

@enduml
```

```plantuml
@startuml template_class
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

Title Template Class
hide circle

together {
interface Object {
    Operation1()
    Operation2()
}

class ConcreteObject extends Object {
    Operation1()
    Operation2()
}
}

together {
class TemplateClass <<T base of Object>> {
    DoSomething()
    T object
}

class ConcreteClass <<ConcreteObject>> extends TemplateClass{
    DoSomething()
    ConcreteObject object
}
}

note left of TemplateClass::DoSomething
    ...
    object.Operation1()
    ...
    object.Operation2()
    ...
end note

Object <- TemplateClass::T 
@enduml
```

### Usage

Template (Method) pattern should be used

* to implement the invariant part of an algorithm/functionality once and leave it up to the subclasses or template object to implement the behavior that can/should vary.
* when common behavior among subclasses should be factored and localized in a common class to avoid code duplication.
* to control subclasses behavior
* to define dependency injection objects at compile time without the requirement to change the objects at run time.  

#### Advantages

* less code duplication
* support inversion of control mechanism by default
* in the case of Template Method, can be changed on run time
* In the case of Template Class, no pointer indirection, because the Template Objects are defined at compile time and can therefore be directly added as members.

#### Disadvantages

* common code separation make subclasses less flexible to optimize specific section of the algorithm.

* In case of template method, pointer indirection in dependency injection may result in additional overhead.
* In case of template classes, they are defined at compile time so they cannot be switched at run-time
* some language doesn`t support generic interfaces
