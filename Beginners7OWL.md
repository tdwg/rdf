# Beginner's guide to RDF: 7. Ontologies and OWL #

[go to part 6. Querying with SPARQL](Beginners6SPARQL.md)

[Introduction to the Guide](Beginners.md)

**Contents**



## 7.1.  What is an ontology (again)? ##
In [section 4.2.](Beginners4Vocabularies#4.2._What_is_an_ontology?.md) it was noted that there is no strict definition of an ontology. However, in general an ontology describes the formal constraints of the terms in a vocabulary and expresses relationships among terms in the vocabulary using some kind of ontology representation language.  The transition from simple vocabulary to complex ontology is a continuum without a distinct boundary.  At one extreme are vocabularies such as Darwin Core where, although defined in RDF, properties have few or no expressed relationships to other properties or classes, and there are no defined relationships among the classes.  At the other extreme are complex ontologies which exhibit many of the features described in the following section.

## 7.2. Some features that may apply to ontologies ##

### 7.2.1.  Hierarchical relationships ###
Ontologies can express how one term is related hierarchically to another, e.g. a class is a subclass of another, a class is broader than another, object A is `partOf` object B, etc.

### 7.2.2. Characteristics of properties ###
Ontologies can define the characteristics of properties using terms that are well known to machines.  For example, a property can be the inverse of another, a property can be transitive, symmetric, or functional, etc.  _Annotation properties_ (e.g. `rdfs:label`) can be applied as properties to describe the characteristics of other properties.  [(1)](#1_Annotations_in_Web_Ontology_Language.md)

### 7.2.3. Properties with assumed types of values ###
Properties can be defined to have values that are identifiable objects, or defined to have values that are literals.

### 7.2.4. Ontologies can facilitate inferences ###
The relationships and restrictions expressed in an ontology can allow facts to be inferred that are not stated explicitly.  Those relationships and restrictions can also allow it to be determined that there are logical inconsistencies in data described using terms from the ontology.

## 7.3. Examples of ontologies ##
### 7.3.1. Friend of a Friend (FOAF) vocabulary ###
The FOAF vocabulary (`foaf: = http://xmlns.com/foaf/0.1/`) is a very simple ontology used to describe people and their relationships to information. [(2](#2_FOAF_Vocabulary_Specification.md))  Some terms in the vocabulary, such as `foaf:fundedBy` have a meaning that is understood through a human-readable text description, but whose definition implies nothing about either the subject or the object of the term.  It also has no relationships to other terms in the ontology.  Other terms have range, domain, subclass, and subproperty assignments as described in the DCMI abstract model and RDFS ([section 4.3](Beginners4Vocabularies#4.3._The_DCMI_Abstract_Model_(DCAM).md) and [section 4.4](Beginners4Vocabularies#4.4._RDF_Schema_and_the_relationship_of_the_DCMI_Abstract_Model.md)).  For example, because of its range declaration, using the term `foaf:publications` implies that the object of the statement is a `foaf:Document`.  Instances of the class `foaf:Person` are also instances of `foaf:Agent` because the `foaf:Person` class is a subclass of the `foaf:Agent` class.  There are also properties that are declared to be the inverse of other properties.  For example, `foaf:maker` and `foaf:made` are inverse properties.  So if A `foaf:made` B, then it can be inferred that B has `foaf:maker` A.  Because of these declarations of the characteristics of FOAF properties, it is possible to infer additional facts that are not explicitly expressed.

### 7.3.2. The Plant Ontology (PO) ###
The Plant Ontology is a controlled vocabulary (`po: = http://owlfiles.plantontology.org/PO_`) that describes plant morphology and developmental stages.  [(3)](#3_Plant_Ontology.md)  It is follows the principles of the The Open Biological and Biomedical Ontologies (OBO) Foundry.  [(4)](#4_The_Open_Biological_and_Biomedical_Ontologies.md)  The PO is currently used to describe patterns of gene expression and the phenotypes of genetic variants.

Relationships among terms in the PO are described by a set of Relationship Types which includes
```
is_a
part_of
develops_from
has_part
participates_in
adjacent_to
derives_from
```
For example, the term `po:0020043` which represents `compound leaf`, has the following relationships detailed at http://www.plantontology.org/amigo/go.cgi?view=details&query=PO:0020043
```
po:0020043 is_a po:0009025  (vascular leaf)
po:0020055 (leaf rachis) part_of po:0020043
po:0020049 (leaflet) part_of po:0020043
po:0020046 (palmate leaf) is_a po:0020043
po:0020045 (pinnate leaf) is_a po:0020043
```
Although the PO uses few properties to relate its terms, it has many terms.  So its complexity is due to size rather than complexity of relationships.

The PO is an abstract model without a particular serialization ([section 3.3](Beginners3RDFbasics#3.3._Serializations_of_RDF.md)), although it does have an OWL representation at http://owlfiles.plantontology.org/ .

### 7.3.3. TaxonConcept Ontology (txn) ###
This is a large and complex ontology that imports terms from other vocabularies and ontologies as well as coining new terms.  It is beyond the scope of this guide to describe the TaxonConcept ontology, but it can be explored at http://lod.taxonconcept.org/ontology/doc/index.html or by examining the raw RDF at http://lod.taxonconcept.org/ontology/txn.owl .

## 7.4. What is Web Ontology Language (OWL)? ##

Web Ontology Language (OWL) is a declarative language for expressing ontologies. [(5)](#5_OWL_2_Web_Ontology_Language_Primer.md)  This means that it is used to describe a state of affairs in a domain of interest in a logical way. [(6)](#6_What_is_OWL_2?.md)  It is a  knowledge representation language - it does not "do" anything in contrast to a computer language which can cause actions by providing instructions for the functioning of a computer.  However, applications called "reasoners" can infer information about the state of affairs by assessing statements made using the language of an OWL ontology.

An OWL ontology can be considered an abstract model about knowledge in some domain, and is sometimes expressed in other modeling languages such as UML [(7)](#7_OMG_Unified_Modeling_Language_(UML).md), a modeling language familiar to many programmers which shares with OWL notions of classes and relations between them.  However, OWL was designed so that ontologies could be expressed as RDF graphs, with a default exchange serialization of RDF/XML. [(8)](#8_OWL_2_Overview.md)  As an RDF serialization, OWL is a more expressive extension of RDF than of its precursor RDFS ([section 4.4](Beginners4Vocabularies#4.4._RDF_Schema_and_the_relationship_of_the_DCMI_Abstract_Model.md)) or generic RDF ([part 3](Beginners3RDFbasics#Beginner%27s_guide_to_RDF:_3._RDF_basics.md)).  However, this increased expressivity comes at the expense of increased complexity.

### 7.4.1. Varieties of OWL ###

Meanings can be assigned to ontologies through OWL in two ways: OWL DL and OWL Full.  [(9)](#9_OWL_2_DL_and_OWL_2_Full.md)  The details of the distinction between these two semantics is beyond the scope of this guide.  However, at the risk of oversimplification, one can say that OWL Full is less restrictive than OWL DL.  In OWL Full, the same URI can refer to both a class and an instance of a class or as both a class and a property.  This increased expressivity comes at a price because the restrictions imposed by OWL DL ensure that a reasoner can at least in principle always come up with "an answer" while OWL Full is by its nature undecidable.  So constraining an ontology to OWL DL makes life easier for implementers.

There is an additional version of OWL known as OWL Lite.  [(10)](#10_OWL_Lite_Feature_Synopsis.md)  It consists of a subset of the terms available in OWL DL and OWL Full.  It is less expressive but easier to implement and does provide useful terms that are not available in RDFS for describing relationships.

### 7.4.2. OWL language profiles ###
There are three profiles [(11)](#11_OWL_2_Web_Ontology_Language_Profiles.md) which restrict the expressiveness of OWL in order to achieve efficiency under different circumstances.  For example, OWL EL is intended to be useful in circumstances where there are many properties or classes,  while OWL QL is intended to be useful in applications with large amounts of instance data where query answering is the primary reasoning task.

## 7.5. How does one create an OWL ontology? ##

Because of the complexity of OWL, OWL-based ontologies are nearly always constructed using a software tool called an ontology editor.  The most widespread is Protégé [(12)](#12_Prot%C3%A9g%C3%A9_ontology_editor.md) which is free and open source, although other editors are available.  [(13)](#13_OWL_tools.md)  The _Protégé OWL Tutorial_ [(14)](#14_A_Practical_Guide_To_Building_OWL_Ontologies_Using_Prot%C3%A9g%C3%A9.md) is a straightforward guide (with examples) for using Protégé.

## 7.6. OWL basics ##
The namespace abbreviation for OWL terms is `owl: = http://www.w3.org/2002/07/owl#`

### 7.6.1. OWL and RDFS ###
Since OWL is an extension of RDFS, it contains some of the concepts introduced to RDF by RDFS.  OWL uses classes and properties, and includes terms from RDFS and RDF including `rdf:Property`, `rdfs:subClassOf`, `rdfs:subPropertyOf`, `rdfs:range`, and `rdfs:domain` which were discussed in [section 4.3](Beginners4Vocabularies#4.3._The_DCMI_Abstract_Model_(DCAM).md) and [section 4.4](Beginners4Vocabularies#4.4._RDF_Schema_and_the_relationship_of_the_DCMI_Abstract_Model.md).

### 7.6.2. owl:Class and individuals ###
The concept of a class in OWL is similar to its meaning in RDFS.  In fact,
```
owl:Class rdfs:subClassOf rdfs:Class
```
[(15)](#15_Axiomatic_Triples_for_the_Classes_of_the_OWL_2_RDF-Based_Voca.md)  In OWL, there is a built-in most general class named `owl:Thing`.  All other OWL classes are automatically subclasses of `owl:Thing`.  In OWL, instances of classes are called _individuals_.

#### 7.6.2.1. owl:DisjointClasses ####
OWL allows any two classes to be declared _disjoint_, i.e. it is not allowable for an individual to be an instance of both classes.  Unless disjointness is declared explicitly, it is allowable for an individual to be simultaneously a member of any two (or more) classes.

### 7.6.3. Properties in OWL ###
In OWL, properties state relationships involving individuals, just as in RDFS properties state relationships involving instances of classes.  OWL defines two types of properties: `owl:ObjectProperty` which relates individuals to other individuals and `owl:DatatypeProperty` which relates individuals to data values (strings, numbers, etc.).  Both of these kinds of properties are `rdfs:subClassOf rdf:Property`.

Outside of OWL, if a particular term is defined to be `rdf:type rdf:Property`, then it is not necessarily clear whether the object of a triple which has that property as a predicate should be a literal or a URI.  For example, if one wanted to describe a name in RDF using `dwc:nameAccordingTo`, a Darwin Core property, should the object be a literal as in:
```
urn:lsid:ubio.org:namebank:2472422   dwc:nameAccordingTo  "Claramunt Derryberry et al. 2010"
```
or should it be a URI?
```
urn:lsid:ubio.org:namebank:2472422   dwc:nameAccordingTo  http://dx.doi.org/10.1525/auk.2009.09022
```
[(16](#16_Expressing_DOIs_as_HTTP_URIs.md)) There is no clear answer to this question.  [(17)](#17_Should_Darwin_Core_terms_have_literals_or_URIs_as_objects?.md)  However, in OWL the distinction is clear.  In the following example the appropriate type of the object resource is unambiguous. (`tc: = http://rs.tdwg.org/ontology/voc/TaxonConcept#`)
```
urn:lsid:ubio.org:namebank:2472422   tc:accordingToString  "Claramunt Derryberry et al. 2010"
```
or
```
urn:lsid:ubio.org:namebank:2472422   tc:accordingTo  http://dx.doi.org/10.1525/auk.2009.09022
```
because `tc:accordingToString` is defined as an `owl:DatatypeProperty`, while `tc:accordingTo` is defined as an `owl:ObjectProperty`.  [(18)](#18_TDWG_Taxon_Concept_Ontology.md)

### 7.6.4. Statements of equivalence in OWL ###
OWL provides a means of indicating that resources are equivalent.

#### 7.6.4.1. owl:equivalentClass ####
Making the statement `X owl:equivalentClass Y` essentially means that two named classes are synonymous, i.e. that all instances of class X are instances of class Y and vice versa.  For example, in the TDWG Taxon Concept Ontology [(18)](#18_TDWG_Taxon_Concept_Ontology.md), the `tc:Taxon` class and the `tc:TaxonConcept` class are declared to be equivalent.

#### 7.6.4.2. owl:equivalentProperty ####
In OWL, if two properties are declared to be equivalent, they relate an individual to the same set of other individuals.  [(19)](#19_Equivalent_properties_in_RDFS.md)  For example, Dublin Core has declared that
```
dcterms:creator owl:equivalentProperty foaf:maker
```
This means that
```
 kimage:ac1490  dcterms:creator   agents:kirchoff#coblea
```
implies
```
 kimage:ac1490  foaf:maker   agents:kirchoff#coblea
```
The definition of `foaf:maker`  [(20)](#20_Definition_of_the_FOAF_vocabulary_in_RDF.md), which is written in OWL, declares that `foaf:maker` is an `owl:ObjectProperty` which means that the object of a triple using that property should be a URI.  The [definition](http://purl.org/dc/terms/creator) of `dcterms:creator`, which primarily uses RDFS, specifies a non-literal range (`dcterms:Agent`), so there is no inconsistency.  However, there has historically been confusion over whether `creator` in Dublin Core should refer to a person or a person's name.  The FOAF guidelines suggest that `dc:creator` (as opposed to `dcterms:creator`) should be used for textual names and `foaf:maker` should be used to refer to the creators as identified by URIs.  [(21)](#21_Definition_of_foaf:maker.md)

#### 7.6.4.3. owl:sameAs ####
The property owl:sameAs is used to state that two individuals (i.e. class instances) are the same.  The practical effect of this is to say that if we declare `uri1 owl:sameAs uri2`, and a statement is made in the form of a triple containing `uri1`, one can infer that the triple formed by substituting `uri1` for `uri2` represents a logically correct assertion (assuming that the original assertion is itself correct).  Informally, this means that `uri1` and `uri2` identify the same resource.  For example, if
```
http://biocol.org/urn:lsid:biocol.org:col:35115  owl:sameAs  urn:lsid:biocol.org:col:35115
```
[(22)](#22_Life_Science_Identifiers_(LSID)_Applicability_Statement.md) and the triple
```
http://bioimages.vanderbilt.edu/ind-baskauf/11657.rdf  foaf:maker  http://biocol.org/urn:lsid:biocol.org:col:35115
```
is stated, then it can be reasoned that
```
http://bioimages.vanderbilt.edu/ind-baskauf/11657.rdf  foaf:maker  urn:lsid:biocol.org:col:35115
```

The property `owl:sameAs` is a very powerful and a very dangerous thing.  If Institution A describes item `url1` using many triples stored in a dataset and Institution B describes item `url2` using many other triples stored in the same dataset, then an assertion by Person C that
`uri1 owl:sameAs uri2`
effectively merges all parts of the graph which relate to both `uri1` and `uri2`.  This may be a good thing, but if `uri1` and `uri2` aren't actually precisely the same thing, the result might be silly or possibly logically inconsistent statements.[(25)](#25_Reference_on_owl:sameAs.md)

### 7.6.5. OWL property characteristics ###
OWL allows the creator of an ontology to specify special characteristics of properties that can be used by machines (reasoners) to infer triples that are not explicitly stated.  Several of these characteristics are described below.
#### 7.6.5.1. owl:inverseOf ####
If  `propertyA owl:inverseOf propertyB` then if
```
x propertyA y
```
then
```
y propertyB x
```
Well-known pairs of inverse properties include: `foaf:made/foaf:maker` and `foaf:depiction/foaf:depicts`

#### 7.6.5.2. owl:TransitiveProperty ####
If a property is transitive, then if
```
x property y
```
and
```
y property z
```
then
```
x property z
```
For example, in the Plant Ontology, `is_a` is a transitive property.  If
```
po:0020045 (pinnate leaf)  is_a  po:0020043 (compound leaf)
```
and
```
po:0020043 (compound leaf) is_a po:0009025 (vascular leaf)
```
then it can be inferred that
```
po:0020045 (pinnate leaf) is_a po:0009025 (vascular leaf)
```

#### 7.6.5.3. owl:FunctionalProperty ####
A property that is declared to be an `owl:FunctionalProperty` can have only one unique value as an object.  An example is `foaf:primaryTopic` which relates a document to the thing which its main topic.  Because of the `owl:FunctionalProperty` declaration, a document can have only one `foaf:primaryTopic`.  In a manner similar the OWL terms of equivalence, using `owl:FunctionalProperty` can cause a reasoner to infer that individuals identified by different URIs are the same.  For example, if two triples using `foaf:primaryTopic` to describe the same subject resource have different object URIs, a reasoner would infer that the resources identified by those object URIs are the same.  For example, if I state
```
http://bioimages.vanderbilt.edu/baskauf/10998.rdf foaf:primaryTopic http://bioimages.vanderbilt.edu/baskauf/10998
```
(a true statement declaring an RDF-formatted document to have an image as its `foaf:primaryTopic`), and if the following statement were also made (perhaps by mistake):
```
http://bioimages.vanderbilt.edu/baskauf/10998.rdf foaf:primaryTopic http://bioimages.vanderbilt.edu/ind-baskauf/10997
```
(that the primary topic of the document is the trees which are depicted in the image), then a reasoner would conclude
```
http://bioimages.vanderbilt.edu/baskauf/10998 owl:sameAs http://bioimages.vanderbilt.edu/ind-baskauf/10997
```
(i.e. the image is the same thing as the tree) and subsequently could conclude that all properties of the image also apply to the tree, e.g. the tree was a StillImage created by Steven J. Baskauf and that the image was a natualized IndividualOrganism.  For this reason functional properties (and inverse functional properties) should be used with caution.

#### 7.6.5.4. Other property characteristics ####
`owl:InverseFunctionalProperty` and `owl:SymmetricProperty` are two additional properties which can be used to describe the characteristics of properties more fully. [(10)](#10_OWL_Lite_Feature_Synopsis.md) [(14)](#14_A_Practical_Guide_To_Building_OWL_Ontologies_Using_Prot%C3%A9g%C3%A9.md)

## 7.7. What is reasoning? ##
Software applications which are designed to examine sets of OWL statements and draw inferences from them are called _reasoners_.  The function of reasoners can be described as follows:

"When humans think, they draw consequences from their knowledge. An important feature of OWL is that it captures this aspect of human intelligence for the forms of knowledge that it can represent. But what does it mean, generally speaking, that a statement is a consequence of other statements? Essentially it means that this statement is true whenever the other statements are. In OWL terms: we say, a set of statements `A` entails a statement `a` if in any state of affairs wherein all statements from `A` are true, also `a` is true. Moreover, a set of statements may be consistent (that is, there is a possible state of affairs in which all the statements in the set are jointly true) or inconsistent (there is no such state of affairs). The formal semantics of OWL specifies, in essence, for which possible “states of affairs” a particular set of OWL statements is true.  There are OWL tools – reasoners – that can automatically compute consequences." [(23)](#23_Description_of_reasoning_in_basic_notions_on_modeling_knowled.md)

One basic function that a reasoner can perform is to check an OWL ontology for _consistency_, i.e. whether it is possible for a class to have any instances.  It can also infer an ontology class hierarchy which may go beyond the hierarchy asserted explicitly by OWL statements. [(24)](#24_Inconsistent_Classes.md)

Some reasoners which are available are listed at [(13)](#13_OWL_tools.md).

### 7.7.1. Some publications related to reasoning ###
A method of reasoning, which uses rules to infer triples from an OBO ontology followed by SPARQL queries, is described in Blondé et al. 2011 ([doi: 10.1093/bioinformatics/btr164](http://dx.doi.org/10.1093/bioinformatics/btr164)).

Hogan et al. describe a "system for performing rule-based forward-chaining reasoning which we call SAOR: Scalable Authoritative OWL Reasoner" at http://www.deri.ie/fileadmin/documents/DERI-TR-2009-04-21.pdf.  Aidan Hogan, Andreas Harth and Axel Polleres.  Scalable Authoritative OWL Reasoning for the Web.  International Journal on Semantic Web and
Information Systems, 5(2), pages 49-90, April-June 2009.

The principles of Referent Tracking, which can be used to represent and track "particulars" (instances which are based in objective reality), is discussed in [Cuesters and Smith. 2007](http://ceur-ws.org/Vol-249/submission_105.pdf).  Referent Tracking is designed to support unique identifiers and reduce ambiguity with the ultimate goal of facilitating reasoning.

Calder et al. [doi:10.1016/j.ecoinf.2009.08.007](http://dx.doi.org/10.1016/j.ecoinf.2009.08.007) describe a validation tool which uses machine reasoning to draw inferences about anomalous sensor data.

Rector et al. OWL Pizzas: Practical Experience of Teaching OWL-DL: Common Errors & Common Patterns http://www.co-ode.org/resources/papers/ekaw2004.pdf

# References #
### 1 Annotations in Web Ontology Language ###
In some forms of OWL (e.g. OWL DL) there are restrictions on the use of annotation properties because if they are used incorrectly they would prevent a machine reasoner from completing its task. See
http://www.w3.org/TR/owl-ref/#Annotations

### 2 FOAF Vocabulary Specification ###
http://xmlns.com/foaf/spec/

### 3 Plant Ontology ###

http://www.plantontology.org/

### 4 The Open Biological and Biomedical Ontologies ###

http://www.obofoundry.org/

For unambiguous formal definitions of the primitive relationships used in OBO ontologies, see Smith et al. 2005. Relations in biomedical ontologies. `Genome Biology 6:R46` [doi:10.1186/gb-2005-6-5-r46](http://dx.doi.org/10.1186/gb-2005-6-5-r46)

### 5 OWL 2 Web Ontology Language Primer ###
OWL is a W3C Recommendation with a number of normative documents.  This particular document was designed for novices.

http://www.w3.org/TR/owl-primer/

### 6 What is OWL 2? ###

http://www.w3.org/TR/owl2-primer/#What_is_OWL_2.3F

### 7 OMG Unified Modeling Language (UML) ###

http://www.omg.org/spec/UML/2.1.2/Infrastructure/PDF/

### 8 OWL 2 Overview ###

http://www.w3.org/TR/owl2-overview/#Overview

### 9 OWL 2 DL and OWL 2 Full ###

http://www.w3.org/TR/owl2-primer/#OWL_2_DL_and_OWL_2_Full

### 10 OWL Lite Feature Synopsis ###

http://www.w3.org/TR/2004/REC-owl-features-20040210/#s2.1

### 11 OWL 2 Web Ontology Language Profiles ###
http://www.w3.org/TR/owl-profiles/

### 12 Protégé ontology editor ###

http://protege.stanford.edu/

### 13 OWL tools ###

http://www.w3.org/TR/owl2-primer/#OWL_Tools

A commonly used reasoner is Pellet:

http://clarkparsia.com/pellet ([Pellet tutorial](http://clarkparsia.com/pellet/tutorial))

### 14 A Practical Guide To Building OWL Ontologies Using Protégé 4 and CO-ODE Tools ###

http://owl.cs.manchester.ac.uk/tutorials/protegeowltutorial/

### 15 Axiomatic Triples for the Classes of the OWL 2 RDF-Based Vocabulary ###

http://www.w3.org/TR/owl2-rdf-based-semantics/#A_Set_of_Axiomatic_Triples

### 16 Expressing DOIs as HTTP URIs ###
http://www.crossref.org/CrossTech/2011/04/content_negotiation_for_crossr.html

### 17 Should Darwin Core terms have literals or URIs as objects? ###
Darwin Core includes "ID" versions of several terms.  For example `dwc:nameAccordingTo` shows strings as its examples, while its corresponding ID term `dwc:nameAccordingToID` is defined to be an identifier.  However, since Darwin Core does not have a RDF Guide indicating how its terms should be used and since the normative definition of terms in RDF describe the property terms as `rdf:type rdf:Property`, there are no clear guidelines for how the ID terms might be used in RDF triples.  The example given in the XML Guide (http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#classes) uses `dwc:locationID` as both an identifier for the subject resource and as an ID reference for the object of a property.  The situation is further complicated by the fact that all of the ID terms are declared to be subproperties of `dcterms:identifier` which has range `rdfs:Literal`.  This implies that the ID terms also have range `rdfs:Literal`, which might not be the intent of Darwin Core.  See [this](#1.3.2.4._dcterms:identifier_(AC).md) for more information.

In some cases (such as `dwc:recordedBy`), the definition clearly states that the object of the property should be text.  But in many other cases, usage is not clear.

### 18 TDWG Taxon Concept Ontology ###
http://rs.tdwg.org/ontology/voc/TaxonConcept

viewable at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.owl

### 19 Equivalent properties in RDFS ###
In RDFS, the same thing can be accomplished by declaring two properties to be subproperties of each other, e.g.
```
A rdfs:subPropertyOf B
B rdfs:subPropertyOf A
```

### 20 Definition of the FOAF vocabulary in RDF ###
http://xmlns.com/foaf/spec/index.rdf

### 21 Definition of foaf:maker ###
http://xmlns.com/foaf/spec/#term_maker

For additional discussion of `dcterms:creator` and `foaf:maker`, see

http://wiki.foaf-project.org/w/UsingDublinCoreCreator

The DCMI notes on the specifications for Dublin Core metadata in RDF specifies that literal value strings for a value should be expressed using the `rdf:value` property for resources that should be represented as URI references.

http://dublincore.org/documents/dc-rdf/#sect-4

This strategy is clarified at

http://dublincore.org/documents/dc-rdf-notes/#sect-3

which describes the best practices for this situation in Dublin Core.  Use of `rdf:value` is described at

http://www.w3.org/TR/rdf-primer/#rdfvalue

### 22 Life Science Identifiers (LSID) Applicability Statement ###
The [LSID Applicability Statement](http://www.tdwg.org/standards/150/) ([pdf viewable in browser](http://bioimages.vanderbilt.edu/pages/LSID%20AS_2011_01_final.pdf)) states in Recommendation 30 that descriptions of objects identified by LSIDs must contain an OWL statement of equivalence (e.g. `owl:sameAs`) that relates the LSID to its HTTP proxied form.

### 23 Description of reasoning in basic notions on modeling knowledge ###
http://www.w3.org/TR/owl2-primer/#Modeling_Knowledge:_Basic_Notions

### 24 Inconsistent Classes ###
Refer to section 4.9.2. of _A Practical Guide To Building OWL Ontologies Using Protégé 4 and CO-ODE Tools_ at

http://owl.cs.manchester.ac.uk/tutorials/protegeowltutorial/

### 25 Reference on owl:sameAs ###
Harry Halpin, Patrick J. Hayes, James P. McCusker, Deborah L. McGuinness,
and Henry S. Thompson. 2010. When owl:sameAs isn’t the Same: An Analysis of Identity in Linked Data. International Semantic Web Conference (ISWC).

http://iswc2010.semanticweb.org/pdf/261.pdf


---

Thanks to Paul Murray and Bob Morris for helpful suggestions on this page.

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