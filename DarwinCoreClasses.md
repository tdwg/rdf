Prepared 2012-04-13 by Steve Baskauf (steve.baskauf@vanderbilt.edu)

**Table of Contents:**



# Introduction #
This discussion summary does not include the class dwc:GeologicalContext, which has not been the subject of much discussion, nor does it include the Auxiliary Term classes (which have been the subject of some discussion that has not been summarized).

A general introduction to Darwin Core is at http://rs.tdwg.org/dwc/index.htm .  An authoritative guide to the classes of Darwin Core is at http://rs.tdwg.org/dwc/terms/index.htm .  That page also groups property terms under the classes (although there are no formally defined domain relationships between property and class terms.  The abstract model which underlies Darwin Core is described at http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#abstractmodel .

An attempt to show the relationship of Darwin Core to the ASC (Association of Systematics Collections) model developed in 1992 is at http://code.google.com/p/darwin-sw/wiki/RelationshipToExistingModels .  This page also attempts to show how the existing Darwin Core classes might be extended to include "Individuals" (organisms) and "Tokens" (evidence) as discussed at the end of this page.

The introductory paragraph of http://rs.tdwg.org/dwc/terms/history/index.htm provides information about the pre-standard versions of Darwin Core and http://rs.tdwg.org/dwc/terms/history/versions/index.htm provides mappings of those versions to the current standard.

The public review of the current standard began in July 2009 and the discussion associated with and subsequent to that review can be viewed at http://lists.tdwg.org/pipermail/tdwg-content/.

# The dcterms:Location class #
< Note added 2013-10-25: In the discussion which led up to the creation of the Darwin Core RDF Guide, it was felt that it was desirable to use the more well-known Dublin Core classes rather than Darwin Core-defined classes.  Because of this, the RDF Guide specifies that dcmitype:Event (http://purl.org/dc/dcmitype/Event ) and dcterms:Location (http://purl.org/dc/terms/Location) be included in the Darwin Core type vocabulary and used for typing resources rather than the Darwin Core-defined analogues dwc:Event (http://rs.tdwg.org/dwc/terms/Event ) and dwctype:Location (http://rs.tdwg.org/dwc/dwctype/Location ). >

Strictly speaking, Darwin Core does not define a location class because it simply adopts the corresponding Dublin Core class http://purl.org/dc/terms/Location .  However, the Darwin Core type vocabulary does define a term dwctype:Location (http://rs.tdwg.org/dwc/dwctype/Location) which does not have any formal relationship to dcterms:Location .

It was suggested at the iDigBio meeting in March 2012 that Darwin Core should have a separate class for geolocation, since any particular dcterms:Location instance may have multiple geolocation instances.  If this were done, some terms which are currently listed under the dcterms:Location class would be moved to the new class.  However, there has not yet been any official proposal to make such a change.

# The dwc:Event class #
(Modified from [Darwin-SW wiki page ClassEvent](http://code.google.com/p/darwin-sw/wiki/ClassEvent).)

< Note added 2013-10-25: In the discussion which led up to the creation of the Darwin Core RDF Guide, it was felt that it was desirable to use the more well-known Dublin Core classes rather than Darwin Core-defined classes.  Because of this, the RDF Guide specifies that dcmitype:Event (http://purl.org/dc/dcmitype/Event) and dcterms:Location (http://purl.org/dc/terms/Location) be included in the Darwin Core type vocabulary and used for typing resources rather than the Darwin Core-defined analogues dwc:Event (http://rs.tdwg.org/dwc/terms/Event ) and dwctype:Location (http://rs.tdwg.org/dwc/dwctype/Location ). >

Although it is possible to assign separate space/time coordinates (i.e. time, latitude, and longitude) to each Occurrence, some users may prefer to group multiple Occurrences within a single Event.<sup>1</sup>  Likewise, several Events can occur at one defined Location at different times.  Thus the Event class functions primarily as a node to connect one or  more Occurrences to an Event, and one or more Events at a Location.<sup>2</sup>

Because the Event class represents a "join" between other classes, it is difficult to define exactly what it represents conceptually.<sup>3</sup> At a minimum, an Event represents time and Location information, but it also implies some act (e.g. collecting, photographing, etc.) so metadata related to the methodology (e.g. sampling method, effort, etc.) can be included as properties of the event.<sup>4</sup> <sup>5</sup>  The origin of the concept of Event as embodied in DwC can probably be traced back to the Association of Systematics Collections (ASC) model.<sup>6</sup> <sup>7</sup>  It should be noted that Dublin Core defines an Event class (http://purl.org/dc/dcmitype/Event) in its type vocabulary.  However, there is no formal relationship between dcmitype:Event and dwc:Event .

Although time could be described as an explicit class with its own terms<sup>8</sup>, in the current DwC model time properties are included within the Event class.

<sup>1</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001685.html

<sup>2</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001703.html

<sup>3</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001797.html and subsequent posts.

<sup>4</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001801.html

<sup>5</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001804.html

<sup>6</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001799.html

<sup>7</sup> http://wiki.tdwg.org/twiki/bin/viewfile/TAG/HistoricalDocuments?rev=1;filename=Ascmodrpt.pdf

<sup>8</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001771.html

# The dwc:Identification class #

(Modified from [Darwin-SW wiki page ClassIdentification](http://code.google.com/p/darwin-sw/wiki/ClassIdentification).)

The dwc:Identification class connects a subject resource to a Taxon.  Taxon is understood to be an instance of a taxon concept or taxon name usage (see the discussion of the Taxon class).  The subject resource may be assigned several identifications.  Each identification should be a separate instance of dwc:Identification.

Note: it is not entirely clear what should be the subject of an identification.  During discussion on the tdwg-content email list, there seemed to be agreement that the actual thing which was being identified was an organism (or clone or group of organisms).  However, DwC does not have any class for this, so people typically talk about identifications applying to Occurrences or specimens.  There is significant ambiguity here.

## Notes on the Identification class ##

No distinction is made between the initial identification and subsequent identifications made by persons who "annotate" evidence (e.g. specimens) at a later time.  "Identification" in this case is synonymous with "determination"; therefore the person doing the identifying could be referred to as the "determiner" rather than the "identifier" (to avoid confusion with use of "identifier" as in "globally unique identifier").<sup>1</sup> <sup>2</sup> <sup>3</sup>

The term identificationReferences is "a list of references
used in the assessment to make the determination. The dwc:identificationReferences might include taxonomic treatments, but they might also include something such as an expert range map or a field guide".<sup>4</sup>  identificationReferences is a string literal property populated with a concatenated text list of sources that were consulted.  dwc:identificationReferences is distinguished from dwc:nameAccordingTo which is a property of Taxon.  nameAccordingTo is intended to convey the publication which establishes the concept by circumscription or description of the characters which delineate the taxon.<sup>4</sup> <sup>2</sup>   (See the Taxon class discussion for more on this.)

<sup>1</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001694.html

<sup>2</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001703.html

<sup>3</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001708.html

<sup>4</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001704.html

# The dwc:Taxon class #

(Modified from [Darwin-SW wiki page ClassTaxon](http://code.google.com/p/darwin-sw/wiki/ClassTaxon).)

## What is a Taxon? ##
< Note added 2013-10-25 by Steve Baskauf: Since this page was originally made, there was a discussion thread about Taxon Concepts and Taxon Name Uses (TNUs) [here](http://code.google.com/p/tdwg-rdf/wiki/TCSthread).  As a result, the diagram [here](http://code.google.com/p/tdwg-rdf/wiki/TCSBasedTaxon) was created.  The apparent consensus reached in the discussion thread informed the document [Describing Taxon Concepts as RDF](http://code.google.com/p/tdwg-rdf/wiki/TaxonInRDF) which is an ancillary document related to the proposed Darwin Core RDF Guide, although not included as part of the standard itself. >

A taxon is a unit of biodiversity (Hyam and Kennedy, 2006) e.g. species, genus, family, etc.  However, taxonomists consider a particular taxon to be defined not only by a name, but also by an understanding of what organisms should be included in the taxon under that name.  Taxa can be referenced in varying degrees of detail:
  1. **Nominal Taxon Concept** (a.k.a."nominal taxon" and "nominal concept") - reference is made to a taxon name but no information is available about how the user intends for that name to be applied.  Such instances could be referenced by "placeholder" Taxon instances which contained with no nameAccordingTo, and no other metadata besides the scientificName.<sup>1</sup> <sup>2</sup>
  1. **Taxon Name Usage (TNU)** (synonym: **assertion**, defined in Pyle,2004,p.20) - reference is made to a taxon name with some indication of what the author intends the name to mean.  This may or may not include published details about how the author intends to define the taxon.<sup>3</sup> <sup>4</sup>
  1. **Taxon Concept** - reference is made to a taxon name along with a publication which explains how the author intends for the name to be applied (Kennedy et al. 2005, p.81).  The name used is followed by "_sec._" (_secundum_) or "_sensu_", then a citation for the reference which explains the author's intention.  A taxon concept may be considered to be a more rigorously defined TNU<sup>5</sup> <sup>6</sup>; a "defined" taxon concept rather than an "implied" taxon concept (i.e. TNU). <sup>7</sup>

A taxon concept can be defined by a **circumscription** which refers to a collection of specimens that represent the concept.  Alternatively, a taxon concept can defined by describing the characters that define the concept (Kennedy et al., 2005, p.84).

**Note:**  A reference defining a taxon concept is not necessarily synonymous with the reference which published the name (although it could be if the intended concept was also expressed by the author when the name was published).  Thus a text representation identifying a taxon concept could be:

genus+specificEpithet+scientificNameAuthorship+ "_sec._" (or "_sensu_")+ conceptAuthor+publicationDate

for example:

_Aus bus_ L. 1758 _sec._ Archer 1965

where the species name was published by Linnaeus in 1758 and the taxon concept describing _Aus bus_ was published by Archer in 1965.  The Darwin Core term dwc:nameAccordingTo is for the concept publication, whereas the dwc:namePublishedIn term is for the name publication.

**Note** If no dwc:nameAccordingTo or dwc:nameAccordingToID is given explicitly given for a Taxon record, the nominal concept as defined by TCS should be assumed - so the Taxon could be a taxon concept **OR** a nominal concept.

## Equivalence of "Taxon" in the Darwin Core standard and "TaxonConcept" in the TDWG Ontology ? ##
Unfortunately, there is some lack of clarity about what exactly constitutes an instance of Taxon in the DwC standard.  The terms listed under the Taxon class in DwC are a mixture of terms which could apply to both taxa and names.  The meaning of Taxon is clearer in the TDWG Ontology.  In particular, Taxon and TaxonConcept are defined to be equivalent classes according to their definitions under the URI http://rs.tdwg.org/ontology/voc/TaxonConcept.owl which is hosted and can be viewed at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.owl .  The Taxon component of the TDWG Ontology seems to be the part of the Ontology that is the most well-supported by other standards (e.g. TCS; see Hyam and Kennedy, 2006), it is the part of the Ontology to which the most effort seems to have been applied, and it also seems to be one of the few parts of the Ontology that has actually been implemented by anyone.

It has been noted by some of the architects of the DwC standard that the term dwc:taxonID is intended to represent a "nameUsageID"<sup>8</sup> and thus instances of TNUs could be described using the vocabulary of the dwc:Taxon class.  Since taxon concepts can be considered a more narrowly defined subset of TNUs, by extension terms in the dwc:Taxon class could apply to them as well.  Because terms in the Darwin Core standard do not have strictly defined domains and because the DwC standard does not explicitly define a class for names or sensu/secundum references, there are also some terms listed under the Taxon class that may apply specifically to names or sensu/secundum references rather than TNUs/taxon concepts.

Hyam, R. and J. Kennedy. 2006. Taxon Concept Schema - User Guide.  http://www.tdwg.org/standards/117/

Kennedy, J.B., R. Kukla, and T. Paterson. 2005. Scientific names are ambiguous as identifiers for biological taxa: their context and definition are required for accurate data integration.  Data Integration in the Life Sciences 2005, LNBI 3615, 80-95.  http://www.springerlink.com/content/7bv5pa3falxwrrvx/

Pyle, R.L. 2004. Taxonomer: a relational data model for managing information relevant to taxonomic research.  PhyloInformatics 1:1-54.  http://systbio.org/files/phyloinformatics/1.pdf

Franz, N.M. and J. Cardona-Duque. 2013. Description of two new species and phylogenetic reassessment of Perelleschus O’Brien & Wibmer, 1986 (Coleoptera: Curculionidae), with a complete taxonomic concept history of Perelleschus sec. Franz & Cardona-Duque, 2013.  Systematics and Biodiversity 11:209-236. http://dx.doi.org/10.1080/14772000.2013.806371

<sup>1</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001703.html

<sup>2</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001814.html

<sup>3</sup> http://lists.tdwg.org/pipermail/tdwg-content/2009-November/000268.html

<sup>4</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001831.html

<sup>5</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001820.html

<sup>6</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001835.html

<sup>7</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001840.html

<sup>8</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001814.html

Note: there are numerous threads on the tdwg-content mailing list about the subject of taxa and taxon concepts.  I do not have the stamina to summarize them all here, but some entry points to several threads are:

http://lists.tdwg.org/pipermail/tdwg-content/2010-June/000188.html

http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001585.html

http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001819.html


# The dwc:Occurrence class #

(Modified from [Darwin-SW wiki page ClassOccurrence](http://code.google.com/p/darwin-sw/wiki/ClassOccurrence).)

The Occurrence class represents instances where the presence of an organism at a location is documented.  It functions primarily as a node that connects organisms to Events and as well as to evidence that supports the record (e.g. preserved specimens).  In Darwin Core, properties that perhaps should be separated out into properties of specimens, properties of organisms, and properties of occurrences are all lumped together in a single class.  For this reason, members of the TDWG community now commonly use the term "occurrence" synonymously with "specimen" and sometimes synonymously with "observation".

## Definitions of Occurrence ##

The Occurrence class is perhaps the most difficult to define of any of the classes included in Darwin Core.  Occurrence resources are at the intersection of several other classes and depending on where the boundaries occur, various components may or may not be included in the definition.<sup>1</sup>  There is a general consensus that an Occurrence is related to the events, individual organisms, and the evidence used to support the Occurrence.  This relationship has resulted in several definitions of Occurrence.  An Occurrence can be formally defined as "a tuple of (Individual, Event), and has properties for referring to the Individual and the Event." <sup>2</sup> (A tuple is defined as an ordered list of elements and has a technical meaning in the programming community.)  An alternative way of expressing this using terminology of the database world would be to say that an Occurrence is a "a many-to-many join between Events and Individuals, with a few additional properties".<sup>3</sup>  In RDF terminology an Occurrence could be said to be a node that is connected by object properties to instances of the Event and individual organisms (which are not currently represented by any DwC class).

<sup>1</sup> http://code.google.com/p/darwincore/issues/detail?id=70

<sup>2</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001782.html

<sup>3</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001785.html

## Scope of Occurrence ##

Part of the confusion about the meaning of "an occurrence" stems from the historical use of the term to refer both to a primary unit of data gathering (i.e. that an individual of a taxon occurred at a particular time and place) and also to the result of modeling (i.e. we know from aggregate records that a taxon occurs or ever occurred, in a particular geographic area).<sup>1</sup>  This second use has been referred to as the "checklist" use of occurrence<sup>2</sup> (i.e. indicating the presence of a taxon in an area on a list of taxa present) and is different enough from the first type of use that it has actually been described as a separate class: "Distribution".<sup>3</sup>  However, it has been pointed out<sup>4</sup> that the "checklist" use of Occurrence is actually related to the first use if the relationship
```
TaxonConcept <--> Occurrence <--> Event <--> Location
```
is collapsed to
```
TaxonConcept <--> Location
```
The argument has also been made<sup>4</sup> that the difference between these two views is simply a matter of scale and on that basis it may not make sense to create a distinction between the two.<sup>5</sup>  As a practical matter, there seems to be a fairly clear distinction between properties that should be applied to the first type of use (e.g. dwc:recordedBy) and those that should be applied to the second type (e.g. dwc:occurrenceStatus).

<sup>1</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001631.html

<sup>2</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001633.html

<sup>3</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001650.html

<sup>4</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001638.html

<sup>5</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001642.html

## What is included within the boundaries of the Occurrence class? ##

Although most references to occurrences carry the connotation of a taxon representative documented by evidence at a place and time, there has been considerable variation in which of these aspects of an occurrence are assumed to be included as a part of the Occurrence resource itself.

~~The definition of Occurrence as a subclass of dctype:Event (http://purl.org/dc/dcmitype/Event) in the Darwin Core type vocabulary<sup>1</sup> carries the connotation that an occurrence resource includes the event at which the resource was recorded/observed/collected.<sup>2</sup>~~  (Note: in Darwin Core Decision-2011-10-16\_6 at http://rs.tdwg.org/dwc/terms/history/decisions/index.htm the subclass declarations of terms in the Dawin Core Type vocabulary have been removed.)

More widely held is the understanding that an occurrence resource also includes the evidence which serves as the documentation that the occurrence happened.<sup>3</sup> In particular, at the time that the Darwin Core standard was ratified specimens were considered to "be" Occurrences, not just to serve as evidence for Occurrences.<sup>4</sup>  This view is reflected by the inclusion of terms which refer to specimens (e.g. dwc:preparations<sup>5</sup>) within the Occurrence class of DwC<sup>6</sup> and the definition of the Darwin Core type PreservedSpecimen as a subclass of Occurrence.<sup>1</sup> (This subclass relationship has been removed as of 2011-10-16.)  However, this view was not universally held.<sup>7</sup>  Considering Occurrence resources to include the evidence that supports them introduces serious difficulties when one tries to describe them in RDF,<sup>8</sup> so it has been proposed that Occurrences should be separated from Individuals and the evidence (also known as "Token") that supports Occurrences.<sup>9</sup>  However, no action has been taken on this proposal pending further discussion, clarification, and community consensus.

<sup>1</sup> http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwctype.rdf

<sup>2</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001828.html

<sup>3</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001681.html

<sup>4</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-November/001836.html and http://lists.tdwg.org/pipermail/tdwg-content/2009-June/000441.html

<sup>5</sup> http://rs.tdwg.org/dwc/terms/index.htm#preparations

<sup>6</sup> http://rs.tdwg.org/dwc/terms/index.htm

<sup>7</sup> http://lists.tdwg.org/pipermail/tdwg-content/2009-October/000291.html

<sup>8</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001742.html

<sup>9</sup> http://lists.tdwg.org/pipermail/tdwg-content/2011-July/002575.html

## Relationship of "observations" to Occurrences ##

In earlier drafts of Darwin Core, separate terms were defined for properties of observations and properties of specimens.  The creation of the Occurrence class was in part a recognition that there was a fundamental similarity in metadata which described observations and metadata which described specimens.  In the DwC standard, a single term in the Occurrence class, such as dwc:recordedBy, replaces separate terms (e.g. collector<sup>1</sup> or observer) that apply to specimens and observations but which fundamentally represent the same thing.  Taking the approach that a Token is separate from an Occurrence leads to the question of the nature of the Token that supports an "observation"<sup>2</sup>.  One approach is to define observations as Occurrences that do not have tokens.<sup>3</sup>  Another is to define a class of Token called something like "Observation" in recognition that even observations have evidence, although that evidence may not be as accessible as an image or a specimen.<sup>4</sup> <sup>5</sup>  An advantage of this approach is that it would allow Observation class Tokens to be assigned identifiers and described using existing vocabularies for Observations.<sup>6</sup>

<sup>1</sup> http://rs.tdwg.org/dwc/terms/history/versions/index.htm

<sup>2</sup> "Observation" suffers from the same problem as "occurrence" in the sense that it is vague in the absence of a clear definition.  In fact, one could take the position that "observations" are essentially what darwin-sw asserts Occurrences to be, i.e. the record that a taxon representative was present at a certain time and place apart from the evidence (Token) that supports that record.  See http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001743.html for a historical reference to this outlook.  It is also possible to consider an "observation" to be a type of dctype:Event.  However, this fails to make a distinction between "observation" as an act (i.e. sensu Event) and "observation" as the product of that act (i.e. sensu Token).  See http://lists.tdwg.org/pipermail/tdwg-content/2009-November/000263.html for discussion of this distinction.

<sup>3</sup> _Biodiversity Informatics_ 7:17-44.  https://journals.ku.edu/index.php/jbi/article/view/3664

<sup>4</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001743.html

<sup>5</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001755.html

<sup>6</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001736.html

## Separating the use of Occurrences in documenting species distributions from the declaration of a resource as an instance of the class Occurrence ##

The use of the term "occurrence" to describe the kinds of things included in the dwc:Occurrence class may lead to the misconception that all instances of the class must serve the purpose of documenting a "valid" occurrence of a taxon in its "natural" environment.<sup>1</sup>  However, it has been made clear that there is no expectation that an instance of the Occurrence class must be suitable for modeling species distributions, only that it represent the presence of a particular taxon representative at a particular time and location.  It is not necessary that the location, time, or taxon necessarily be known<sup>2</sup> but the Occurrence cannot refer to a generic representation of a taxon such as a diagram or generic illustration.<sup>3</sup>  In DwC, the appropriate term for describing whether an Occurrence is a "natural occurrence" (i.e. indicating that the Occurrence is suitable for modeling a taxon's distribution excluding captive or cultivated Occurrences) is dwc:establishmentMeans<sup>4</sup>.  However, extensive discussion<sup>5</sup> of the use of dwc:establishmentMeans revealed that there was substantial disagreement about what should be permissible as the controlled vocabulary for that term and even the DwC class under which the term should be listed<sup>6</sup>.  The conclusion (if there actually was one!) was that the term dwc:establishmentMeans implied a property that was associated by complex relationships with several existing DwC classes<sup>7</sup> <sup>8</sup> <sup>9</sup>.  Thus it is probably impossible to assign a domain to dwc:establishmentMeans which is any existing DwC class.


<sup>1</sup> http://lists.tdwg.org/pipermail/tdwg-content/2009-October/000282.html

<sup>2</sup> http://lists.tdwg.org/pipermail/tdwg-content/2009-October/000280.html

<sup>3</sup> http://lists.tdwg.org/pipermail/tdwg-content/2009-October/000289.html

<sup>4</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001612.html

<sup>5</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001611.html and many subsequent posts in that thread.

<sup>6</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001629.html

<sup>7</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001644.html

<sup>8</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001646.html

<sup>9</sup> http://lists.tdwg.org/pipermail/tdwg-content/2010-October/001731.html

# The proposed "dwc:Individual" class #
A proposal was made in 2010-01 (http://code.google.com/p/darwincore/issues/detail?id=69) to add a class called "Individual".  There was extensive discussion of this proposal and during that discussion it was suggested that other names such as "IndividualOrganism", "TaxonomicallyHomogeneousEntity", "BiologicalIndividual", "BiologicalEntity", "Organism", and "DataSets/DataSet/Units/Unit" would be more appropriate.  In 2011-09, the proposal was effectively tabled until a broader consensus was reached as to how the relationships among Individuals, Occurrences, Specimens, Tokens, etc. should be defined.  The Darwin Semantic Web (Darwin-SW) ontology (not sanctioned by TDWG) defines classes for IndividualOrganism, Token, and Specimen and provides a rational for doing so at:

http://code.google.com/p/darwin-sw/wiki/ClassIndividual

http://code.google.com/p/darwin-sw/wiki/ClassToken

http://code.google.com/p/darwin-sw/wiki/ClassSpecimen

http://code.google.com/p/darwin-sw/wiki/TokenIssues

http://code.google.com/p/darwin-sw/wiki/TaxonomicHeterogeneity

These pages summarize the discussion of these topics that took place on the tdwg-content mailing list.