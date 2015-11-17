## Submitters: ##

John Wieczorek, Joel Sachs, James Macklin, Markus Döring, Rich Pyle, Tim Robertson, Bob Morris, Hilmar Lapp, and Steve Baskauf.

## Date: ##
2014-01-16

## Justification: ##

This material is taken from [Issue 204](http://code.google.com/p/darwincore/issues/detail?id=204) of the Darwin Core Issue Tracker.

A number of problems related to classes in Darwin Core were identified and discussed at the Documenting Darwin Core workshop at TDWG 2013.  There was an apparent consensus at the meeting regarding steps that should be taken to fix these problems.  In particular:
  * Darwin Core classes exist in two namespaces, `dwc:` (`http://rs.tdwg.org/dwc/terms/`) and `dwctype:` (`http://rs.tdwg.org/dwc/dwctype/`).  In some cases, there are parallel terms in both namespaces.  To reduce confusion when typing resources, all Darwin Core-defined classes should be in a single namespace.
  * The class definitions contain phrases such as "The category of information pertaining to " and "A resource describing " which make it unclear what entities should be considered instances of those classes.  The class definitions should define the types of the entities themselves and not categories or records related to the entities.
  * Some class definitions are unclear, e.g. are circular or contain ambiguous terms.  Class definitions should be clear enough that users will know what entities should be included in the class.
  * Concerns about the inclusion of an "Individual" or "Organism" class ([Issue 69](https://code.google.com/p/tdwg-rdf/issues/detail?id=69)) seemed to have been allayed and an adequate constituency felt that its inclusion in Darwin Core would be beneficial and would help in clarifying the definitions of some of the ambiguous classes.

An ad hoc group (the submitters of this issue) volunteered or were drafted to turn this consensus into concrete proposals for clarifying the Darwin Core class terms.  That group proposes the following general changes to address the problems identified above:
  1. All Darwin Core-defined class terms will be defined in the `http://rs.tdwg.org/dwc/terms/` (`dwc:`) namespace.
  1. `dcterms:Location` (`http://purl.org/dc/terms/Location`), which is imported into Darwin Core from Dublin Core will continue to be used as a class in Darwin Core.
  1. The terms in the `http://rs.tdwg.org/dwc/dwctype/` (`dwctype:`) namespace, which are all class terms, will be deprecated.  `dwc:` namespace analogues will be created for any `dwctype:` classes that don't already have analogues.  This deprecation includes no longer importing `dcmitype:Event` (`http://purl.org/dc/dcmitype/Event`), whose definition is confusing in the presence of an Occurrence class.
  1. [Issue 69](http://code.google.com/p/darwincore/issues/detail?id=69) will be resolved by the addition of the `dwc:Organism` class (`http://rs.tdwg.org/dwc/terms/Organism`).
  1. Each class term definition will be modified so that it defines the entities included in the class rather that a "category" or data record about the entity.  This generally means removing the phrases "The category of information pertaining to " and "A resource describing " from the definition.
  1. Ambiguous class definitions will be modified so that users are clear about what entities are included in them.  This may be accomplished using in the definition English or URI terms whose meanings are well-known.

**Note:** `dwctype:MaterialSample` is the only Darwin Core class whose normative RDF definition includes a machine-readable (i.e. non-literal) property that links it to another class.  It is defined in the RDF as `rdfs:subClassOf OBI:0100051` (`http://purl.obolibrary.org/obo/OBI_0100051`).  Under the current proposal this linkage would be removed since as a `dwctype: namespace` term, `dwctype:MaterialSample` would be deprecated and since the `dwc:` namespace analogue, `dwc:MaterialSample` does not include this linkage.

To facilitate public discussion about the definitions of particular classes, each class which is new or which has a changed definition will be entered as a separate issue with reference to this issue as the overall rationale for the change.

## Summary of proposed changes ##

See the [Darwin Core Issue Tracker](http://code.google.com/p/darwincore/issues/list) for the actual proposed changes.

|**class terms (existing and proposed additions)**|**proposed revised definitions**|**existing dwc: namespace analogue**|**existing dwctype: namespace analogue to be deprecated**|Issue|
|:------------------------------------------------|:-------------------------------|:-----------------------------------|:--------------------------------------------------------|:----|
|dwc:Organism                                     |A particular organism or defined group of organisms considered to be taxonomically homogeneous.  An organism in the sense used here is defined as OBI:0100026 (http://purl.obolibrary.org/obo/OBI_0100026).  Instances of the Organism class are intended to facilitate linking of one or more Identification instances to one or more Occurrence instances.  Therefore, things that are typically assigned scientific names (such as viruses, hybrids, and lichens) and aggregates whose occurrences are typically recorded (such as packs, clones, and colonies) are included in the scope of this class.  |none                                |none                                                     |[205](http://code.google.com/p/darwincore/issues/detail?id=205)|
|dwc:Occurrence                                   |The existence of a dwc:Organism (http://rs.tdwg.org/dwc/terms/Organism) at a particular place at a particular time.|dwc:Occurrence                      |dwctype:Occurrence                                       |[212](http://code.google.com/p/darwincore/issues/detail?id=212)|
|dwc:MaterialSample                               |The physical results of a sampling (or subsampling) event. In biological collections, the material sample is typically collected, and either preserved or destructively processed.|dwc:MaterialSample                  |dwctype:MaterialSample                                   |[213](http://code.google.com/p/darwincore/issues/detail?id=213)|
|dwc:Event                                        |An action that occurs at a place and time.|dwc:Event                           |dcmitype:Event                                           |[214](http://code.google.com/p/darwincore/issues/detail?id=214)|
|dcterms:Location                                 |A spatial region or named place.|dcterms:Location                    |dwctype:Location                                         |[215](http://code.google.com/p/darwincore/issues/detail?id=215)|
|dwc:GeologicalContext                            |Geological information, such as stratigraphy, that qualifies a region or place.|dwc:GeologicalContext               |none                                                     |[216](http://code.google.com/p/darwincore/issues/detail?id=216)|
|dwc:Identification                               |A taxonomic determination (e.g., the assignment of a scientific name).|dwc:Identification                  |none                                                     |[217](http://code.google.com/p/darwincore/issues/detail?id=217)|
|dwc:Taxon                                        |A group of organisms considered by taxonomists to form a homogeneous unit. An organism in the sense used here is defined as OBI:0100026 (http://purl.obolibrary.org/obo/OBI_0100026).|dwc:Taxon                           |dwctype:Taxon                                            |[218](http://code.google.com/p/darwincore/issues/detail?id=218)|
|dwc:ResourceRelationship                         |A relationship of one rdfs:Resource (http://www.w3.org/2000/01/rdf-schema#Resource) such as an Occurrence, Taxon, Location, etc., to another.|dwc:ResourceRelationship            |none                                                     |[219](http://code.google.com/p/darwincore/issues/detail?id=219)|
|dwc:MeasurementOrFact                            |A measurement or fact about an rdfs:Resource (http://www.w3.org/2000/01/rdf-schema#Resource) such as an Occurrence, MaterialSample, GeologicalContext, etc.|dwc:MeasurementOrFact               |none                                                     |[220](http://code.google.com/p/darwincore/issues/detail?id=220)|
|dwc:PreservedSpecimen                            |A preserved specimen.           |none                                |dwctype:PreservedSpecimen                                |[206](http://code.google.com/p/darwincore/issues/detail?id=206)|
|dwc:FossilSpecimen                               |A fossilized specimen.          |none                                |dwctype:FossilSpecimen                                   |[207](http://code.google.com/p/darwincore/issues/detail?id=207)|
|dwc:LivingSpecimen                               |A living specimen.              |none                                |dwctype:LivingSpecimen                                   |[208](http://code.google.com/p/darwincore/issues/detail?id=208)|
|dwc:HumanObservation                             |An observation made by one or more people.|none                                |dwctype:HumanObservation                                 |[209](http://code.google.com/p/darwincore/issues/detail?id=209)|
|dwc:MachineObservation                           |An observation made by a machine.|none                                |dwctype:MachineObservation                               |[210](http://code.google.com/p/darwincore/issues/detail?id=210)|
|dwc:NomenclaturalChecklist                       |A nomenclatural checklist.      |none                                |dwctype:NomenclaturalChecklist                           | [211](http://code.google.com/p/darwincore/issues/detail?id=211)|