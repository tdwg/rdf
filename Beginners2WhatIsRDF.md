# Beginner's guide to RDF: 2. What is RDF and what is it for? #

[go to part 1: Resources and URIs](Beginners1URIs.md)

[go to part 3: RDF basics](Beginners3RDFbasics.md)

[Introduction to the Guide](Beginners.md)

**Contents**



## 2.1. What is RDF? ##
RDF stands for Resource Description Framework.  RDF is a method of describing resources that is designed to be easily understood by computers.  It was designed to be a simple, extensible system that would make it possible to draw inferences by combining information from several sources. [(1)](#1_RDF_Motivation_and_Goals.md)

When the World Wide Web was created, it was designed to make it easy for humans to access and comprehend interconnected content created by many users.  The HyperText Markup Language (HTML) was created as a way to accomplish this through Web pages.  There is no question that this effort has been wildly successful.  However, the Web was not designed to allow computers to do the same thing without human help.  Web "scrapers" or "bots" (software designed to explore and extract information from the Web automatically) have been quite successful at guessing the nature of the content on Web pages and compiling that information in centralized repositories.  But they sometimes wrongly interpret the meaning of the pages they "scrape".  In 1999, Tim Berners-Lee, the creator of the Web, enunciated a vision of a "semantic web" in which computers would be able to understand and act on information present on the Web by discovering, aggregating, and interpreting machine-readable metadata that was intentionally provided in a form that was designed to be processed by computers. [(2)](#2_Tim_Berners-Lee_on_the_Semantic_Web.md)

The same year, the World Wide Web Consortium (W3C) published a model and syntax specification for RDF [(3)](#3_Resource_Description_Framework_(RDF)_Model_and_Syntax_Specific.md) as a W3C Recommendation. [(4)](#4_W3C_Recommendations.md)    Since that time, RDF has been used to publish a limited amount of information on the Web and has formed the basis of more complex systems, such the Web Ontology Language (OWL; see [part 7](Beginners7OWL.md) of this guide).  However, the vision of a "semantic web" has not materialized at a speed comparable to the development of the web.

## 2.2. What can RDF be used for? ##
The primary purpose of RDF is to provide information about resources.  The extent and complexity of this information depends on the nature and amount of information provided about the resource and the capability that a user has to combine information about that resource from different sources.  The following sections outline increasingly complex ways that RDF can provide information about resources.

### 2.2.1. Determining the type. ###
A URI is simply a string which uniquely identifies a resource.  Although the form of a URI string might provide clues about the nature of the resource, e.g.
```
http://bioimages.vanderbilt.edu/taxon/18117-fna1993
```
one generally should not draw any conclusions about what kind of thing the resource is without first directly or indirectly obtaining information about the type of the resource.  RDF has established methods for stating the type of a resource. [(5)](#5_Classes_and_types_are_described_in_the_RDF_Schema_(RDFS).md)  See [section 4.4.4.](Beginners4Vocabularies#4.4.4._Using_rdf:type_and_ways_to_determine_instances_of_classes.md) of this guide for more information about this.

### 2.2.2. Determining literal properties. ###
RDF can be used to make statements about characteristics (known as properties) of a resource which can be described using literal strings.  For example, a particular ball can be described as "red" where "red" is a series of characters that humans can understand.  Likewise, a person can be described as having the surname "Smith".  A computer processing this information would have no actual understanding of what "Smith" meant, but could certainly enumerate all of the resources which have the property of a surname of "Smith".  The reason why a computer could not "know" additional things about the literal string is because RDF can only describe the properties of resources identified by URIs, and not the properties of literals.  [Section 3.2.2.](Beginners3RDFbasics#3.2.2._Example_of_a_triple_having_a_literal_as_its_object.md) of this guide provides an example of a declaration of a literal property.

### 2.2.3. Determining properties that are described as relationships to other resources. ###
RDF also can be used to describe properties of a resource by stating how that resource is related to another.  For example one could state that
```
uri1 hasParent uri2
```
From that statement, a computer could learn not only that the resource identified by _uri1_ has a parent, but the computer can find out more about that parent by searching out additional information about _uri2_, e.g. the sex, name, age, etc. of the resource identified by _uri2_.  [Section 3.2.3.](Beginners3RDFbasics#3.2.3._Example_of_a_triple_having_a_URI_as_its_object.md) of this guide provides an example of the declaration of a relationship between two resources.

### 2.2.4. Aggregating information about a resource. ###
When a resource becomes known through discovery of its URI, some properties of the resource may be determined immediately through RDF provided at the time of the discovery.  For example, a client computer may try to dereference the URI and as a result, the server may send one or more statements about the resource in the form of an RDF file (e.g. the ball identified by _uri3_ is red).  However, at a later time additional information may be discovered about that resource when statements are made elsewhere using the URI of the resource (e.g. the ball identified by _uri3_ has a diameter of 3 cm).  Since URIs are globally unique, the user can be confident that the additional statements do in fact apply to the same resource (i.e. the ball _uri3_ is red and has a diameter of 3 cm).  However, there is no guarantee that those statements will actually be true (e.g. the ball _uri3_ has mass=0) or that they will not contradict previously known information about the resource (e.g. the ball _uri3_ is blue).  They are accurate to the degree that their source is reliable.  [Section 5.](Beginners5RDFdata.md) of this guide describes how RDF data can be discovered and aggregated.

### 2.2.5. Drawing inferences about a resource ###
Depending on the amount of information known about the properties used to describe a resource, combining information from two sources may allow the user to conclude properties of the resource that were not previously known.  For example, if it is known from source 1 that
```
uri1 hasParent uri2
```
and from source 2 that
```
uri3 hasParent uri2
```
then if it is known from the definition of the property hasParent that two resources having a common parent are siblings, then it can be inferred that
```
uri1 hasSibling uri3
```
Whether such inferences are correct depends on whether both source 1 and source 2 are providing correct information and whether source 1 and source 2 intend for the property terms to mean the same thing.  For example, source 1 may intend for hasParent to apply only to biological parents where source 2 may understand that hasParent applies to either biological or adoptive parents.  If _uri2_ is the adoptive parent of _uri3_ then a user subscribing to source 1's view may incorrectly conclude that _uri1_ and _uri3_ are biological siblings.  [Section 7.](Beginners7OWL.md) of this guide introduces how complex relationships among resources may be described using Web Ontology Language (OWL).

## 2.3. What is LOD? ##
Linked Open Data (LOD), or simply Linked Data, is community that seeks to connect data that weren't previously linked. [(6)](#6_Linked_Open_Data_Project.md)  It also describes a set of best practices for exposing, sharing, and aggregating data using RDF.  Since the focus of LOD is allowing diffuse users to share and discover data through the Web, the HTTP protocol is the existing technology that is key to making the LOD world possible. [(7)](#7_Frequently_asked_questions_about_LOD.md)  For that reason, LOD proponents favor using HTTP URIs over other forms of identifiers since they can be dereferenced by anyone to discover whatever information their creators wish to be made known.  LOD is described in more detail in [section 5.4.](Beginners5RDFdata#5.4._The_Linked_Open_Data_(LOD)_Cloud.md) of this guide.

## 2.4. What is the Semantic Web? ##
The Semantic Web is a rather nebulous term that is used somewhat interchangeably with LOD.  However, using the term "Semantic Web" carries the connotation that the interconnected Web of Data which is the LOD world might be used by computers to learn and discover things using reasoning.  So persons interested in the Semantic Web may be more prone to focusing on the creation of ontologies that define properties which allow the kind of reasoning described in [section 2.2.5.](#2.2.5._Drawing_inferences_about_a_resource.md) than persons who are more interested in the discovery and exchange of raw data through LOD. [(8)](#8_Linked_Data_vs._the_Semantic_Web.md)  [Section 7.](Beginners7OWL.md) of this guide describes ontologies in more detail.

## 2.5. Why is the biodiversity informatics community interested in RDF? ##
The organization Biodiversity Information Standards (TDWG) [(9)](#9_TDWG_home_page.md) has as its mission to "Develop, adopt and promote standards and guidelines for the recording and exchange of data about organisms". [(10)](#10_About_TDWG.md)  Historically TDWG has promoted data exchange standards such as XML (e.g. in TCS, TAPIR, ABCD, etc. [(11)](#11_TDWG_Standards.md)).  However, transferring data using plain XML requires a pre-existing understanding between the sender and receiver about the format of the data in the form of an XML schema.  In a series of "roadmaps" beginning in 2006 [(12)](#12_TDWG_TAG_2006_roadmap.md) the TDWG Technical Architecture Group (TAG) articulated the goal of developing an infrastructure that would facilitate interoperability among TDWG standards and other standards outside the TDWG domain.  Central to this effort was the development of a system of Globally Unique Identifiers (GUIDs) which could be used to reference objects, and a Semantic Hub that would define the types of objects and the properties used to describe them.  In the 2006 articulation of the TAG goals, it was made clear that the Semantic Hub should not be tied to one particular technology, but rather that the concepts embodied in it should expressible in multiple technologies.  Nevertheless, initial efforts were focused on the development of a particular type of URI-based GUID known as Life Science Identifiers (LSIDs) [(13)](#13_LSID_Best_Practices.md) and a TDWG Ontology expressed in OWL (whose statements are themselves expressed in RDF) [(14)](#14_TDWG_Ontology_Google_Code_repository.md).  This effort ultimately resulted in at least one concrete result: a standard in the form of an applicability guide for the use of GUIDs and LSIDs [(15)](#15_GUID_and_Life_Sciences_Identifiers_Applicability_Statements.md).  However, many users found LSIDs difficult to implement and the TDWG Ontology was difficult to complete and maintain.  Thus the first attempt at implementation of the vision expressed in the TAG roadmaps stalled to some extent.

Despite the failure of GUIDs expressed as URIs and the Semantic Hub expressed as OWL/RDF to quickly materialize as the backbone architecture of TDWG, several aspects of the URI/RDF model have already found their way into the workings of TDWG in two ways.

### 2.5.1. Use of URIs to identify vocabulary terms ###
Following the example of the Dublin Core Metadata Initiative (DCMI) Abstract Model [(16)](#16_DCMI_Abstract_Model.md), URIs are used as the means to unambiguously refer to terms in TDWG standard vocabularies: [Darwin Core (DwC)](http://rs.tdwg.org/dwc/terms/) and the draft [Audubon Core](http://species-id.net/wiki/Audubon_Core) for media resources.  For example,
```
dwc:eventTime
```
is an abbreviated way of referring to the URI
```
http://rs.tdwg.org/dwc/terms/eventTime
```
where "dwc:" is an abbreviation for the namespace "`http://rs.tdwg.org/dwc/terms/`" which ensures that the term eventTime as used in Darwin Core is distinct from any other use of eventTime that might be intended by others.

### 2.5.2. Use of RDF/XML for normative term definitions. ###
In Darwin Core, the normative [(17)](#17_The_TDWG_Standards_Documentation_Specification.md) version of the standard is expressed in RDF serialized as XML. [(18)](#18_Darwin_Core_expressed_in_RDF/XML.md).  For example the definition for the term dwc:eventTime in RDF:

```
<rdf:Description rdf:about="http://rs.tdwg.org/dwc/terms/eventTime">
<rdfs:label xml:lang="en-US">Event Time</rdfs:label>
<rdfs:comment xml:lang="en-US">The time or interval during which an Event occurred. Recommended best practice is to use an encoding scheme, such as ISO 8601:2004(E).</rdfs:comment>
<dcterms:description xml:lang="en-US">Examples: "14:07-0600" is 2:07pm in the time zone six hours earlier than UTC, "08:40:21Z" is 8:40:21am UTC, "13:00:00Z/15:30:00Z" is the interval between 1pm UTC and 3:30pm UTC.</dcterms:description>
<rdfs:isDefinedBy rdf:resource="http://rs.tdwg.org/dwc/terms/"/>
<dcterms:issued>2009-04-24</dcterms:issued>
<dcterms:modified>2009-04-24</dcterms:modified>
<rdf:type rdf:resource="http://www.w3.org/1999/02/22-rdf-syntax-ns#Property"/>
<dcterms:hasVersion rdf:resource="http://rs.tdwg.org/dwc/terms/history/#eventTime-2009-04-24"/>
<dcterms:replaces rdf:resource="http://rs.tdwg.org/dwc/terms/eventTime-2009-04-24"/>
<dwcattributes:status>recommended</dwcattributes:status>
<dwcattributes:abcdEquivalence>accessible from DataSets/DataSet/Units/Unit/Gathering/ISODateTimeBegin and DataSets/DataSet/Units/Unit/Gathering/ISODateTimeEnd</dwcattributes:abcdEquivalence>
<dwcattributes:organizedInClass rdf:resource="http://rs.tdwg.org/dwc/terms/Event"/>
</rdf:Description>
```

provides most of the same information as the non-normative human-readable definition at http://rs.tdwg.org/dwc/terms/#eventTime.  However since the normative version is in RDF, it can be provided to a machine client (i.e. computer) that tries to dereference the URI for the term.  The information provided in the defining RDF is relatively simple and and contains mostly literal properties, so the machine client would not be able to do much reasoning on the information in its present form.

## 2.6. What is the TDWG RDF/OWL Task Group trying to do? ##
The [RDF/OWL Task Group (TG)](http://code.google.com/p/tdwg-rdf/) is attempting to determine what RDF and OWL can reasonably be expected to do in the biodiversity informatics context and to recommend approaches that can be used to achieve these expectations.  We seek to use the experience of other communities and to follow an experimental approach to find out what will and will not work on a practical level.  In particular, we hope to leverage existing infrastructure (i.e. existing TDWG vocabularies and existing delivery systems such as HTTP) to accomplish this in a reasonable amount of time.  For further information, see the [TG charter](CharterOfTG.md).

# References #
### 1 RDF Motivation and Goals ###
http://www.w3.org/TR/rdf-concepts/#section-Overview

### 2 Tim Berners-Lee on the Semantic Web ###
Berners-Lee, Tim and Mark Fischetti. 1999. Weaving the Web: the original design and ultimate destiny of the World Wide Web by its inventor.  San Francisco, Harper.  `isbn:9780062515872`

### 3 Resource Description Framework (RDF) Model and Syntax Specification ###
http://www.w3.org/TR/1999/REC-rdf-syntax-19990222/
superseded by
http://www.w3.org/TR/rdf-syntax-grammar/

### 4 W3C Recommendations ###
are the final product of a technical report development process described at
http://www.w3.org/2005/10/Process-20051014/tr.html#Reports

### 5 Classes and types are described in the RDF Schema (RDFS) ###
http://www.w3.org/TR/rdf-schema/

### 6 Linked Open Data Project ###
http://linkeddata.org/

### 7 Frequently asked questions about LOD ###
http://linkeddata.org/faq

### 8 Linked Data vs. the Semantic Web ###
http://tomheath.com/blog/2009/03/linked-data-web-of-data-semantic-web-wtf/

http://blogs.nature.com/jhendler/2009/06/16/what-is-the-semantic-web-really-all-about

### 9 TDWG home page ###
http://www.tdwg.org/

### 10 About TDWG ###
http://www.tdwg.org/about-tdwg/

### 11 TDWG Standards ###
http://www.tdwg.org/standards/

### 12 TDWG TAG 2006 roadmap ###
http://www.tdwg.org/uploads/media/TAG_Roadmap_01.doc

### 13 LSID Best Practices ###
http://www.ibm.com/developerworks/opensource/library/os-lsidbp/
See also http://www.omg.org/cgi-bin/doc?dtc/04-05-01 and http://xml.coverpages.org/lsid.html

### 14 TDWG Ontology Google Code repository ###
http://code.google.com/p/tdwg-ontology/source/browse/ specifically http://code.google.com/p/tdwg-ontology/source/browse/#svn%2Ftrunk%2Fontology

### 15 GUID and Life Sciences Identifiers Applicability Statements ###
http://www.tdwg.org/standards/150/

Directly viewable in a browser at: http://bioimages.vanderbilt.edu/pages/guid-applicability-final-2011-01.pdf and http://bioimages.vanderbilt.edu/pages/LSID%20AS_2011_01_final.pdf

### 16 DCMI Abstract Model ###
http://dublincore.org/documents/abstract-model/

The DCMI Abstract Model is discussed in greater detail in [section 4.3.](Beginners4Vocabularies#4.3._The_DCMI_Abstract_Model_(DCAM).md) of this guide.

### 17 The TDWG Standards Documentation Specification ###
http://www.tdwg.org/standards/147/
is an unratified standard which prescribes how TDWG standards should be described.  In that specification, a normative (Type 1) document which forms part of a standard is tightly controlled and defines the standard.  A non-normative (Type 2) document is also tightly controlled but explains and justifies the standard rather than defining it.  Other documents (Type 3) may provide additional information to support the standard without actually forming a part of it.

### 18 Darwin Core expressed in RDF/XML ###
Normative at http://rs.tdwg.org/dwc/rdf/dwctermshistory.rdf.  Directly browsable at http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwctermshistory.rdf but not normative.


---

Questions? Comments? Contact [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide)


.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.