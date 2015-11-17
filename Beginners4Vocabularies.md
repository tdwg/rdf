# Beginner's guide to RDF: 4. Vocabularies, DCAM, and RDFS #

[go to part 3: RDF basics](Beginners3RDFbasics.md)

[go to part 5: Discovery, Transmission, and Storage of RDF data](Beginners5RDFdata.md)

[Introduction to the Guide](Beginners.md)

**Contents**



## 4.1. What is a vocabulary? ##

A vocabulary is a list of terms and their definitions. [(1)](#1__Definition_of_a_vocabulary.md)    In this context, "vocabulary" refers specifically to a controlled vocabulary in the sense that terms are included in the list by the declaration of some sponsoring body.  Within a vocabulary, the best practice is to have only one term for a single thing and to have only a single definition for each term.  Terms are often identified by a URI created from a text string which is generally understandable by humans to be related to the concept that is embodied in the term.

Although different terms may be named by URIs that use the same string after a prefix, e.g. `ac:derivedFrom` and `dsw:derivedFrom`, they do not necessarily mean the same thing.  The term text strings are _qualified_ by prefixing them in such a way that they form a URI which unambiguously relates them to their defining vocabulary.  What each term means is defined in the vocabulary from which they came, and the data in the RDF cannot be interpreted without reference to that definition.

For example, the string "derivedFrom" can represent "a reference to an original resource from which the current one is derived" (the sense in which it is used in the draft Audubon Core standard [(2)](#2_Term_list_for_Audubon_Core_draft_TDWG_standard.md) ).   However, "derivedFrom" can also be a term representing the organism or Token from which another Token is derived (the sense in which it is used in darwin-sw [(3)](#3_Description_of_the_Token_class_of_Darwin-sw.md) ).  To differentiate between different definitions of terms, a _namespace_ abbreviation is placed in front of the term to make it unique.  In this example, `ac:` can abbreviate "`http://rs.tdwg.org/ac/terms/`" and `dsw:` can abbreviate "`http://purl.org/dsw/`".  So when one writes `ac:derivedFrom` it is an abbreviation for the URI `http://rs.tdwg.org/ac/terms/derivedFrom` while `dsw:derivedFrom` is an abbreviation for the URI `http://purl.org/dsw/derivedFrom` .  In this convention, the namespace provides a way to identify the defining vocabulary while the entire URI provides a globally unique identifier for the term. Often a variety of the namespace itself serves as an identifier for the entire vocabulary, known as the vocabulary URI.

Commonly vocabulary namespaces are either a "hash namespace" or a "slash namespace".  URIs for terms in vocabularies that use hash namespaces are constructed by appending a "#" character to the end of the vocabulary URI, then appending the term string. For example, the SKOS core vocabulary has the URI `http://www.w3.org/2004/02/skos/core`.  The URI for the term `skos:closeMatch` is formed by concatenating the vocabulary URI, "#", and the term name "closeMatch": `http://www.w3.org/2004/02/skos/core#closeMatch`.  URIs for terms in vocabularies that use hash namespaces are constructed by appending the term name to the end of the vocabulary URI.  For example, the Dublin Core "terms" vocabulary has the vocabulary URI `http://purl.org/dc/terms/`.  The URI for the term `dcterms:subject` is formed by concatenating the vocabulary URI and the term name "subject": `http://purl.org/dc/terms/subject`.  The choice of whether to use a hash or slash namespace depends on several factors, including the size of the vocabulary and the method by which the RDF describing the vocabulary will be served.  This is described in detail in Appendix B of [Best Practice Recipes for Publishing RDF Vocabularies](http://www.w3.org/TR/swbp-vocab-pub/#naming).

Even though a vocabulary may use a URI to identify its terms, it should not be presumed that attempting to dereference the URI using a web browser or semantic client will necessarily return any useful information.  If a URI does dereference, the information returned can range from a minimal human-readable text description of the term to a complex RDF description of the properties of that term and how it is related to other terms.

## 4.2. What is an ontology? ##
Although there is no strict definition of an ontology, it is generally recognized that an ontology describes the formal constraints of the terms in a vocabulary and expresses relationships among terms in the vocabulary using some kind of ontology representation language.  An ontology can describe hierarchical relationships among terms (as in a taxonomy), describe associative relationships among terms (as in a thesaurus), and relate terms within the vocabulary to other terms described outside of the vocabulary.  Basic RDF makes few distinctions in the ways that URIs can be used to represent predicates and objects.  But other systems have been developed to extend basic RDF and provide ways to indicate more clearly the nature of resources and the relationships between them.  RDFS ([section 4.4.](#4.4._RDF_Schema_and_the_relationship_of_the_DCMI_Abstract_Model.md)) and OWL ([section 7.4.](Beginners7OWL#7.4._What_is_Web_Ontology_Language_(OWL)?.md)) provide increasingly complex means of describing such relationships.

There are tradeoffs involved in choosing to describe terms using an ontology rather than a simpler controlled vocabulary.  Terms that are described as part of an ontology carry much more meaning and can be used to do more sophisticated machine reasoning (i.e. to "generate" new triples from existing ones).  On the other hand, terms that are described by an ontology are far more encumbered and may have a much more restricted utility than terms that are described in a simple controlled vocabulary.

For example, Audubon Core is very vague about the types of resources that can be the subjects and objects of `ac:derivedFrom`.  Because Audubon Core is concerned with media items, one might assume that it is intended to describe how one media item (e.g. an image) is related to another.  For instance a particular StillImage might be `ac:derivedFrom` some particular MovingImage . However, there is nothing in the formal description of `ac:derivedFrom` that would prohibit someone from making the statement that an offspring is `ac:derivedFrom` its mother.  Thus a simple description of a term allows it to be adapted to uses that were not conceived by the original creators of the term.

In contrast, the darwin-sw ontology defines `dsw:derivedFrom` to be a transitive property (i.e. if `A dsw:derivedFrom B` and `B  dsw:derivedFrom C`, then `A dsw:derivedFrom C`) and is also defined to have the inverse property `dsw:hasDerivative` (i.e. if `A dsw:derivedFrom B`, then `B dsw:hasDerivative A`).  So persons who are not careful in using `dsw:derivedFrom` may end up saying things that they do not intend.  The problem of making unintended statements is particularly acute when an ontology declares terms to have range and domain properties (see sections [4.3.2.5.](#4.3.2.5._has_domain.md) and [4.3.2.6.](#4.3.2.6._has_range.md)).

Ontologies and a language to describe them (OWL) are described in more detail in [section 7.](Beginners7OWL.md) of this guide.

## 4.3. The DCMI Abstract Model (DCAM) ##

### 4.3.1. What is the DCMI Abstract Model? ###
In 2007, the Dublin Core Metadata Initiative (DCMI) [(4)](#4_Dublin_Core_Metadata_Initiative.md) produced a Recommendation describing an abstract model for Dublin Core (DC) metadata. [(5)](#5_DCMI_Abstract_Model.md)  Because DC is a widely recognized and used vocabulary, the DCMI Abstract Model (DCAM) has been used as a model for other vocabularies outside DCMI, with [Darwin Core as a notable example](http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#abstractmodel) within our community.  The proposed [Audubon Core TDWG standard is also modeled after the DCMI Abstract Model](http://species-id.net/wiki/Audubon_Core).  As an abstract model, the DCMI Abstract Model is independent of any particular coding scheme.  Thus it can be used as a model for vocabularies such as Audubon Core, whose normative definition is in human-readable terms and assumes no particular serialization.  Nevertheless, the DCAM was built upon concepts defined in the World Wide Web Consortium's (W3C's) [Resource Description Framework (RDF)](Beginners2WhatIsRDF#2.1._What_is_RDF?.md).  So even vocabularies which are based on the DCAM but which are not expressed in RDF are structured in a way analogous to the structure of RDF.

### 4.3.2. Main features of the DCMI Abstract Model ###

#### 4.3.2.1. Use of URIs and literals ####
Resources that are described using the DCAM are identified by URIs or are expressed as string literals.  The nature of literals can be clarified by applying an ISO language tag or by indicating the structure of the string by associating it with a syntax encoding scheme (e.g. it is an integer or formatted date).  See [this](DublinCore#1.3.1._Dublin_Core_terms_which_have_range_rdfs:Literal.md) for details of DCAM literal value surrogates.

#### 4.3.2.2. Resource description set ####
A subject resource is described by a set of statements.  Each statement is made up of a _property-value_ pair.

#### 4.3.2.3. Property-value pair ####
In a statement about a subject resource which consists of a property-value pair, the property (also known as an _element_) is a term from the vocabulary (e.g. the DC vocabulary) which relates the subject resource to the value.  The value of the statement can be represented by either a URI or a literal.  For example a book (the subject) could be described by the property `dcterms:title` and the literal value "`A Tale of Two Cities`".  Optionally, the literal could have the tag `xml:lang="en"` or `xml:lang="es"` for property-value pair `dcterms:title`  "`Historia De Dos Ciudades`".

The _value surrogate_ (which represents the value resource) could also be a URI as in the property-value pair:
```
dcterms:type   http://purl.org/dc/dcmitype/Text
```
where `http://purl.org/dc/dcmitype/Text` is a URI which identifies the type of things that consist primarily of words for reading.

#### 4.3.2.4. Class ####
The DCAM defines a special type of vocabulary term called a _class_.  A class is a mechanism defining a group of resources of a particular type.  A resource which is a member of a particular class of resources is called an _instance_ of that class.

Note: a common convention is to capitalize the names of classes and to write the names of properties in `camelCase`.  However, this convention is one of convenience and it is not safe to make assumptions about the nature of a term based on its capitalization.

#### 4.3.2.5. has domain ####
Terms in a vocabulary which are properties that can describe all instances of a particular class are said to have a _domain_ relationship with that class.  For example, the property term `dcterms:medium` has a domain which is the class `dcterms:PhysicalResource`.  So the property `dcterms:medium` will apply to all `dcterms:PhysicalResource` instances.

Many DC terms which are properties do not have domain assignments. Thus, although a resource which is an instance of the class `dcterms:BibliographicResource` may have the property `dcterms:publisher`, there is nothing which says that a thing which has the property `dcterms:publisher` must be an instance of the `dcterms:BibliographicResource` class.  However, any thing which has the property `dcterms:medium` can be inferred to be an instance of the class `dcterms:PhysicalResource` because of the domain assignment in the definition of `dcterms:medium`.

#### 4.3.2.6. has range ####
In some cases, it may be assumed that all values associated with a particular property would be instances of a particular class.  This is called a _range_ relationship between the property and the class.  For example, if a subject resource has a creator, it can be inferred that the creator is some kind of agent which is capable of creating.  Therefore, the definition of the property `dcterms:creator` states that it has the range `dcterms:Agent`.  So if one makes a statement about the painting Starry Night that
```
dcterms:creator  people:Vincent_van_Gogh
```
one can infer that `people:Vincent_van_Gogh` is a `dcterms:Agent`

As was the case with domain, there is no requirement that any property term have a range assignment.

#### 4.3.2.7. Sub-classes and sub-properties ####
The DCMI Abstract Model allows a class to be related to another class by a _sub-class_ relationship.  One class is a sub-class of another class if all instances of the first class are also instances of the second class.  For example `dcterms:FileFormat` is defined to be a sub-class of `dcterms:MediaType`.  Therefore, anything which is a `dcterms:FileFormat` is also a `dcterms:MediaType`.  It is NOT true that anything which is a `dcterms:MediaType` will also be a `dcterms:FileFormat`.

The DCAM also allows a property to be related to another property by a _sub-property_ relationship.  A property is a sub-property of another property if all instances of the first property also have the same relationship as the second property.  For example `dcterms:creator` is a sub-property of `dcterms:contributor`.  So if the painting Starry Night is described by the property value pair:
```
dcterms:creator  people:Vincent_van_Gogh
```
then it can also be known that the property value pair:
```
dcterms:contributor  people:Vincent_van_Gogh
```
also applies to Starry Night even if it is not stated explicitly.

### 4.3.3. Implications of using the DCMI Abstract Model as the basis for a vocabulary ###
If the DCAM is used as the basis for a vocabulary, one can assume:
  * that the purpose of the vocabulary is to describe resources using sets of property-value pairs.
  * that a described (subject) resource may be identified by a URI, although this is not required.
  * that resources which are values may be described using URI references or literals.
  * that the properties will be identified by qualified URIs.

Although the DCAM assumes the existence of classes, it does NOT require that a vocabulary following its model define any classes.  If the vocabulary defines classes the DCAM allows but does NOT require that those classes be associated with any property terms through domain or range assignments.

Although the DCAM was designed to be compatible with RDF, it is a generic information model and does not assume any particular encoding syntax.

## 4.4. RDF Schema and the relationship of the DCMI Abstract Model to RDF ##

### 4.4.1. RDFS ###
RDF was developed as a general purpose model for representing information on the Web.  After the introduction of RDF, the W3C published a Recommendation known as the RDF Schema (RDFS) for specifying how RDF could be used to describe vocabularies.  [(6)](#6_RDF_Vocabulary_Description_Language_1.0:_RDF_Schema.md)  RDFS extends the basic RDF syntax by defining additional terms which facilitate the categorization of resources into classes, and which describe how properties are related to those classes.  Because the DCMI Abstract Model was developed based on the concepts defined in RDF and RDFS, there is a direct relationship between the concepts discussed in section [4.3.](#4.3._The_DCMI_Abstract_Model_(DCAM).md) and those which are described formally in RDFS.  In fact, although the DCAM does not assume any particular encoding syntax for vocabularies which follow it, the model itself is formally defined based on RDF and RDFS.

### 4.4.2. Correspondence between the structure of the DCAM and RDF/RDFS ###

A described resource of the DCAM corresponds to the subject of an RDF triple.  The property-value pair of the DCAM corresponds to the predicate and object of an RDF triple.  The DCAM states that the description of a resource is made up of one or more instances of property-value pairs which describe that single resource.  RDF does not demand that resources be described in sets of triples related to a single resource.  Rather, RDF triples stand as independent statements of fact which do not have to be grouped in any particular way.  However, as a practical matter when RDF is serialized using XML or N3, the triples which describe a single resource are grouped together.  For example the following DCAM description:
```
Described resource: http://bioimages.vanderbilt.edu/kirchoff/ac1490
Property-value pairs:
dcterms:title "Quercus michauxii (Fagaceae) - leaf"
dcterms:created "2010-09-01T03:41:31"
dcterms:dateCopyrighted "2011"
```
can be expressed in RDF/XML as:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/ac1490">
  <dcterms:title>Quercus michauxii (Fagaceae) - leaf</dcterms:title> 
  <dcterms:created>2010-09-01T03:41:31</dcterms:created>
  <dcterms:dateCopyrighted>2011</dcterms:dateCopyrighted>
</rdf:Description>
```
or in N3 as
```
<http://bioimages.vanderbilt.edu/kirchoff/ac1490> 
        dcterms:title "Quercus michauxii (Fagaceae) - leaf"
        dcterms:created "2010-09-01T03:41:31";
        dcterms:dateCopyrighted "2011".
```

In both of these RDF serializations, the predicates and objects which describe the subject are presented in a list of pairs which are analogous to property-value pairs as described in the DCAM.

### 4.4.3. Correspondence between the terminology of the DCAM and RDF/RDFS ###
Because of the basis of the DCMI Abstract Model on the ideas embodied in RDF and RDFS, there are equivalencies between the abstract terminology used in the DCMI Abstract Model and the formally defined terms of RDF and RDFS.  The following table summarizes these equivalencies [(7)](#7_Comparison_of_DCMI_Abstract_Model_with_RDF/RDFS.md):

| DCAM |RDF/RDFS|
|:-----|:-------|
|resource|rdfs:Resource|
|property or element|rdf:Property|
|class |rdfs:Class|
|syntax encoding scheme|rdfs:Datatype|
|has domain|rdfs:domain|
|has range|rdfs:range|
|sub-property of|rdfs:subPropertyOf|
|sub-class of|rdfs:subClassOf|

### 4.4.4. Using `rdf:type` and ways to determine instances of classes ###

#### 4.4.4.1. Declaring an instance of a class using `rdf:type` ####
The DCAM model presents the concept that a vocabulary term can be a class.  However, it does not provide a direct means of declaring that a resource is an instance of a class.  This can be done explicitly in RDF using the predicate `rdf:type`.  If a triple states that the subject resource has `rdf:type` C, then C is inferred to be an `rdfs:Class` and the triple states that the subject resource is an instance of that class. [(8)](#8_Description_of_rdf:type.md)

#### 4.4.4.2. Inferring an instance of a class based on `rdfs:range` and `rdfs:domain` properties of a RDF predicate ####
Because the RDFS terms `rdfs:range` and `rdfs:domain` correspond directly to the has range and has domain relationships described in the DCAM, the explanation provided in sections [4.3.2.5.](#4.3.2.5._has_domain.md) and [4.3.2.6.](#4.3.2.6._has_range.md) apply to RDFS as well. [(9)](#9_Definitions_of_rdfs:range_and_rdfs:domain.md)  In the following example,
```
foaf: = "http://xmlns.com/foaf/0.1/" and 
kimage: = "http://bioimages.vanderbilt.edu/kirchoff/
```
The definition of the term `foaf:depicts` in RDF [(10)](#10__Definition_of_the_FOAF_vocabulary_in_RDF.md) contains the following triple:
```
foaf:depicts   rdfs:domain  foaf:Image
```
which says that a subject of the property `foaf:depicts` is an `foaf:Image`.   If we make the statement:
```
kimage:ac1490  foaf:depicts   http://bioimages.vanderbilt.edu/uncg/14
```
then the following triple can be inferred even if it is not explicitly stated in any RDF describing `kimage:ac1490` since `kimage:ac1490` is the subject of a triple having `foaf:depicts` as its predicate.
```
kimage:ac1490  rdf:type   foaf:Image
```
Thus applying the property `foaf:depicts` to a resource implicitly asserts that the resource is an instance of the class `foaf:Image`.

Similarly, if a property term T is defined to have range C, then if resource O is the object of a triple containing the T as the predicate, it is implied that `O rdf:type C` and therefore O is an instance of class C.

The following example illustrates the danger of using a property term having an assigned domain as the predicate of a statement about a resource of a type not intended to be described by that term.  If I would like to describe the nature of novels using terms I have created in a vocabulary defined under the namespace `myNmspc:` I might make the statement
```
http://dbpedia.org/resource/The_Lord_of_the_Rings   foaf:depicts   myNmspc:goodVsEvil
```
However, making this statement asserts that my descriptive term for novels `myNmspc:goodVsEvil` is an instance of the class `foaf:Image` which doesn't make very much sense.

#### 4.4.4.3. Implying an instance of a class using the class name as the name of a container element in XML serialization of RDF ####
When the name of a class is used as the name of the XML container element for the description of a resource (instead of the generic `rdf:Description` element), a `rdf:type` statement is implied which indicates that the resource is an instance of that class.  See section [3.3.3.](Beginners3RDFbasics#3.3.3._XML_representation.md) for an example.

#### 4.4.4.4. Inferring an instance of a class based on a `rdfs:subClassOf` declaration ####
The definition of the class `foaf:Image` in RDF [(10)](#10__Definition_of_the_FOAF_vocabulary_in_RDF.md) makes the statement
```
foaf:Image  rdfs:subClassOf   foaf:Document
```
Thus if one declares that
```
kimage:ac1481  rdf:type  foaf:Image
```
it can also be inferred that
```
kimage:ac1481  rdf:type  foaf:Document
```
Note that nothing prohibits a particular resource from being an instance of several classes.
Also note that in section [4.4.4.2.](#4.4.4.2._Inferring_an_instance_of_a_class_based_on_rdfs:range_an.md) it was shown that the triple
```
kimage:ac1490  foaf:depicts   http://bioimages.vanderbilt.edu/uncg/14
```
implies that `kimage:ac1490` is an instance of the `foaf:Image` class.  Given the `rdfs:subClassOf` statement in the definition of `foaf:Image`, the triple also implies that `kimage:ac1490` is also an instance of the `foaf:Document` class.

#### 4.4.4.5. The hazards of `rdfs:subClassOf`, `rdfs:range`, and `rdfs:domain` ####
The examples given above show that careless application of the `rdfs:subClassOf`, `rdfs:range`, and `rdfs:domain` properties in the definitions of terms or the careless use of terms having such properties can result in unintended consequences if users are not aware of the implications of their actions.  For this reason, the three properties listed above (as well as `rdfs:subPropertyOf`) are generally used sparingly in term definitions of general purpose vocabularies.

## 4.5. The Darwin Core vocabulary as an implementation of the DCMI Abstract Model ##
The Darwin Core vocabulary [(11)](#11__Darwin_Core.md) is a TDWG technical specification standard.  [(12)](#12_Categories_of_TDWG_standards.md)  It follows the DCMI Abstract Model [(13)](#13_Darwin_Core_abstract_model.md).  In accordance with the DCAM, Darwin Core has terms that are classes or properties.  Those properties could have domains which are Darwin Core class terms (although they don't have any that are explicitly declared in the term definitions).  The properties are associated with values to form property-value pairs that describe the subject.

However, this particular version of the abstract model is described in the context of the guidelines for implementing application schemas as XML, so some of the statements made in those guidelines are more restrictive than the general DCAM.  In particular, they restrict a property to describe at most one class.  This is to promote consistency in implementation of the containment system that is described in the guide.  The XML guide also restricts values to be literal strings contained within property elements as opposed to allowing values to be specified as XML attributes.  So although the model described is considered an abstract model, it is focused on describing "flat" records ("Simple Darwin Core").  The guidelines specifically state that they apply in situations where RDF/XML are not appropriate and that they are NOT guidelines for the implementation of RDF/XML. [(14)](#14_Introduction_to_the_Darwin_Core_XML_Guide.md)  So the restrictive modifications of the DCAM described in the Darwin Core abstract model should not be considered to apply to any RDF implementation of Darwin Core.

## 4.6. The Darwin Core vocabulary normative definition as RDF ##

### 4.6.1. Informational properties ###
Although there is no existing implementation guide or statement of best practices indicating how Darwin Core should be implemented as RDF, the standard itself is described using RDF in the normative document for Darwin Core [(15)](#15__Darwin_Core_terms_described_in_RDF/XML.md).  Much of the information about the Darwin Core terms which are defined in this document is in the form of literal strings intended for human consumption, namely `rdfs:label`, `rdfs:comment`, and `dcterms:description`.  These properties can be viewed at the human-readable Quick Reference Guide. [(16)](#16_Darwin_Core_Quick_Reference_Guide.md)  Each term has the property `rdfs:isDefinedBy` which has the value of the URI of the vocabulary ( `http://rs.tdwg.org/dwc/terms/`). Several additional well-known informational properties are given for each term: `dcterms:issued` and `dcterms:modified` which are untyped strings but are in ISO 8601 format, `rdf:type` which is either `rdfs:Property` or `rdfs:Class`, `dcterms:hasVersion` which references a permanent record in the term history [(17)](#17_Darwin_Core_term_history.md), and  `dcterms:replaces` which references dated terms in the term namespace which are not explicitly described there as subject resources.  The properties also include three terms that are described in the Darwin Core attributes vocabulary [(18)](#18_Darwin_Core_attributes_vocabulary.md): `dwcattributes:abcdEquivalence`, `dwcattributes:status` (with values of `recommended` or `deprecated`), and `dwcattributes:organizedInClass`.  The first of these three terms maps Darwin Core terms to similar terms in the Access to Biological Collections Data (ABCD) schema.[(19)](#19_The_Access_to_Biological_Collections_Data_(ABCD)_schema.md)  The second suggests to humans whether the term is still recommended for use.  The last term suggests to humans the class which a property term might describe; Darwin core terms have no formal `rdfs:domain properties` (and no `rdfs:range` properties as well).

### 4.6.2. `rdfs:subProperty` relationships to other properties ###
Of the possible DCAM/RDFS relationships which allow a machine to infer additional facts from a property statement (i.e. range, domain, subclass, and subproperty), only `rdfs:subProperty` is used in the Darwin Core term definitions.  There are several types of `rdfs:subProperty` declarations:
  * ID properties which describe identifiers (e.g. `dwc:acceptedNameUsageID` and `dwc:datasetID`) which are declared to be `rdfs:subProperty` of `dcterms:identifier`.
  * properties involving dates (e.g. `dwc:eventDate` and `dwc:georeferencedDate`) which are declared to be `rdfs:subProperty` of `dcterms:date`.
  * `dwc:namePublishedIn` which is declared an `rdfs:subProperty` of `dcterms:bibliographicCitation`
  * "By" terms (`dwc:georeferencedBy`,`dwc:identifiedBy`, `dwc:locationAccordingTo`, `dwc:measurementDeterminedBy`, `dwc:nameAccordingTo`, `dwc:recordedBy`, `dwc:relationshipAccordingTo`) which are declared to be `rdfs:subProperty` of `dwc:accordingTo`, a Darwin Core-defined property which is an "Abstract term to attribute information to a source."
  * `dwc:collectionCode` which is declared an `rdfs:subProperty` of `http://rs.tdwg.org/ncd/terms/Collection#Code`
  * `dwc:collectionID` which is declared an `rdfs:subProperty` of `http://rs.tdwg.org/ncd/terms/Collection#Id`
  * `dwc:institutionCode` which is declared an `rdfs:subProperty` of `http://rs.tdwg.org/ncd/terms/Institution#Code`
  * `dwc:institutionID` which is declared an `rdfs:subProperty` of `http://rs.tdwg.org/ncd/terms/Institution#Id`
  * `dwc:ownerInstitutionCode` which is declared an `rdfs:subProperty` of `http://rs.tdwg.org/ncd/terms/Institution#Code`
  * `dwc:ResourceRelationship` (a Darwin Core class) which is declared an `rdfs:subProperty` of `dcterms:relation` [(20)](#20__dwc:_ResourceRelationship_is_both_a_class_and_a_property.md)

Note: the URIs having namespace `http://rs.tdwg.org/ncd/terms/Institution#` seem to be incorrect as the namespace for the Natural Collection Description vocabulary is defined as `http://rs.tdwg.org/ontology/voc/Collection#` in the draft standard. [(21)](#21_Natural_Collections_Descriptions_(NCD)_draft_TDWG_standard.md)

### 4.6.3. Darwin Core terms not defined by Darwin Core ###
There are a number of terms included in the Darwin Core standard which are not defined by Darwin Core itself.   Most of these terms are record-level property terms that are defined by Dublin Core [(22)](#22_DCMI_Metadata_Terms.md), e.g. `dcterms:type`, `dcterms:modified`, etc.  The exception is `dcterms:Location` which serves as one of the classes under which Darwin Core terms are organized.

A significant aspect of these terms is that unlike the terms defined in the Darwin Core namespace, the Dublin core terms may have domains and ranges specified in their definitions.  This is significant in the case of `dcterms:type` which will be discussed in section [4.7.3.1.](#4.7.3.1._Why_the_DCMI_and_Darwin_Core_type_vocabularies_are_defi.md)  See also [a discussion of problems involving Darwin Core guidelines for using Dublin Core terms](DublinCore#2._Implications_of_Dublin_Core_RDF_Guidelines_for_the_TDWG_vocab.md).

## 4.7. _Hic sunt dracones_: Using classes and types ##

### 4.7.1. How does one indicate that a resource is a class? ###

There are two ways to assert that a resource is a class

#### 4.7.1.1. Define a term to be a class directly by declaring its `rdf:type` to be `rdfs:Class` ####
As described in section [4.4.4.1.](#4.4.4.1._Declaring_an_instance_of_a_class_using_rdf:type.md), one can express that a term represents a class if it is declared explicitly to be a class in its description.  For example, in the definition of `dcterms:Agent` the following RDF triple is used to declare it to be a class:
```
http://purl.org/dc/terms/Agent   rdf:type   http://www.w3.org/2000/01/rdf-schema#Class
```
If a term is declared to be an `owl:Class`, then it is also implicitly declared to be an `rdfs:Class` because `owl:Class  rdfs:subClassOf  rdfs:Class`.  See [section 7.6.2.](Beginners7OWL#7.6.2._owl:Class_and_individuals.md) of this guide for more on `owl:Class`.

#### 4.7.1.2. Assert that a term is a class by using it as the object of an `rdf:type` triple ####
The RDFS schema defines the relationship between `rdf:type` and `rdfs:Class`.[(23)](#23_Definition_of_rdfs:type.md)  The schema says that `rdf:type` is used to state that a resource is an instance of an `rdfs:Class`.  Significantly, the range of `rdf:type` is defined to be `rdfs:Class`.  Therefore, when one uses `rdf:type` to declare that a resource is an instance of a particular class, one is also asserting that the object of the triple IS an `rdfs:Class` even if the term which is the object isn't already explicitly defined to be one.  (So the in the previous example, the triple not only asserts that `dcterms:Agent` is an instance of `rdfs:Class`, it is also asserting indirectly that `rdfs:Class` is an instance of `rdfs:Class` !)

For example, if one asserts that
```
http://bioimages.vanderbilt.edu/kirchoff/ac1490  rdf:type   http://purl.org/dc/dcmitype/StillImage
```
or in abbreviated form
```
kimage:ac1490  rdf:type  dctype:StillImage
```
not only does it assert that `kimage:ac1490` is an instance of `dctype:StillImage`, but it also declares `dctype:StillImage` to be an `rdfs:Class`.  As it turns out, `dctype:StillImage` is already declared to be an `rdfs:Class` in its term definition [(24)](#24_Definition_of_dcterms:_StillImage.md), but if it hadn't already been a class, one would be asserting that it was one by using it as the object of the type declaration.

### 4.7.2. Where can we find classes to use in `rdf:type` statements? ###
The RDFS schema is silent about what constitutes appropriate classes or types in a particular situation.  Users are free to use any pre-existing types/classes or to define their own.

However, since the purpose of having classes seems to be to allow different users to know that they are both talking about the same kind of resource, it is a best practice to use well-known types rather than making up ad hoc types.[(25)](#25_Typing_using_well-known_vocabularies.md)  The wiki page [ClassInventory](ClassInventory.md) lists classes defined in some well-known vocabularies and ontologies.

### 4.7.3. Type vocabularies ###
Both Dublin Core [(26)](#26_DCMI_Type_Vocabulary.md) and Darwin Core [(27)](#27_Darwin_Core_Type_Vocabulary.md) define type vocabularies.  In the RDF which defines both of these vocabularies, each of the listed types is declared to be an `rdfs:Class`.  So as a practical matter, from the standpoint of RDF these terms are no different than the classes defined within the regular Dublin Core and Darwin Core term vocabularies.  The classes in the type vocabularies are also listed on the page [ClassInventory](ClassInventory#2._Type_vocabularies.md).


#### 4.7.3.1. Why the DCMI and Darwin Core type vocabularies are defined separately from other terms ####

These type vocabulary terms are defined separately from the classes defined in the general terms vocabularies because these terms are intended to be used as controlled values for other property terms in the respective vocabularies.  The DCMI Type Vocabulary provides a list of approved terms that may be used as controlled values for the `dcterms:type` property, while the Darwin Core Type Vocabulary "extends the DCMI Type Vocabulary and provides a list of approved values that may be used for the `dwc:basisOfRecord` term to identify the specific type of a resource." [(27)](#27_Darwin_Core_Type_Vocabulary.md)  In the case of a Simple Darwin Core [(28)](#28_Simple_Darwin_Core.md) serialization, values are expressed as text literals.  `dcterms:type` and `dwc:basisOfRecord` can be used as field names in a text file with the literals from the type vocabularies given as values for that field in a record.  In Darwin Core XML [(29)](#29_Darwin_Core_XML_Guide.md), the type values are expressed as string literal content of `dcterms:type` and `dwc:basisOfRecord` elements.

In RDF, a type vocabulary term could be used as an object of `dcterms:type` and `dwc:basisOfRecord` properties.  For example:
```
http://bioimages.vanderbilt.edu/kirchoff/ac1490  dcterms:type  dctype:StillImage
http://bioimages.vanderbilt.edu/specimen/ncu592805 dwc:basisOfRecord   dwctype:LivingSpecimen
```
However, as an `rdfs:Class` each of these type terms could also be used as the object of an `rdf:type` property as well.
```
http://bioimages.vanderbilt.edu/kirchoff/ac1490  rdf:type  dctype:StillImage
http://bioimages.vanderbilt.edu/specimen/ncu592805 rdf:type  dwctype:LivingSpecimen
```
The guidelines for expressing Dublin Core metadata as RDF [(30)](#30_Notes_on_semantics_of_Dublin_Core_as_RDF.md) state that "It is recommended that RDF applications implementing this specification primarily use and understand `rdf:type` in place of `dcterms:type` when expressing Dublin Core metadata in RDF, as most RDF processors come with built-in knowledge of `rdf:type`."  It also notes that `dcterms:type` has semantics that are similar to `rdf:type`, but that the precise relationship between those properties is undecided.  There is no similar guideline for use of `dwc:basisOfRecord` vs. `rdf:type`, but using the same rationale, it would seem preferable to use `rdf:type` when Darwin Core is expressed in RDF.

Interestingly, Darwin Core includes two classes borrowed from Dublin Core: `dcterms:Location` as a class defined in the Darwin Core Terms vocabulary and `dctype:Event` in the Darwin Core Type vocabulary.  However, Darwin Core also defines classes `dwctype:Location` and `dwc:Event`.  Nothing in the RDF ties these similarly-named classes together, so a machine would not consider a resource with `rdf:type dctype:Event` to be an instance of the same class as another resource with `rdf:type dwc:Event`; likewise resources typed as `dcterms:Location` and `dwctype:Location` would be considered instances of different classes.  In a serialization where the types were expressed as text literals rather than URIs, they would simple be "`Event`" and "`Location`" and not differentiable.

### 4.7.4.  Why does this matter??? ###
The creators of RDFS and the DCMI Abstract Model considered identification of the class of which a resource was an instance to be such a significant aspect of describing a resource that special structures and vocabulary were developed to declare or infer the type of a resource.  In order for effective querying of an RDF database, or to conduct reasoning based on RDF data, it is important to be able to know whether resources described by different people or organizations are actually the same kind of thing.  Thus it should be an important task of the community to reach a consensus about the precise URIs which should be used for typing, or if several URIs are acceptable, to define equivalency among terms from different vocabularies.

# References #

### 1  Definition of a vocabulary ###
For some descriptions of what a vocabulary is and how it is related to terms such as taxonomy, thesaurus, and ontology, see

http://infogrid.org/wiki/Reference/PidcockArticle

http://semwebtec.wordpress.com/2010/11/23/contolled-vocabulary-vs-ontology/

### 2 Term list for Audubon Core draft TDWG standard ###
http://species-id.net/wiki/Audubon_Core_Term_List#derivedFrom

### 3 Description of the Token class of Darwin-sw ###
http://code.google.com/p/darwin-sw/wiki/ClassToken

### 4 Dublin Core Metadata Initiative ###
http://dublincore.org/

There are important distinctions between the legacy terms in the `dc: = http://purl.org/dc/elements/1.1/` namespace and the terms in the `dcterms: = http://purl.org/dc/terms/` namespace.  See the sections "Addition of domains and ranges for existing properties and creation of new properties" and "Subproperty relations between terms in 'the Dublin Core' " at http://dublincore.org/usage/decisions/2008/dcterms-changes/#sect-2 as well as http://dublincore.org/documents/2008/01/14/domain-range/ for details.

### 5 DCMI Abstract Model ###
http://dublincore.org/documents/abstract-model/

### 6 RDF Vocabulary Description Language 1.0: RDF Schema ###
http://www.w3.org/TR/rdf-schema/

### 7 Comparison of DCMI Abstract Model with RDF/RDFS ###
The information in this table is taken from

http://dublincore.org/documents/abstract-model/#sect-5

using the following namespace abbreviations to simplify the table:

rdf: = `http://www.w3.org/1999/02/22-rdf-syntax-ns#`

rdfs: = `http://www.w3.org/2000/01/rdf-schema#`

### 8 Description of rdf:type ###
http://www.w3.org/TR/rdf-schema/#ch_type

### 9 Definitions of rdfs:range and rdfs:domain ###
http://www.w3.org/TR/rdf-schema/#ch_range

### 10  Definition of the FOAF vocabulary in RDF ###
http://xmlns.com/foaf/spec/index.rdf

### 11  Darwin Core ###
http://rs.tdwg.org/dwc/

### 12 Categories of TDWG standards ###
http://www.tdwg.org/standards/status-and-categories/

### 13 Darwin Core abstract model ###
http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#abstractmodel

### 14 Introduction to the Darwin Core XML Guide ###
http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#introduction

### 15  Darwin Core terms described in RDF/XML ###
can be downloaded from

http://rs.tdwg.org/dwc/rdf/dwcterms.rdf

using most web browsers.  However, it is not possible to **view** the file using most web browsers.

The file at http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwcterms.rdf (viewable in a browser) is similar but may be an outdated version.

The official normative document (i.e. Type 1 document sensu the draft TDWG documentation standard) for Darwin Core is http://rs.tdwg.org/dwc/rdf/dwctermshistory.rdf viewable at http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwctermshistory.rdf but as a practical matter, dereferencing term URIs leads to the dwcterms.rdf file since the terms in the dwctermshistory.rdf file have dates appended for versioning purposes.

### 16 Darwin Core Quick Reference Guide ###
http://rs.tdwg.org/dwc/terms/index.htm

### 17 Darwin Core term history ###
can be downloaded from

http://rs.tdwg.org/dwc/rdf/dwctermshistory.rdf

using most web browsers and which can be viewed in human-readable form at

http://darwincore.googlecode.com/svn/trunk/terms/history/index.htm

but which is not necessarily up to date.

### 18 Darwin Core attributes vocabulary ###
http://rs.tdwg.org/dwc/terms/attributes/

which is described by the document

http://rs.tdwg.org/dwc/terms/attributes/dwcattributes.rdf

### 19 The Access to Biological Collections Data (ABCD) schema ###
The ABCD schema is a TDWG Standard (http://www.tdwg.org/standards/115/) which can be used to describe collections, specimens, and observations in a highly structured fashion.  It is in the form of an XML schema and its terms are not identified by URIs nor defined in RDF, so they cannot be used as URI object references in RDF.

### 20  dwc:ResourceRelationship is both a class and a property ###
see http://code.google.com/p/darwincore/issues/detail?id=135

### 21 Natural Collections Descriptions (NCD) draft TDWG standard ###
Human readable http://www.tdwg.org/standards/312/

RDF at

http://rs.tdwg.org/ontology/voc/Collection

http://rs.tdwg.org/ontology/voc/Institution

http://rs.tdwg.org/ontology/voc/InstitutionType

http://rs.tdwg.org/ontology/voc/ContactDetails

Use view page source to view RDF; however, a note at that page says management of the vocabulary is now at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/

### 22 DCMI Metadata Terms ###
http://dublincore.org/documents/dcmi-terms/

### 23 Definition of rdfs:type ###
http://www.w3.org/TR/rdf-schema/#ch_type

### 24 Definition of dcterms:StillImage ###
http://dublincore.org/2010/10/11/dctype.rdf  in RDF

http://dublincore.org/documents/dcmi-type-vocabulary/ in human-readable form

### 25 Typing using well-known vocabularies ###
The TDWG GUID Applicability Standard
http://www.tdwg.org/standards/150/
states in Recommendation 11 that "Objects in the biodiversity domain that are identified by a GUID should be typed using the TDWG ontology or other well-known vocabularies in accordance with the TDWG common architecture."  Thus in our community, it is considered to be a best practice to use a well-known vocabulary.

### 26 DCMI Type Vocabulary ###
Human readable at http://dublincore.org/documents/dcmi-type-vocabulary/#H7

RDF at http://dublincore.org/2010/10/11/dctype.rdf

See the section "The Vocabulary Encoding Scheme 'DCMI Type Vocabulary' and its member terms" at http://dublincore.org/usage/decisions/2008/dcterms-changes/#sect-2 for a history of the evolution of the DCMI Type vocabulary

### 27 Darwin Core Type Vocabulary ###
Human readable at http://rs.tdwg.org/dwc/terms/type-vocabulary/index.htm

RDF at http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwctype.rdf

### 28 Simple Darwin Core ###
http://rs.tdwg.org/dwc/terms/simple/index.htm

### 29 Darwin Core XML Guide ###
http://rs.tdwg.org/dwc/terms/guides/xml/index.htm

### 30 Notes on semantics of Dublin Core as RDF ###
http://dublincore.org/documents/dc-rdf/#sect-5


---

Thanks to Paul Murray for helpful comments and suggestions on this page, including part of the definition of _term_.

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