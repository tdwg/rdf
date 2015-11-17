# Inventory of Classes Relevant to Biodiversity Informatics #

In [Issue 3](http://code.google.com/p/tdwg-rdf/issues/detail?id=3) it was requested that we create a list of classes and terms relevant to our community. Below is the beginnings of a list of classes organized according to their defining vocabulary.  In these lists, if a class is defined to be a subclass of another, that is noted.

## 1. General class lists ##

#### 1.1.  Dublin Core classes [(1)](#1_Dublin_Core_classes.md) (`dcterms: = http://purl.org/dc/terms/`) ####
```
Agent
AgentClass  (subclass of itself???)
BibliographicResource
FileFormat  subclass of dcterms:MediaType
Frequency
Jurisdiction subclass of LocationPeriodOrJurisdiction
LicenseDocument  subclass of RightsStatement
LinguisticSystem
Location  subclass of LocationPeriodOrJurisdiction
LocationPeriodOrJurisdiction
MediaType  subclass of MediaTypeOrExtent
MediaTypeOrExtent
MethodOfAccrual
MethodOfInstruction
PeriodOfTime  subclass of LocationPeriodOrJurisdiction
PhysicalMedium  subclass of MediaType
PhysicalResource
Policy
ProvenanceStatement
RightsStatement
SizeOrDuration  subclass of MediaTypeOrExtent
Standard
```
We should include Dublin Core and Darwin Core type vocabularies here.

#### 1.2.  Darwin Core classes [(2)](#2_Darwin_Core_Quick_Reference_Guide.md)  (`dwc: = http://rs.tdwg.org/dwc/terms/`) ####
```
Occurrence
Event
dcterms:Location (note: references the Dublin Core class)
GeologicalContext
Identification
Taxon
ResourceRelationship
MeasurementOrFact
```
#### 1.3.  FOAF classes [(3)](#3_FOAF_vocabulary.md) (`foaf: = http://xmlns.com/foaf/0.1/`) ####
```
Agent
Person subclass of Agent
Project
Organization subclass of Agent
Group subclass of Agent
Document
Image subclass of Document
OnlineAccount
PersonalProfileDocument subclass of Document
```
#### 1.4.  Classes in the TDWG Ontologies [(4)](#4_TDWG_Ontology.md) ####
This ontology defines many classes which to some degree correspond to the Darwin Core classes, although they are not explicitly declared to be the same as those classes.  The ontology consists of a number of classes and terms which are defined under their own namespaces.  Most of the classes are declared to be subclasses of other classes in the Base or Core Ontologies.  Unless otherwise stated, in the list below all are subclass of `base:BaseThing`.  The overall ontology is in an unfinished state.  Several of the individual ontology documents are apparently unfinished and therefore contain errors.  Those ontologies are noted.

The Taxon Concept and Taxon Name Ontologies differ somewhat from the others in that their classes are not linked to the Base Ontology through subclassing.  So they essentially stand alone.  Although those ontologies are not TDWG standards, they are specifically designed to be an RDF representation of the Taxonomic Concept Transfer Schema standard [(5)](#5_Taxonomic_Concept_Transfer_Schema.md) which itself is not expressed in RDF.

The classes listed in the Collection Ontology represent classes from the Natural Collections Description (NCD) draft standard [(6)](#6_Natural_Collections_Descriptions_(NCD)_draft_TDWG_standard.md).  The base URI of those classes (`http://rs.tdwg.org/ontology/voc/Collection#`) does not agree with the URIs used in the subproperty declarations for NCD terms in the Darwin Core RDF (`http://rs.tdwg.org/ncd/terms/`) which do not dereference.

**Base Ontology (base: = `http://rs.tdwg.org/ontology/Base#`)**
```
BaseThing (not  subclass)
Actor
Space
Name
DefinedTerm
MediaObject
```
**Core Ontology (core: = `http://rs.tdwg.org/ontology/Core#`) Note apparent error with Person subclassing**
```
ContactInformation
Organisation subclass of base:Actor
Collection
Description
Geolocalisation
Person subclass of base:BaseActor ( is this an error?)
Place
PublicationCitation
Specimen
Concept
Identification
Team base:subclass of Actor
Observation
Gathering
```
**Collection Ontology (collection: = `http://rs.tdwg.org/ontology/voc/Collection#`)**
```
Collection  subclass of core:Collection
DerivedCollection  subclass of collection:Collection
DevelopmentStatusTypeTerm  subclass of base:DefinedTerm
SpecimenPreservationMethodTypeTerm  subclass of base:DefinedTerm
PrimaryPurposeTypeTerm subclass of base:DefinedTerm
PrimaryGroupingPrincipleTypeTerm  subclass of base:DefinedTerm
KingdomTypeTerm  subclass of base:DefinedTerm
ConservationStatusTypeTerm  subclass of base:DefinedTerm
```
**Collection Type Ontology (collectiontype: = `http://rs.tdwg.org/ontology/voc/CollectionType#`)**
```
CollectionTypeTerm  subclass of base:DefinedTerm
```
**ContactDetails Ontology (contact: = `http://rs.tdwg.org/ontology/voc/ContactDetails#`)**
```
ContactDetails
Address
ContactTypeTerm  subclass of base:DefinedTerm
```
**Cyclicity Terms Ontology (cycle: = `http://rs.tdwg.org/ontology/voc/CyclicityTerm#`)**
```
CyclicityTerm  subclass of base:DefinedTerm
```
**Digital Image Ontology (not functional: defines the ontology as `http://rs.tdwg.org/ontology/voc/ContactDetails` and is incomplete)**

**Geographic Region Ontology (geographic: = `http://rs.tdwg.org/ontology/voc/GeographicRegion#`)**
```
GeographicRegion  subclass of base:DefinedTerm
GeographicRegionLevel1Term  subclass of geographic:GeographicRegion
GeographicRegionLevel2Term  subclass of geographic:GeographicRegion
GeographicRegionLevel3Term  subclass of geographic:GeographicRegion
GeographicRegionLevel4Term  subclass of geographic:GeographicRegion
```
**Institution Ontology (institution: = `http://rs.tdwg.org/ontology/voc/Institution#`)**
```
Institution
```
**Institution Type Ontology (institutiontype: = `http://rs.tdwg.org/ontology/voc/InstitutionType#`)**
```
InstitutionTypeTerm  subclass of base:DefinedTerm
```
**Occurrence Record Ontology (occurrence: = `http://rs.tdwg.org/ontology/voc/OccurrenceRecord#`)**
```
OccurrenceRecord
Identification
```
**Occurrence Status Type Ontology (occurencestatus: = `http://rs.tdwg.org/ontology/voc/OccurrenceStatusTerm#`)**
```
OccurrenceStatusTerm  subclass of base:DefinedTerm
AbsentOccurrenceStatusTerm  subclass of occurencestatus:OccurrenceStatusTerm
PresentOccurrenceStatusTerm  subclass of occurencestatus:OccurrenceStatusTerm
NativeOccurrenceStatusTerm  subclass of occurencestatus:OccurrenceStatusTerm
IntroducedOccurrenceStatusTerm  subclass of occurencestatus:OccurrenceStatusTerm
```
**Person Ontology (person: = `http://rs.tdwg.org/ontology/voc/Person#`)**
```
Person  subclass of core:Person
PersonNameAlias  subclass of  core:Name
```
**Procedure Ontology (not functional: defines the ontology as `http://rs.tdwg.org/ontology/voc/ContactDetails` and is incomplete)**

**Publication Citation Ontology (pubcitation: = `http://rs.tdwg.org/ontology/voc/PublicationCitation#`)**
```
PublicationCitation  subclass of core:PublicationCitation
PublicationTypeTerm  subclass of base:DefinedTerm
```

**Species Profile Model InfoItems Ontology (labeled as "experimental"; contains about 38 classes to be used as a controlled vocabulary)**

**Taxon Concept Ontology (taxonconcept: = `http://rs.tdwg.org/ontology/voc/TaxonConcept#`)**
```
TaxonConcept (no subclassing, declared equivalent to Taxon)
Taxon (no subclassing, declared equivalent to TaxonConcept)
```
**Taxon Name Ontology (taxonname: = `http://rs.tdwg.org/ontology/voc/TaxonName#`)**
```
TaxonName (no subclassing)
NomenclaturalType (no subclassing)
NomenclaturalTypeTypeTerm (no subclassing)
NomenclaturalNote (no subclassing)
NomenclaturalNoteTypeTerm (no subclassing)
NomenclaturalCodeTerm (no subclassing)
```
**Taxon Occurrence Ontology (taxonoccurrence: = `http://rs.tdwg.org/ontology/voc/TaxonOccurrence#`)**
```
TaxonOccurrence
Identification
BasisOfRecordTerm
```
**Interaction Ontology (interaction: = `http://rs.tdwg.org/ontology/voc/TaxonOccurrenceInteraction#`)**
```
TaxonOccurrenceInteraction (no subclassing) 
InteractionTerm  subclass of base:DefinedTerm
```
**Taxon Rank Ontology (ontology incorrectly identified as `http://rs.tdwg.org/ontology/voc/TaxonName`)**
```
TaxonRankTerm  subclass of base:DefinedTerm
```

**Team Ontology (team: = `http://rs.tdwg.org/ontology/voc/Team#`)**
```
Team  subclass of core:Team
TeamMember 
```
**Term with Source Ontology (ontology incorrectly identified as `http://rs.tdwg.org/ontology/voc/CollectionType`)**
```
TermWithSource
```

## 2. Type vocabularies ##

#### 2.1. DCMI Type Vocabulary classes (`dctype: = http://purl.org/dc/dcmitype/`) ####
```
Collection
Dataset
Event
Image
InteractiveResource
MovingImage  subclass of dctype:Image
PhysicalObject
Service
Software
Sound
StillImage  subclass of dctype:Image
Text
```
#### 2.2. Darwin Core Type Vocabulary classes (`dwctype: = http://rs.tdwg.org/dwc/dwctype/`) ####
```
Occurrence
dctype:Event (note: references the Dublin Core type)
Location
Taxon
PreservedSpecimen
FossilSpecimen
LivingSpecimen
HumanObservation
MachineObservation
NomenclaturalChecklist
```

### 1 Dublin Core classes ###
Human readable at http://dublincore.org/documents/dcmi-terms/#H6

RDF at http://dublincore.org/2010/10/11/dcterms.rdf

### 2 Darwin Core Quick Reference Guide ###
http://rs.tdwg.org/dwc/terms/index.htm

### 3 FOAF vocabulary ###
Human readable at http://xmlns.com/foaf/spec/

RDF at http://xmlns.com/foaf/spec/index.rdf

### 4 TDWG Ontology ###
Human readable at http://wiki.tdwg.org/twiki/bin/view/TAG/TDWGOntology

RDF at: http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/

### 5 Taxonomic Concept Transfer Schema ###
http://www.tdwg.org/standards/117/

### 6 Natural Collections Descriptions (NCD) draft TDWG standard ###
Human readable http://www.tdwg.org/standards/312/

RDF at

http://rs.tdwg.org/ontology/voc/Collection

http://rs.tdwg.org/ontology/voc/Institution

http://rs.tdwg.org/ontology/voc/InstitutionType

http://rs.tdwg.org/ontology/voc/ContactDetails

Use view page source to view RDF; however, a note at that page says management of the vocabulary is now at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/