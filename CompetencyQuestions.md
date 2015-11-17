# Introduction #

A number of Darwin Core related efforts are underway, including
  * [extending Darwin Core to include new terms](http://code.google.com/p/darwincore/issues/list).
  * [representing Darwin Core in RDF](CharterOfIG.md).
  * [relating Darwin Core to genomic metadata standards](http://gensc.org/gc_wiki/index.php/Biodiversity_Working_Group).

A BoF at iEvoBio2011 [discussed](http://www.piratepad.net/iEvoBio11-BoF-reportouts) the above (as well as collections-related perspectives), and amongst the agreed next steps was to establish a common repository for use cases and competency questions. Until a better home is found for the competency questions, we will collect them here. [Here](http://marinemetadata.org/references/competencyquestionsoverview)'s a nice overview of what competency questions are all about.

# Competency questions #
For some examples of competency questions, see http://www.w3.org/TR/rdf-dawg-uc/

For an explanation of what "competency question" means, see http://marinemetadata.org/references/competencyquestionsoverview .

Terms in **_bold italic_** represent the GUID that would appear in a query.

### Darwin Core (including proposed new classes) ###
  1. Find all occurrences of **_taxon_**.
    * Find all occurrences of **_taxon_** satisfying **_spatial or temporal constraint_**.
    * Find all occurrences of **_taxa of concern_**. (e.g. "Find all occurrences of endangered or invasive species.")
  1. Find all occurrences for which there are no identifications.
  1. Find all occurrences for which there are multiple identifications.
  1. Find all occurrences of **_individual_**.
  1. Find all identifications for **_occurrence_**.
  1. Find all identifications of **_individual_**.
  1. Find all evidence for **_occurrence_**.
  1. Find all evidence to support the identification of **_individual_**

### Querying biodiversity occurrences based on genomic characters ###
  1. Find all occurrences of taxa whose genome includes a homolog of **_gene_**.


## Example and potential SPARQL queries corresponding to above ##
DwC 1b (query for invasive occurrences):
```
PREFIX rdf:       <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs:      <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dwc:       <http://rs.tdwg.org/dwc/terms/#>
PREFIX issg:       <http://spire.umbc.edu/ontologies/lists/ISSG-GISD.rdf#>

select ?occurrenceID ?taxon

FROM <http://www.csee.umbc.edu/~jsachs/occurrences/TechnoBioblitzOccurrences.rdf>
FROM <http://spire.umbc.edu/ontologies/lists/ISSG-GISD.rdf>

WHERE {?occurrence dwc:occurrenceID ?occurrenceID .
       ?occurrence dwc:Identification ?identification .
       ?identification dwc:taxonConceptID ?taxon .
       ?taxon rdfs:subClassOf issg:ISSG-GISDThing}
```


DwC 4:
```
select ?identification
where {
        ?identification rdf:type dwc:Identification .
        ?identification dwc:ofIndividual [individual] .
}
```

DwC 6:
```
select ?identification
where {
        ?identification rdf:type dwc:Identification .
        ?identification dwc:ofIndividual [individual] .
}
```