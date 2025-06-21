🧠 Mermaid-OWL Lite (MOWL-Lite)
A minimal, visual syntax for expressing OWL ontologies using Mermaid.js classDiagram syntax, designed to be transformable to valid OWL 2 .ttl files.

✨ Overview
Mermaid-OWL Lite (MOWL-Lite) is:

✅ Human-readable and diagram-friendly

🔄 Bidirectionally transformable (Mermaid ↔ TTL)

⚖️ Based on OWL 2 DL semantics

🔧 Designed for lightweight ontology authoring, visualization, and validation

💡 Compatible with diagram editors like Obsidian, VS Code, or GitHub Preview

📘 Class Syntax
Class Declaration
text
classDiagram
    class Pizza
OWL Equivalent:

text
:Pizza rdf:type owl:Class .
🧭 Class Hierarchy
Subclassing
text
classDiagram
    Pizza <|-- NamedPizza
OWL Equivalent:

text
:NamedPizza rdfs:subClassOf :Pizza .
🔗 Object Properties
Basic Object Property
text
classDiagram
    Pizza --> "hasTopping" Topping
OWL Equivalent:

text
:hasTopping rdf:type owl:ObjectProperty ;
            rdfs:domain :Pizza ;
            rdfs:range :Topping .
Inverse Properties (optional)
text
classDiagram
    Topping --> "isToppingOf ^" Pizza
OWL Equivalent:

text
:isToppingOf owl:inverseOf :hasTopping .
🔢 Data Properties
text
classDiagram
    Customer --> "numberOfPizzasPurchased: xsd:integer" int
OWL Equivalent:

text
:numberOfPizzasPurchased rdf:type owl:DatatypeProperty ;
                         rdfs:domain :Customer ;
                         rdfs:range xsd:integer .
int is a placeholder node to satisfy Mermaid’s diagram rendering. Use similar dummy nodes for other XSD types.

🧬 Property Restrictions
someValuesFrom
text
classDiagram
    American --> "hasTopping some" MozzarellaTopping
OWL Equivalent:

text
:American rdfs:subClassOf [
  rdf:type owl:Restriction ;
  owl:onProperty :hasTopping ;
  owl:someValuesFrom :MozzarellaTopping
] .
allValuesFrom
text
classDiagram
    American --> "hasTopping only" TomatoTopping
OWL Equivalent:

text
:American rdfs:subClassOf [
  rdf:type owl:Restriction ;
  owl:onProperty :hasTopping ;
  owl:allValuesFrom :TomatoTopping
] .
hasValue
text
classDiagram
    American --> "hasCountryOfOrigin value America" America
OWL Equivalent:

text
:American rdfs:subClassOf [
  rdf:type owl:Restriction ;
  owl:onProperty :hasCountryOfOrigin ;
  owl:hasValue :America
] .
♻️ Equivalence (owl:equivalentClass)
text
classDiagram
    CheeseyPizza "≡" Pizza & hasTopping some CheeseTopping
OWL Equivalent:

text
:CheeseyPizza owl:equivalentClass [
  owl:intersectionOf (
    :Pizza
    [ rdf:type owl:Restriction ;
      owl:onProperty :hasTopping ;
      owl:someValuesFrom :CheeseTopping ]
  )
] .
Use & to represent class intersections inside equivalence expressions.

🔀 Union Classes
text
classDiagram
    PizzaTopping o-- "unionOf" (MeatTopping, CheeseTopping, VegetableTopping)
OWL Equivalent:

text
:PizzaTopping owl:equivalentClass [
  owl:unionOf ( :MeatTopping :CheeseTopping :VegetableTopping )
] .
❗ Disjoint Classes
text
classDiagram
    CajunSpiceTopping --|>disjointWith RosemaryTopping
OWL Equivalent:

text
:CajunSpiceTopping owl:disjointWith :RosemaryTopping .
🛠️ Transformation Table
Mermaid Pattern	TTL Equivalent
A <-- B	A --> "p" B
p is owl:ObjectProperty from A to B
A --> "p: xsd:type" dummy	p is owl:DatatypeProperty with given range
A --> "p some" C	rdfs:subClassOf [ owl:someValuesFrom C ]
A --> "p only" C	rdfs:subClassOf [ owl:allValuesFrom C ]
A --> "p value C"	rdfs:subClassOf [ owl:hasValue C ]
A "≡" X & Y	owl:equivalentClass [ owl:intersectionOf (X Y) ]
A o-- "unionOf" (X, Y)	owl:unionOf (X Y)
A -->disjointWith B	owl:disjointWith
B --> "inverseOf ^" A	owl:inverseOf
✅ Example Diagram
text
classDiagram
    class Pizza
    class Topping
    class CheeseTopping
    class NamedPizza
    class American
    class Customer
    class int

    Pizza --> "hasTopping" Topping
    Topping <|-- CheeseTopping
    NamedPizza <|-- American
    American --> "hasTopping some" CheeseTopping
    Customer --> "numberOfPizzasPurchased: xsd:integer" int
🚧 Roadmap
🎨 Mermaid Editor Plugin

🔁 Mermaid-to-TTL Compiler (Python or Node)

✅ TTL-to-Mermaid Converter

🧪 OWLAPI Validator

🧾 Round-trip Visual Diff Tool

🤝 Contributing
If you'd like to extend this syntax, improve parsing tools, or build related tooling, please submit a pull request or open an issue.

📄 License
This syntax is open and free to use under the MIT License.

🔗 References
OWL 2 Web Ontology Language Specification

Mermaid.js Documentation
