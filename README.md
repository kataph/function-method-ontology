# Capabilities, functionalities, and engineering methods ontology

Attachment to the paper "About functions, behaviours, and capabilities
in formal ontology and engineering" in submission to the Semantic Web Journal, this ontology exemplify how the first order theory described in the paper can be translated in OWL.

The DOLCE Lite ontology, which is used to align this ontology with DOLCE, is taken from http://www.loa.istc.cnr.it/dolce/overview.html


# Example queries

In the paper some queries are written as functions of a variable input iri.
In the following we rewrite them with a fixed iri for sake of example and to facilitate reproducibility.

Takes a function as input and returns what components have a capability that corresponds to the given function:
```
PREFIX : <https://github.com/kataph/function-method-ontology#>
SELECT ?component
WHERE {
  ?capability :definition-founded-on :convert_chemical_energy_into_electricity_1 .
  ?capability :quality-of ?component}
```

Takes a system in input and returns what capacities of what components are involved in executing the ontological functions present in the given system:
```
PREFIX : <https://github.com/kataph/function-method-ontology#>
SELECT ?component ?functionOntological ?capacity
WHERE {
  ?functionSystemic :function-of ?component .
  ?functionSystemic :sp-dependent-on :electrical_circuit_1 .
  ?functionSystemic :sub-concept-of ?functionOntological .
  ?capability :definition-founded-on ?functionOntological .
  ?capability :quality-of ?component .
  ?capability :sp-dependent-on ?capacity .
  ?capacity :quality-of ?component}
```
  
Takes a given system as inputs and returns all systemic functions involved in a method, with
their role (main-function or sub-function) and underlying component:
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX : <https://github.com/kataph/function-method-ontology#>
SELECT ?component ?functionSystemic ?role ?method
WHERE {
  ?functionSystemic ?role ?method .
  ?method rdf:type/rdfs:subClassOf* :EngineeringMethod .
  ?functionSystemic :function-of ?component .
  ?component :constant-part-of :electrical_circuit_1}
```
Select the relevant parameter of a given capability
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX : <https://github.com/kataph/function-method-ontology#>
SELECT ?capacity ?parameter_value
WHERE {
  ?capability :sp-dependent-on ?capacity.
  ?capability :quality-of :battery_1.
  ?capacity :has-direct-quale ?parameter_value.}
```
  
