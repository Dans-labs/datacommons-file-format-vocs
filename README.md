# Data-type Classification of Research Data Files

***Repository dedicated to investigation the classification of data files, according to their content***

## Problem Statement

A file, such as a NetCDF, might contain very different content. It might contain 24h of a remote sensing observation, or multi-year simulation data.

Since EOSC Data Commons intents to make on the possible operations of a file, it is essential that the *type of data* and its *context* is made explicit in a machine-readable manner, so that appropriate actions can be taken.

In order to achieve that is important to agree on vocabularies that describe these *data-types* in an unambigous way, that is accepted by the research domain which makes use of those data-types.

Looking further head, once the classification is agreed upon, it might be possible to automate the classification, using AI methods.  

## Planning

### Stage 1: Landscape Analysis - Vocabularies for Data Types and Formats

**what vocabularies are used to classify data types, by which communities, and through which method?**

* [EDAM ontology](https://bioportal.bioontology.org/ontologies/EDAM) and its Data classification and (file) Format] classification  
  * research in [docs/EDAM-overview.sparqlbook](docs/EDAM-overview.sparqlbook)


# Run Repository code/notebook

## Python Virtual environment & requirements

In the top directory:

Create a virtual environment `python3 -m venv venv`

Activate it: `source venv/bin/activate`

Install Python requirements: `pip install -r requirements.txt`

## Jupyter notebooks with SPARQL

In order to run SPARQL inside jupyter notebooks, this repo uses the [SPARQL Notebook VScode extension](https://github.com/zazuko/vscode-sparql-notebook).

This requires:

* Install and enable the SPARQL Notebook extension
* Set the local endpoint (.ttl or .rdf file) you want to query, by mouse-right-click on the file and select "SPARQL Notebook: use File as Store"
* Remote endpoints can also be selected in SPARQL Connections panel

Note: .sparqlbook files are not displayed nicely in Github. In order to make possible oters reading the .sparqlbook should be converted to markdown by, mouse-right-click on the file and select "SPARQL Notebook: Export to Markdown". This is far from idea, since it does not show the results of the cell execution.