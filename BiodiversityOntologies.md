![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Summary of some ontologies/data models which provide object properties that can connect instances of biodiversity-related classes #

**Date:** (Created) 16 March 2013; (Last modified) 9 October 2013

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document)

**Permanent URL:** http://code.google.com/p/tdwg-rdf/wiki/BiodiversityOntologies

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=BiodiversityOntologies) (TDWG RDF/OWL Task Group)

**Abstract:** This document diagrams the class structure of several ontologies or data models that provide terms which can be used as object properties in RDF. It summarizes those object properties and their characteristics.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)


**Contents**



# 1 Introduction #

Biodiversity Information Standards (TDWG) is a standards organization which adopts standards for the exchange of biodiversity exchange.  The Darwin Core standard (http://www.tdwg.org/standards/450/) is a technical specification that defines terms that can serve as properties to describe biodiversity-related resources.  When Darwin Core is used in text- and XML-based exchange schemes, the terms which end in "ID" can be used to specify identifiers of resources which are related to the subject resource.  However, these terms cannot be used as object properties in RDF.  For that reason, object properties which relate instances of biodiversity-related classes must come from vocabularies outside of Darwin Core.  This document describes three ontologies that define biodiversity-related classes and object properties which relate them.  None of these ontologies are TDWG standards, although the first was commissioned by the Technical Architecture Group (TAG) of TDWG.  The information in this document is provided for informational purposes only - the RDF Task Group has not recommended any of these ontologies for use.  Please report any errors to [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=BiodiversityOntologies).

## 1.1 Similarities among the four ontologies/data models ##

Each of the three vocabularies described in this document calls itself an "ontology" (see [The Beginners Guide to RDF](http://code.google.com/p/tdwg-rdf/wiki/Beginners4Vocabularies#4.2._What_is_an_ontology?) for a discussion of the definition of "ontology").  Each of the ontologies uses Web Ontology Language (OWL) to describe the properties of the terms.  Some term descriptions include domain, range, and subproperty declarations and properties are declared to be object or datatype properties.  However, there are few formal constraints to class membership - the ontologies do not make use of OWL restrictions.

Note on 2013-07-01: a fourth data model (the BiSciCol model) has been added.  The URIs for the bsc: namespace (http://biscicol.org/terms/index.html# ) object properties are defined at http://biscicol.org/terms/index.html although they don't dereference to produce RDF/XML at this time.

## 1.2 Conventions used in the diagrams ##

In the diagrams, ovals are used to represent instances of the classes whose URIs are listed on the ovals.  Rectangles represent literals with an example string shown in the rectangle.  If the line connecting two shapes has a single arrowhead, there is a single property that relates the subject resource at the tail end to the object resource at the head end.  If the line connecting two shapes has arrowheads at both ends, there is a pair of properties which can relate the resources with either one serving as the subject.  Classes in the three ontologies which are similar (possibly identical) are filled with the same color in each diagram.  Note: the diagrams are not graphical representations of RDF graphs.

## 1.3 Subclass relationships and object properties ##

The tables which list subclass relationships and object properties were created manually by examining the ontologies using [SWOOP](http://code.google.com/p/swoop/) and example resources which use the ontologies (notably http://ocs.taxonconcept.org/ocs/f522444a-2dd9-400e-be59-47213ef38cb9.rdf for the TaxonConcept ontology).

# 2 The TDWG Ontology #

## 2.1 Description ##

When TDWG made the deployment of Life Science Identifiers (LSIDs) a priority, the development of vocabularies described by RDF (Resource Description Framework; see http://code.google.com/p/tdwg-rdf/wiki/Beginners) was intended to progress in tandem with LSID adoption (see http://wiki.tdwg.org/twiki/bin/view/TAG/LsidVocs ).  These RDF vocabularies (written using a form of RDF called Web Ontology Language or OWL) were in aggregate known as "The TDWG Ontology" and were intended to either be based on an existing standard or to eventually be incorporated as part of an evolving standard.  Thus the TaxonName and TaconConcept ontologies were based on (but not actually part of) the Taxon Concept Transfer Schema (TCS), a Current (2005) Standard, and the Institution and Collection Ontologies were created as part of the development of the NCD Draft Standard.

The "TDWG Ontology" actually consists of a number of individual ontology documents written in OWL/RDF.  They were written primarily by Roger Hyam in 2006 and 2007.  The individual ontologies have base URIs in the form "http://rs.tdwg.org/ontology/[something]#" where [something](something.md) is descriptive of the particular ontology.  The ontology documents can be viewed at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/ and lower levels of the document tree. Semantic clients requesting content-type: application/rdf+xml are redirected to the OWL/RDF versions of the ontology, probably the ones at http://rs.tdwg.org/ontology2/, but maybe http://rs.tdwg.org/ontology/ (I'm not sure which).  The list of ontologies at the Google Code site includes two versions of some of the ontologies, a .owl version and a .rdf version.  It appears that the .rdf versions are the most current version and are the ones which are returned to semantic clients.

The TDWG ontology is not currently under development (see http://www.hyam.net/blog/archives/643#more-643 ) and as of 2013-03-15 its future is under discussion by the TDWG Vocabulary Management (VoMaG) Task Group (see http://community.gbif.org/pg/pages/view/29079/ ).

(Note: much of this information was taken from http://community.gbif.org/pg/pages/view/29079/ and additional details can be found there.)

## 2.2 Class structure ##

All of the classes used in the TDWG Ontology are defined within the parts of the ontology.  The tc:TaxonConcept and tn:TaxonName classes are based on the the ideas expressed in the TCS Standard. A complete list of classes defined in the ontology can be found [here](http://code.google.com/p/tdwg-rdf/wiki/ClassInventory#1.4.__Classes_in_the_TDWG_Ontologies).

![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-ontology-class-structure.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-ontology-class-structure.png)

## 2.3 Subclass relationships ##
base: = http://rs.tdwg.org/ontology/Base#

core: = http://rs.tdwg.org/ontology/Core#

|Class|subClassOf|
|:----|:---------|
|to:TaxonOccurrence|base:BaseThing|
|to:Identification|base:BaseThing|
|tc:TaxonConcept|core:Concept|
|tn:TaxonName|base:Name |

## 2.4 Some object properties ##

|Property|Subject class|Domain declared?|Object class|Range declared?|
|:-------|:------------|:---------------|:-----------|:--------------|
|to:derivedFrom|to:TaxonOccurrence|yes             |to:TaxonOccurrence|yes            |
|to:hostCollection|to:TaxonOccurrence|yes             |col:Collection|yes            |
|to:identifiedTo|to:TaxonOccurrence|yes             |to:Identification|yes            |
|to:occurrence|to:Identification|yes             |to:TaxonOccurrence|yes            |
|to:taxon|to:Identification|yes             |tc:TaxonConcept|yes            |
|to:higherTaxon|to:Identification|yes             |tc:TaxonConcept|yes            |
|to:expert|to:Identification|yes             |per:person  |yes            |
|tc:hasName|tc:TaxonConcept|yes             |tn:TaxonName|no             |
|tc:accordingTo|tc:TaxonConcept|yes             |(any reference type)|no             |
|to:typeForName|to:TaxonOccurrence|yes             |tn:TaxonName|yes            |

Note: the subject and object classes for the terms to:hostCollection and to:typeForName indicate that to:TaxonOccurrence instances are considered to be equivalent to, or to include specimens.

The term to:value to some extent conflates the species presence/absence aspect of "occurrence" with the aspect of "occurrence" as the documentation of a particular organism at a place and time.

# 3 The TaxonConcept Ontology #

## 3.1 Description ##

The goals of the TaxonConcept project (http://www.taxonconcept.org/) are:

  * Create Linked Open Data (LOD) Identifiers for Species Concepts
  * Link Species Concepts to Names in the Global Names Initiative Database
  * Investigate using LOD Methods to match Specimens and related Data to Species Concepts

The TaxonConcept OWL Ontology ([txn](http://lod.taxonconcept.org/ontology/txn.owl)), written by Peter J. DeVries from 2009 through 2012 was based on the earlier GoeSpecies from 2007.  It defines many classes and terms which can be used to describe biodiversity resources.  The diagram here includes only the subset of the classes which correspond approximately to those described in the other two ontologies.  The TaxonConcept ontology also includes classes defined in other vocabularies, such as foaf, bibo, and wgs84.

The rdfs:comment associated with the current version of the ontology (v 0.2 on 2013-03-15) indicates that the ontology is still under development.

## 3.2 Class structure ##

![http://tdwg-rdf.googlecode.com/svn/trunk/file/taxonconcept-class-structure.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/taxonconcept-class-structure.png)

Notes:

txn:SpeciesConcept instances (e.g. http://lod.taxonconcept.org/ses/mCcSp.rdf ) can be described using many terms in the TaxonConcept ontology as well as skos:closeMatch.  The concept itself is described by  tagged resources which are linked to the concept using dcterms:hasPart.  See TaxonConceptOntologyDiagrams for more information about this model.

The ontology does not specifically include a property to relate instances to a secundum/sensu reference component as described in the TDWG TCS standard.  However, the term txn:speciesConceptBasedOn is described as "This describes the theoretical models behind the species concept. All species concepts are at least based on an Objective Model. In addition the may also be based on a Biological Species Model and or a Phylogenetic Species Model. A species concept could be based on all three of these. This is to reflect that there are several criteria used to support a species concept. ..."

The class txn:Area is a subclass of wgs84:SpatialThing which is defined by the WGS84 Geo Positioning RDF Vocabulary (http://www.w3.org/2003/01/geo/wgs84_pos see also [RFC 5870](http://tools.ietf.org/html/rfc5870)) which represents locations using the WGS84 geodetic reference datum.  Thus it would be reasonable to expect that txn:Area instances would be described by WGS84 Vocabulary terms although the semantics of the TaxonConcept ontology does not require this.  For more information, refer to http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001982.html and subsequent posts in that thread.

The ontology provides two datatype properties (txn:startDate and txn:endDate) which might be used to indicate the date range over which the occurrence was documented.  The diagram shows them used thus.  The ontology also defines the class txn:Year which is a subclass of http://www.w3.org/2006/time#DateTimeDescription .  Thus time is modeled as a non-literal object in the ontology, although txn:Year is the range for properties related to publication rather than recording occurrences.

As shown in the diagram, the network of TaxonConcept object properties allows a user to relate instances of one class to another by multiple paths.

## 3.3 Subclass relationships ##
|Class|subClassOf|
|:----|:---------|
|txn:Occurrence|http://purl.org/NET/c4dm/event.owl#Event|
|txn:Identification|http://purl.org/NET/c4dm/event.owl#Event|
|txn:Area|http://www.w3.org/2003/01/geo/wgs84_pos#SpatialThing|
|txn:SpeciesConcept|txn:TaxonConcept|

## 3.4 Some object properties ##

|Property|Subject class|Domain declared?|Object class|Range declared?|
|:-------|:------------|:---------------|:-----------|:--------------|
|txn:identificationHasOccurrence|txn:Identification|yes             |txn:Occurrence|no             |
|txn:occurrenceHasArea|txn:Occurrence|yes             |txn:Area    |yes            |
|txn:areaHasOccurrence|txn:Area     |no              |txn:Occurrence|no             |
|txn:occurrenceHasIndividual|txn:Occurrence|yes             |txn:SpeciesIndividual|no             |
|txn:individualHasOccurrence|txn:SpeciesIndividual|yes             |txn:Occurrence|no             |
|txn:individualHasObservedArea|txn:SpeciesIndividual|yes             |txn:Area    |yes            |
|txn:areaHasIndividual|txn:Area     |no              |txn:SpeciesIndividual|no             |
|txn:individualHasCurrentIdentificationAssertion|txn:SpeciesIndividual|yes             |txn:Identification|no             |
|txn:individualHasPreviousIdentificationAssertion|txn:SpeciesIndividual|yes             |txn:Identification|no             |
|txn:identificationOfIndividual|txn:Identification|yes             |txn:SpeciesIndividual|no             |
|txn:identificationHasSpeciesConcept|txn:Identification|no              |txn:SpeciesConcept|no             |
|txn:individualHasSpeciesConcept|txn:SpeciesIndividual|yes             |txn:SpeciesConcept|no             |
|txn:identifiedBy|txn:Identification|yes             |foaf:Person |yes            |
|txn:speciesConceptHasOccurrence|txn:SpeciesConcept|yes             |txn:Occurrence|no             |
|txn:occurrenceHasSpeciesConcept|txn:Occurrence|yes             |txn:SpeciesConcept|yes            |
|txn:speciesConceptHasObservedArea|txn:SpeciesConcept|yes             |txn:Area    |yes            |
|txn:areaHasObservedSpeciesConcept|txn:Area     |no              |txn:SpeciesConcept|no             |
|txn:hasCollector|txn:Occurrence|yes             |foaf:Person |yes            |

Note: the subject class for txn:hasCollector indicates that txn:Occurrence is viewed as equivalent to or including specimens.

# 4 The Darwin-SW Ontology #

## 4.1 Description ##

**Note: this information describes Darwin-SW version 0.2 .  Darwin-SW is under revision for version 0.3 which will be in line with the draft Darwin Core RDF Guide.  Notably, version 0.3 will refer to classes in the DwC type vocabulary (dwctype: namespace) rather than classes in the general (dwc:) namespace.**

The Darwin-SW Ontology (DSW) is a vocabulary which describes relationships among classes defined by the Darwin Core standard by defining object properties which relate those classes and several classes outside of Darwin Core.  The ontology is described at http://code.google.com/p/darwin-sw/ with the defining OWL ontology file viewable at http://code.google.com/p/darwin-sw/source/browse/trunk/dsw.owl .  Version 0.2 (the most recent version as of 2013-03-15) was written in 2011 by Steve Baskauf and Campbell Webb. The ontology is subject to change in future versions.

The design principles that underlie DSW are elaborated at http://code.google.com/p/darwin-sw/wiki/DesignPrinciples .  DSW co-opts many of the Darwin Core classes and for the most part maintains the meaning of the class as described in the term definition.  DSW takes the position that a dwc:Occurrence instance documents an organism at a place and time, but that the physical or electronic documentary evidence is a separate entity which is considered to be an instance of the class dsw:Token.  In an attempt to add clarity to the meaning of the class dwc:Taxon, DSW declares that class to be equivalent to the tc:TaxonConcept class of the TDWG Ontology, since the meaning of tc:TaxonConcept is underpinned by the TDWG Taxon Concept Transfer Schema (TCS) standard.

## 4.2 Class structure ##

![http://tdwg-rdf.googlecode.com/svn/trunk/file/darwin-sw-class-structure-revised.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/darwin-sw-class-structure-revised.png)

Notes: Each of the core classes in DSW are connected by a pair of DSW-defined object properties which are declared to be inverse properties.  Many of the classes are declared to be disjoint.

Any type of evidence can be an instance of the dsw:Token property.

DSW assumes that Darwin Core property terms will be used as datatype properties of instances of the class under which the terms are listed in the standard.

## 4.3 Subclass relationships ##

None of the classes shown on the diagram have subclass relationships.  The ontology also defines several specimen-related classes which have subclass relationships, but they are not diagrammed here.

## 4.4 Some object properties ##

|Property|Subject class|Domain declared?|Object class|Range declared?|
|:-------|:------------|:---------------|:-----------|:--------------|
|dsw:locates|dcterms:Location|yes             |dwc:Event   |yes            |
|dsw:locatedAt|dwc:Event    |yes             |dcterms:Location|yes            |
|dsw:eventOf|dwc:Event    |yes             |dwc:Occurrence|yes            |
|dsw:atEvent|dwc:Occurrence|yes             |dwc:Event   |yes            |
|dsw:occurrenceOf|dwc:Occurrence|yes             |dsw:IndividualOrganism|yes            |
|dsw:hasOccurrence|dsw:IndividualOrganism|yes             |dwc:Occurrence|yes            |
|dsw:hasIdentification|dsw:IndividualOrganism|yes             |dwc:Identification|yes            |
|dsw:identifies|dwc:Identification|yes             |dsw:IndividualOrganism|yes            |
|dsw:toTaxon|dwc:Identification|yes             |dwc:Taxon   |yes            |
|dsw:taxonOfId|dwc:Taxon    |yes             |dwc:Identification|yes            |
|dsw:hasEvidence|dwc:Occurrence|yes             |dsw:Token   |yes            |
|dsw:evidenceFor|dsw:Token    |yes             |dwc:Occurrence|yes            |
|dsw:idBasedOn|dwc:Identification|yes             |dsw:Token   |yes            |
|dsw:isBasisForId|dsw:Token    |yes             |dwc:Identification|yes            |
|dsw:georefBy|dcterms:Location|yes             |foaf:Agent  |yes            |
|dsw:recBy|dwc:Occurrence|yes             |foaf:Agent  |yes            |
|dsw:idBy|dwc:Identification|yes             |foaf:Agent  |yes            |

Notes: dsw:Token instances may be related to dsw:IndividualOrganism instances in several ways.  General relatedness can be expressed using the pair of inverse properties dsw:derivedFrom and dsw:hasDerivative.  Both of these terms are transitive.  More specific relationships can be declared using foaf:depicts/foaf:hasDepiction for tokens that are images and dcterms:hasPart/dcterms:isPartOf for physical objects (e.g. specimens).  Neither of these specific relationship terms are transitive.  See http://code.google.com/p/darwin-sw/wiki/TokenIssues for more information.

# 5 The BiSciCol data model #

## 5.1 Description ##

The BiSciCol data model is described at http://biscicol.blogspot.com/2013_03_01_archive.html .  It includes six Darwin Core classes: Occurrence, Event, dcterms:Location, GeologicalContext, Identification, and Taxon .

## 5.2 Class structure ##
The relationships among the classes shown on that page are:

![http://2.bp.blogspot.com/--5-pDb4P5fQ/UT66ZpFJK9I/AAAAAAAAAG0/_-koqKyfzSI/s400/DwC_concept_relations-scaled.png](http://2.bp.blogspot.com/--5-pDb4P5fQ/UT66ZpFJK9I/AAAAAAAAAG0/_-koqKyfzSI/s400/DwC_concept_relations-scaled.png)

## 5.3 Subclass relationships ##

None of the classes shown on the diagram have subclass relationships.

## 5.4 Some object properties ##

The BiSciCol relationship predicates are transitive or symmetric and are useful for graph traversal, indicating whether the graph should be traversed one step in a particular direction (depends\_on), one step in either direction (related\_to), all steps in one direction (derives\_from), or all steps in both directions (alias\_of).  In terms of DwC class relationships, only two of the object properties form BiSciCol are used  (the abbreviation bsc: stands for http://biscicol.org/terms/index.html# ):

|Property|Subject class|Domain declared?|Object class|Range declared?|
|:-------|:------------|:---------------|:-----------|:--------------|
|bsc:depends\_on|various      |no              |various     |no             |
|bsc:related\_to|various      |no              |various     |no             |

These properties are defined at http://biscicol.org/terms/index.html .  Neither of these two properties are transitive.