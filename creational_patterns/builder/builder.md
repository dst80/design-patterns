## Builder pattern

The builder pattern separate the construction of a **complex** object from its represenation, so that the same construction process can create different representations. It's used together with the **component pattern** and/or the **strategie pattern** to create complex objects.

> **In contrast to the (Abstract) Factory pattern the builder pattern builds the object step by step and returns it at a final step. Abstract Factories provide a family of products und return it immediately.**

```plantuml
@startuml
!theme plain
object "**Director**" as Director {
    Construct ()
}

object "//**Builder**//" as Builder {
    BuildPartA ()
    BuildPartB ()
}

object "**ConcreteBuilder**" as ConcreteBuilder {
    BuildPartA ()
    BuildPartB ()
    GetResult ()
}

rectangle "**Product**" as Product {
}

Director *---r Builder : builder
Builder <|-- ConcreteBuilder
ConcreteBuilder::GetResult -r..> Product
@enduml
```

### Usage

The builder pattern should be used when

* the algorithm for creating a complex object should be independent of the parts that make up the object and how they're assembled.
* the construction process must allow different representations for the object that's constructed.

### Example

basic example to build different TextFormat-Files with the builder 
pattern

```plantuml
@startuml
!theme plain
allowmixing
skinparam nodesep 50
skinparam ranksep 50
package builder <<rectangle>> {
    together {
        object "//**TextConverter**//" as TextConverter {
            ConvertKeyValuePair ()
            NextSection ()
            ...
        }

        object "**ASCIIConverter**" as ASCIIConverter {
            ConvertKeyValuePair ()
            NextSection ()
            ...
        }

        object "**HTMLConverter**" as HTMLConverter {
            ConvertKeyValuePair ()
            NextSection ()
            ...
        }

        object "**JSONConverter**" as JSONConverter {
            ConvertKeyValuePair ()
            NextSection ()
            ...
        }
    }

    TextConverter <|-- ASCIIConverter
    TextConverter <|-- HTMLConverter
    TextConverter <|-- JSONConverter
}

object "**TextWriter**" as TextWriter {
    Write()
}


rectangle "...\nbuilder->NextSection()\n..." as Execution
TextWriter +.. Execution 


rectangle ASCIIText
ASCIIConverter ..> ASCIIText 

rectangle HTMLText
HTMLConverter ..> HTMLText 

rectangle JSONText
JSONConverter ..> JSONText 


TextWriter::Parse *- TextConverter : builder
@enduml
```
