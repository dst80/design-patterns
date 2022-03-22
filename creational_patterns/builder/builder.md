## Builder pattern

The builder pattern separate the construction of a **complex** class from its represenation, so that the same construction process can create different representations. It's used together with the **component pattern** and/or the **strategie pattern** to create complex classs.

```plantuml
@startuml simple_builder
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
class Director {
    Construct()
}

interface Builder {
    BuildPartA()
    BuildPartB()
}

class ConcreteBuilder extends Builder {
    BuildPartA()
    BuildPartB()
    GetResult()
}

class Product
hide Product members

Director o---r Builder : builder

ConcreteBuilder::GetResult -right.> Product

@enduml
```


> *In contrast to the (Abstract) Factory pattern the builder pattern builds the class step by step and returns it at a final step. Abstract Factories provide a family of products und return it immediately.*

### Usage

The builder pattern should be used when

* the algorithm for creating a complex class should be independent of the parts that make up the class and how they're assembled.
* the construction process must allow different representations for the class that's constructed.

### Example

basic example to build different TextFormat-Files with the builder 
pattern

```plantuml
@startuml builder_exmple
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
package builder {
  class TextConverter {
      ConvertKeyValuePair ()
      NextSection ()
    }

    class ASCIIConverter extends TextConverter {
        ConvertKeyValuePair ()
        NextSection ()
    }

    class HTMLConverter extends TextConverter {
        ConvertKeyValuePair ()
        NextSection ()
    }

    class JSONConverter extends TextConverter {
        ConvertKeyValuePair ()
        NextSection ()
    }
}

class ASCIIText
ASCIIConverter ..> ASCIIText 
hide ASCIIText members

class HTMLText
HTMLConverter ..> HTMLText 
hide HTMLText members

class JSONText
JSONConverter ..> JSONText 
hide JSONText members

class "**TextWriter**" as TextWriter {
    Write()
}
note left of TextWriter::Write
...
builder->NextSection()
...
end note

TextWriter::Write o-l TextConverter


@enduml
```
