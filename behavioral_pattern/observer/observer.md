## Observer Pattern

The observer pattern is the key pattern, then an object needs to be informed that another object has changed. Event handling is one of the core uses of Observer Pattern. This pattern exists in functional programming as well as in object-oriented programming. For the sake of simplicity, the observer pattern is shown in its object-oriented form as an example.

Basically, there is always an *Observer* and the object that the *Observer* wants to observe (*Subject*, *Observable*).
In order for the *Observer* to be informed that the *Subject* has changed, it must register to the *Subject*.
When the *Subject*'s *notify ()* function is called, the *update ()* function is called for all registered *Observers*.

Depending on the used Observer pattern type, the updated information is either pushed to the *Observer* as parameter or pulled from the *Subject* by the *Observer* using a function call of the *Subject*.

### **Push Observer**

```plantuml
@startuml push_observer
!theme plain
skinparam nodesep 50
skinparam ranksep 50
hide circle
hide fields

together {
    abstract "**Subject**" as Subject {
        Attach(Observer) 
        Detach(Observer)
        Notify()
    }
    class "**DataImp**" as DataImp {
        Attach(Observer)
        Detach(Observer)
        Notify()
    }
}

together {
    abstract "**Observer**" as Observer {
        Update(IState)
    }
    abstract "**Display**" as Display {
        Display()
    }
    class "**Display1**" as Display1 {
        Update(IState)
        Display()
    }
    class "**Display2**" as Display2 {
        Update(IState)
        Display()
    }
    Display <|-- Display1
    Display <|-- Display2
    Observer <|-- Display1
    Observer <|-- Display2
}

Subject o- Observer 
Subject::Notify -> Observer::Update
Subject <|-- DataImp
Observer -[hidden] Display

@enduml
```

The Push Observer Pattern is the typical observer design. During the "*notify ()*" call, the information "*State*" is pushed from the "*Subject*" to the "*Observer*".

***Advantages:***

- Simple implementation
- *Observer* doesn't know anything about the *Subject*
- *IState* has a structure independent of *Object* and *Subject*
- *IState* can be different types, hence different State can the notified.

***Disadvantages:***

- In heavy load processes during the notify call IState can be out of sync.

***

### **Pull Observer**

```plantuml
@startuml pull_observer
!theme plain
skinparam nodesep 100
skinparam ranksep 50
hide fields
hide circle

together {
    interface "**Data**" as Data {
        GetData()
    }

    interface "**Subject**" as Subject {
        Attach(Observer) 
        Detach(Observer)
        Notify()
    }
    class "**Data Imp**" as DataImp {
        Attach(Observer)
        Detach(Observer)
        Notify()
        GetData ()
    }
    Data <|-- DataImp
    Subject <|-- DataImp
}

together {
    together {
    interface "**Observer**" as Observer {
        Set(Data)
        Update()
    }
    Interface "**Display**" as Display {
        Paint()
    }
    }
    together {
        class "**Display Imp. 1**" as Display1 {
            Set(Data)
            Update()
            Paint()
        }
        class "**Display Imp. 2**" as Display2 {
            Set(Data)
            Update()
            Paint()
        }
    }
    Observer <|-- Display1
    Observer <|--- Display2
    Display <|-- Display1
    Display <|-- Display2

}

Subject o-r Observer

DataImp::GetData <- Display1::Update 
DataImp::GetData <- Display2::Update 
Subject::Notify -> Observer::Update

@enduml
```

The Pull Observer Pattern is an alternative observer design. During the *notify()* call, the *Data* information is pulled from the *Subject* by the *Observer* by calling the *Subject*'s getData() function. This design should be used when synchronization between *Observer* and *Subject* is required (e.g. high-precision clock) or when the data is so large that copying takes a while.

***Advantages:***

- In heavy load processes during the notify call Data is in sync.

***Disadvantages:***

- *Observer* knows something about the *Subject* because the *Observer* invoked a function of the *Subject*
- Another layer of abstraction is required
