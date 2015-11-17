**See [this page](DwcClassChanges.md) for a summary of the proposed changes.**

## Major revision of Section 2.3.1.5 caused by class proposal ##
#### 2.3.1.5 Classes to be used for type declarations of resources described using Darwin Core ####

The TDWG GUID Applicability Statement standard [GUID-STANDARD](http://www.tdwg.org/standards/150/) specifies that an object in the biodiversity domain that is identified by a GUID should be typed using a well-known vocabulary. With this recommendation in mind, it should be considered a best practice to provide information about the type (i.e. class membership) of any resource that is assigned a persistent identifier in the form of a URI.  Since Darwin Core is a well-known vocabulary and a ratified TDWG standard, its classes should be used for typing in preference to classes in parts of the TDWG ontology which are not ratified standards.  This guide does not specify what specific kinds of resources should be included within particular Darwin Core classes since that is a matter for community consensus ([Section 1.4.4](#1.4.4_Limitations_of_this_guide.md)).

Darwin Core includes two categories of classes.  There are a number of classes defined within the general Darwin Core terms namespace (_dwc:_=`http://rs.tdwg.org/dwc/terms/`).  Another class, _dcterms:Location_, is imported from the Dublin Core (_dcterms:_=`http://purl.org/dc/terms/`) vocabulary.

In addition to classes within Darwin Core, the following classes from the Dublin Core type vocabulary may be used for typing biodiversity-related resources:

<dl><dt><i>dcmitype:StillImage</i></dt><dt><i>dcmitype:MovingImage</i></dt><dt><i>dcmitype:Sound</i></dt><dt><i>dcmitype:PhysicalObject</i></dt></dl>

As of the writing of this guide, there are no rigorously defined classes for taxon concepts and taxon names as they are described in the TDWG Taxon Concept Transfer Schema Standard  [TCS](http://www.tdwg.org/standards/117/) (although the class _dwc:Taxon_ approximates a taxon concept).  As of the writing of this guide, there is not yet guidance for using property terms from a ratified TDWG standard to construct descriptions of taxon concepts.  When such descriptions are available, the term _dwcuri:toTaxonConcept_ may be used to link to them.  Until that time, Darwin Core convenience terms listed under the _dwc:Taxon_ class may be used as properties of _dwc:Identification_ instances to facilitate searching ([Section 2.7.4](#2.7.4_Description_of_a_taxonomic_entity.md)).


## Additional changes ##

Section 1.4.4: Change "Therefore it is outside of the scope of this guide to advise RDF users about what particular kinds of resources should be considered instances of less well-defined Darwin Core classes such as dwctype:Occurrence and dwctype:Event." to "Therefore it is outside of the scope of this guide to advise RDF users about what kinds of resources should be considered instances of particular Darwin Core classes."

Section 2.1.1: remove reference to dwctype: namespace abbreviation.

Section 2.1.2 remove dwctype: from attribute list.

Section 2.3.1 change dwctype:PreservedSpecimen to dwc:PreservedSpecimen .

Section 2.3.1.4 change dwctype:PreservedSpecimen to dwc:PreservedSpecimen .

Section 2.6 change http://rs.tdwg.org/dwc/dwctype/Identification to http://rs.tdwg.org/dwc/terms/Identification and dwctype:Identification to dwc:Identification .

Section 2.6.1 change http://rs.tdwg.org/dwc/dwctype/Identification to http://rs.tdwg.org/dwc/terms/Identification and dwctype:Identification to dwc:Identification .

Section 2.7.3: change http://rs.tdwg.org/dwc/dwctype/PreservedSpecimen to http://rs.tdwg.org/dwc/terms/PreservedSpecimen and dwctype:PreservedSpecimen to dwc:PreservedSpecimen .

Section 2.7.4: change dwctype:Taxon to dwc:Taxon .  Change http://rs.tdwg.org/dwc/dwctype/Identification to http://rs.tdwg.org/dwc/terms/Identification and dwctype:Identification to dwc:Identification .

Section 2.7.6 change http://rs.tdwg.org/dwc/dwctype/GeologicalContext to http://rs.tdwg.org/dwc/terms/GeologicalContext and dwctype:GeologicalContext to dwc:GeologicalContext .

Section 3.5 change "dwctype:Taxon or dwc:Taxon" to "dwc:Taxon".