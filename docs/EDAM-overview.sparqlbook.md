# EDAM - The ontology of data analysis and management

Links:

* https://edamontology.org/page
* https://edamontologydocs.readthedocs.io

## EDAM Overview - focus on data type

EDAM includes 4 main sections of concepts (sub-ontologies):

* Topic - “A category denoting a rather broad domain or field of interest, of study, application, work, data, or technology. Topics have no clearly defined borders between each other.”
* Operation - “A function that processes a set of inputs and results in a set of outputs, or associates arguments (inputs) with values (outputs).”
* Data - “Information, represented in an information artefact (data record) that is 'understandable' by dedicated computational tools that can use the data as input or produce it as output.”
* Format - “A defined way or layout of representing and structuring data in a computer file, blob, string, message, or elsewhere.”

![EDAM relations diagram](https://edamontology.org/EDAMrelations.png)

## Exploration Venues for EDAN

There are some potential venues to explore, which use EDAN as resource containing linked data on (data) *formats* and *data types*, namely:

* Data classification classes
* links between  Data classes and Format classes
  * properties: edam:is_format_of, edam:has_format
  * example:  edam:format_3547 edam:is_format_of edam:data_2968 <s>(Note: this relation is not expressed in [EDAM_1.25.owl](https://edamontology.org/EDAM_1.25.owl) but on a  [EDAM format->data mappings spreadsheet]() )</s>


## Major issues

**Incompleteness/Narrow scope:**

It seems that only the perspective of one community, or group of users is expressed in EDAN. 
Take for instance the statement 
edam:format_3915 ("Zarr") is format of edam:format_3915 ("Sequence tag profile") and edam:data_3112 ("Gene expression matrix")`. Such statement leaves out the use of ZARR for N-Array data (Note: N-Array data or similar is NOT defined in EDAM)  


# links between  Data classes and Format classes

![Detail of EDAM Data class children](../media/EDAM-data.png)


## understanding is_format_of OWL structures

is_format_of relationship, in EDAM are expressed as owl:Restrictions, as expressed below for edam:format_1475 , which state: *the subject format_1475 on property (owl:onProperty) is_format_of, is subject to a restriction(owl:Restriction), applicable (owl:someValuesFrom) to entity data_0883*. In other words *format_1475 is_format_of data_0883*


```xml
    <owl:Class rdf:about="http://edamontology.org/format_1475">
        <rdfs:subClassOf rdf:resource="http://edamontology.org/format_2033"/>
        <rdfs:subClassOf>
            <owl:Restriction>
                <owl:onProperty rdf:resource="http://edamontology.org/is_format_of"/>
                <owl:someValuesFrom rdf:resource="http://edamontology.org/data_0883"/>
            </owl:Restriction>
        </rdfs:subClassOf>
        <rdfs:subClassOf>
            <owl:Restriction>
                <owl:onProperty rdf:resource="http://edamontology.org/is_format_of"/>
                <owl:someValuesFrom rdf:resource="http://edamontology.org/data_3870"/>
            </owl:Restriction>
        </rdfs:subClassOf>
        <created_in>beta12orEarlier</created_in>
        <oboInOwl:hasDefinition>Format of an entry (or part of an entry) from the PDB database.</oboInOwl:hasDefinition>
        <oboInOwl:hasExactSynonym>PDB entry format</oboInOwl:hasExactSynonym>
        <oboInOwl:inSubset rdf:resource="http://purl.obolibrary.org/obo/edam#edam"/>
        <oboInOwl:inSubset rdf:resource="http://purl.obolibrary.org/obo/edam#formats"/>
        <rdfs:label>PDB database entry format</rdfs:label>
    </owl:Class>
```


```sparql
PREFIX edam: <http://edamontology.org/>
PREFIX oboinowl: <http://www.geneontology.org/formats/oboInOwl#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?format ?format_label ?data ?data_label
WHERE {

        ?format rdfs:subClassOf+ edam:format_1915 ;
            rdfs:label ?format_label .
        ?format rdfs:subClassOf ?restriction .
        ?restriction owl:onProperty edam:is_format_of ;
                     owl:someValuesFrom ?data .
        ?data rdfs:label ?data_label .
}
ORDER BY ?format_label
```

```sparql
# Input: 1 format ; Output: data

PREFIX edam: <http://edamontology.org/>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?format ?format_label ?data ?data_label
WHERE {
    BIND ( edam:format_3915 AS ?format )
        ?format rdfs:subClassOf ?restriction ;
                    rdfs:label ?format_label .
        ?restriction owl:onProperty edam:is_format_of ;
                        owl:someValuesFrom ?data .
        ?data rdfs:label ?data_label .
}
ORDER BY ?format_label
```

```sparql
# new graph with is_format_of relation made simple

PREFIX edam: <http://edamontology.org/>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

CONSTRUCT {
    ?format edam:is_format_of ?data .
    }
WHERE {
        ?format rdfs:subClassOf+ edam:format_1915 ;
                rdfs:subClassOf ?restriction .
        ?restriction owl:onProperty edam:is_format_of ;
                     owl:someValuesFrom ?data .
}
```
