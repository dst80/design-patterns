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
together {
    object "//<<Interface>>//\n**//ISubject//**" as ISubject {
        attach (IObserver) 
        detach (IObserver)
        notify ()
    }
    object "**WeatherData**" as WeatherData {
        attach (IObserver)
        detach (IObserver)
        notify ()
    }
}

together {
    object "//<<Interface>>//\n**//IObserver//**" as IObserver {
        update (IState)
    }
    object "//<<Interface>>//\n**//IDisplay//**" as IDisplay {
        display ()
    }
    object "**CurrentConditionDisplay**" as CurrentConditionDisplay {
        update (IState)
        display ()
    }
    object "**DayForecastDisplay**" as DayForecastDisplay {
        update (IState)
        display ()
    }
    object "**ThreeDayForecastDisplay**" as ThreeDayForecastDisplay {
        update (IState)
        display ()
    }
}

ISubject *- IObserver : ""
ISubject -> IObserver : call
ISubject <|-- WeatherData
IObserver -[hidden] IDisplay
IDisplay <|-- DayForecastDisplay
IObserver <|-- DayForecastDisplay
IDisplay <|--- CurrentConditionDisplay
IObserver <|--- CurrentConditionDisplay
IObserver <|---- ThreeDayForecastDisplay
IDisplay <|---- ThreeDayForecastDisplay

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
together {
    object "//<<Interface>>//\n**//IData//**" as IData {
        getData ()
    }

    object "//<<Interface>>//\n**//ISubject//**" as ISubject {
        attach (IObserver) 
        detach (IObserver)
        notify ()
    }
    object "**WeatherData**" as WeatherData {
        attach (IObserver)
        detach (IObserver)
        notify ()

        getData ()
    }
}

together {
    object "//<<Interface>>//\n**//IObserver//**" as IObserver {
        set (IData)
        update ()
    }
    object "//<<Interface>>//\n**//IDisplay//**" as IDisplay {
        display ()
    }
    together {
        object "**CurrentConditionDisplay**" as CurrentConditionDisplay {
            set (IData)
            update ()
            display ()
        }
        object "**DayForecastDisplay**" as DayForecastDisplay {
            set (IData)
            update ()
            display ()
        }
        object "**ThreeDayForecastDisplay**" as ThreeDayForecastDisplay {
            set (IData)
            update ()
            display ()
        }
    }
}

ISubject *- IObserver : ""
ISubject -> IObserver : call
IData <|-- WeatherData
ISubject <|-- WeatherData
IObserver -[hidden] IDisplay
IDisplay <|-- DayForecastDisplay
IObserver <|-- DayForecastDisplay
IDisplay <|--- CurrentConditionDisplay
IObserver <|--- CurrentConditionDisplay
IObserver <|---- ThreeDayForecastDisplay
IDisplay <|---- ThreeDayForecastDisplay
WeatherData::getData <- CurrentConditionDisplay  : call getData
WeatherData::getData <- DayForecastDisplay : call getData
WeatherData::getData <- ThreeDayForecastDisplay : call getData
DayForecastDisplay --[hidden] CurrentConditionDisplay
CurrentConditionDisplay --[hidden]d ThreeDayForecastDisplay
@enduml
```

The Pull Observer Pattern is an alternative observer design. During the *notify()* call, the *IData* information is pulled from the *Subject* by the *Observer* by calling the *Subject*'s getData() function. This design should be used when synchronization between *Observer* and *Subject* is required (e.g. high-precision clock) or when the data is so large that copying takes a while.

***Advantages:***

- In heavy load processes during the notify call Data is in sync.

***Disadvantages:***

- *Observer* knows something about the *Subject* because the *Observer* invoked a function of the *Subject*
- Another layer of abstraction is required
