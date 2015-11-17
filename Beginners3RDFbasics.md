<a href='Hidden comment: 
ToDo: write something about blank nodes
'></a>

# Beginner's guide to RDF: 3. RDF basics #

This guide is intended to help people understand what RDF is and what it is used for.  (For more information, see the [Introduction](Beginners.md).)  It is not intended to teach people how to write RDF.  [Section 3.4.](#3.4._Learn_more_about_RDF.md) provides links to some Web resources for people who want to actually learn to create documents in RDF.

[go to part 2: What is RDF and what is it for?](Beginners2WhatIsRDF.md)

[go to part 4: Vocabularies, DCAM, and RDFS](Beginners4Vocabularies.md)

[Introduction to the Guide](Beginners.md)

**Contents**



## 3.1. What is a triple? ##
The basic unit of RDF is a statement called a triple.  One can think of a triple as a type of sentence that states a single "fact" about a resource.

### 3.1.1. Subject ###
The first part of the triple, the resource being described, is known as the subject of the triple.  The subject is a URI reference to that resource which identifies it unambiguously, i.e. is a globally unique identifier (GUID) for described resource. [(1)](#1_Blank_nodes..md)

### 3.1.2. Predicate ###
The subject is followed by the predicate which indicates the kind of relationship that is being described by the triple.  The predicate is also called the _property_.  Like the subject, the predicate is also described by a URI.  The predicate is generally a term from a well-known vocabulary or ontology (see [section 0.3.7.](Beginners#0.3.7._Biodiversity-related_and_General_vocabularies_and_ontolog.md) for examples of vocabularies and ontologies relevant to the biodiversity community).  The URI is often constructed from a term name in such a way that when abbreviated it will impart to a human a sense of what kind of property the predicate is describing.  For example, the URI predicate

http://purl.org/dc/terms/creator

can be written as `dcterms:creator` where `dcterms:` is an abbreviation for "`http://purl.org/dc/terms/`".  A human will see this term abbreviation as a property that describes the creator of the subject.  However, a computer will simply see the URI as a unique string unless it uses other sources of information to "understand" what that URI "means" as a property.

### 3.1.3. Object ###
The last part of the triple is the object.  The object represents something that is related to the subject through the relationship described by the predicate.  The object can be of two types: literals (character strings) and URIs.  Although in basic RDF there is technically no defined difference between predicates whose object is a literal, and predicates whose object is a URI, predicates whose objects are literals probably tend to be simple properties of the object, while predicates whose objects are URIs are more likely to express relationships between the object and some other resource that is itself likely to be the object of additional RDF descriptions.  Web Ontology Language (OWL) provides a means to declare whether a predicate is a literal or a URI reference (see [section 7.6.3.](Beginners7OWL#7.6.3._Properties_in_OWL.md) for more on this).

## 3.2. Examples of triples ##
The examples given in the remainder of this section use actual functional URIs which should dereference to HTML in a web browser and RDF/XML in a semantic client such as an RDF browser.  Since these represent resources "in the wild" the actual RDF triples are subject to change.  (Note: as of 2012-01-26 the server responding to requests to dereference the `bioimages.vanderbilt.edu` URIs does not correctly identify the RDF/XML files as "Content-type: application/rdf+xml".  This may cause clients to misinterpret the type of response when the client requests an RDF/XML representation of a URI.)

### 3.2.1. Conventions used in the examples ###
In the following examples, the namespace abbreviation
```
rdf: is an abbreviation for "http://www.w3.org/1999/02/22-rdf-syntax-ns#"
kimage: is an abbreviation for "http://bioimages.vanderbilt.edu/kirchoff/",
agents: is an abbreviation for "http://bioimages.vanderbilt.edu/contact/",
foaf: is an abbreviation for "http://xmlns.com/foaf/0.1/", 
dc: is an abbreviation for "http://purl.org/dc/elements/1.1/",
dctype: is an abbreviation for "http://purl.org/dc/dcmitype/", and 
dcterms: is an abbreviation for "http://purl.org/dc/terms/".
```

These examples describe a digital image identified by the URI
`http://bioimages.vanderbilt.edu/kirchoff/ac1490`
which is abbreviated as `kimage:ac1490`.

### 3.2.2. Example of a triple having a literal as its object ###
The triple
```
kimage:ac1490  dcterms:created  "2010-09-01T03:41:31"
```
can be interpreted by a human to say that the image was created on 1 September 2010.  A computer would "know" this if it were programmed to recognize that the URI dcterms:created represented the creation date of a resource and if it were programmed to parse and interpret ISO 8601 formatted date strings.  Literals can also be _typed_ to indicate explicitly their language or datatype. [(2)](#2_Typed_literals..md)

### 3.2.3. Example of a triple having a URI as its object ###
The triple
```
kimage:ac1490  foaf:maker  agents:kirchoff#coblea
```
can be interpreted by a human to say that the image was made the person or organization `kirchoff#coblea`.  If a computer were programmed to recognize the foaf vocabulary, it could interpret this triple to mean that the image was made by some person or organization, but would have no further information about the nature of that agent without additional triples describing `agents:kirchoff#coblea` .

### 3.2.4. Additional triple examples ###
Here are two more statements in RDF about the image:

```
kimage:ac1490  dc:rights  "(c) 2011 Bruce K. Kirchoff"
kimage:ac1490  rdf:type  dctype:StillImage
```

The first describes the copyright statement associated with the image.  The second statement uses a special predicate which is defined in the RDF specification for the specific purpose of indicating the kind of thing (the type) of the subject. [(3)](#3_rdf:type.md)

## 3.3. Serializations of RDF ##
RDF is a model for representing statements about properties of resources. [(4)](#4_Formal_definition_of_the_RDF_model.md)  However, the RDF model is independent of any specific serialization syntax. [(5)](#5_Design_goals_of_RDF.md)  What this means is that there are a number of methods of expressing the information that is contained in RDF triples and the information expressed by these methods is equivalent.

The following examples will illustrate how the following information can be expressed in various serializations of RDF: "The still image having the identifier `kimage:ac1490` was made by `agents:kirchoff#coble` (a person named Ashley Coble) on 1 September 2010 at 3:41:31 AM.  It is copyright 2011 by Bruce K. Kirchoff."

### 3.3.1. Raw RDF triples ###
The following table shows the six triples that are required to express the information in RDF.  In this table, the full URIs are given.
|Subject	|Predicate	|Object|
|:-------|:---------|:-----|
|http://bioimages.vanderbilt.edu/kirchoff/ac1490	|http://www.w3.org/1999/02/22-rdf-syntax-ns#type	|http://purl.org/dc/dcmitype/StillImage|
|http://bioimages.vanderbilt.edu/kirchoff/ac1490	|http://xmlns.com/foaf/0.1/maker	|http://bioimages.vanderbilt.edu/contact/kirchoff#coblea|
|http://bioimages.vanderbilt.edu/kirchoff/ac1490	|http://purl.org/dc/terms/created	|"2010-09-01T03:41:31"|
|http://bioimages.vanderbilt.edu/kirchoff/ac1490	|http://purl.org/dc/elements/1.1/rights	|"(c) 2011 Bruce K. Kirchoff"|
|http://bioimages.vanderbilt.edu/contact/kirchoff#coblea	|http://www.w3.org/1999/02/22-rdf-syntax-ns#type	|http://xmlns.com/foaf/0.1/Person|
|http://bioimages.vanderbilt.edu/contact/kirchoff#coblea	|http://xmlns.com/foaf/0.1/name	|"Ashley Coble"|

The table below contains the same six triples, but using the namespace abbreviations for brevity:
|Subject	|Predicate	|Object|
|:-------|:---------|:-----|
|kimage:ac1490	|rdf:type	 |dctype:StillImage|
|kimage:ac1490	|foaf:maker	|agents:kirchoff#coblea|
|kimage:ac1490	|dcterms:created	|"2010-09-01T03:41:31"|
|kimage:ac1490	|dc:rights	|"(c) 2011 Bruce K. Kirchoff"|
|agents:kirchoff#coblea	|rdf:type	 |foaf:Person|
|agents:kirchoff#coblea	|foaf:name	|"Ashley Coble"|


### 3.3.2. Graphical representation ###
The following diagram shows the triples represented in graphical form using the unabbreviated URIs.

![http://tdwg-rdf.googlecode.com/svn/trunk/file/rdf-graph-example.jpg](http://tdwg-rdf.googlecode.com/svn/trunk/file/rdf-graph-example.jpg)

The diagram is more compact if namespaces are abbreviated:

![http://tdwg-rdf.googlecode.com/svn/trunk/file/simplified-rdf-graph-example.jpg](http://tdwg-rdf.googlecode.com/svn/trunk/file/simplified-rdf-graph-example.jpg)

The convention for graphical representations of RDF are:
  * URIs are represented as ovals
  * literals are represented as rectangles
  * predicates are represented as arrows pointing from the subject to the object.

In the RDF model, a set of triples is referred to as a graph.  This is a general term and does not specifically refer to a graphical representation such as the one shown here.  The subjects and objects are referred to as nodes.  The predicates are referred to as arcs.  A graph represents the network of relationships that are described by all of the triples that are included in the set. [(6)](#6_Graph_data_model_of_RDF.md)

### 3.3.3. XML representation ###

```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:foaf="http://xmlns.com/foaf/0.1/"
>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/ac1490">
  <rdf:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>
  <foaf:maker rdf:resource="http://bioimages.vanderbilt.edu/contact/kirchoff#coblea"/>
  <dcterms:created>2010-09-01T03:41:31</dcterms:created>
  <dc:rights>(c) 2011 Bruce K. Kirchoff</dcterms:rights>
</rdf:Description>

<foaf:Person rdf:about="http://bioimages.vanderbilt.edu/contact/kirchoff#coblea">
  <foaf:name>Ashley Coble</foaf:name>
</foaf:Person>

</rdf:RDF>
```

Although RDF can be expressed in any of a number of serializations, XML has a special status.  The W3C specification for RDF specifically recommends XML as the form of serialization used for the exchange of information among applications. [(7)](#7_XML-based_syntax.md)  Exchange of data using other serializations is not prohibited, but making RDF data available in XML is a best practice because it is widely understood.  XML serialization has been criticized as not easily "read" by humans, but since its primary purpose is information exchange among machines and since most RDF/XML will probably be generated automatically, this should not be a major impediment to its implementation.  There are converters (discussed in [section 3.3.5.](#3.3.5._RDF_validation_and_conversion_from_one_serialization_to_a.md)) that can readily convert RDF/XML into other serializations.

In [section 3.2.3.](#3.2.3._Additional_triple_examples.md) it was noted that the predicate `rdf:type` has the special role in RDF of indicating class membership.  As a shortcut method in RDF/XML, the XML container element for the object being described can be named as the class of which the described resource is an instance rather than using the generic `rdf:Description` container name.  When this is done, there is an implied `rdf:type` statement that is not shown in the actual XML but which exists and will be listed in any set of triples or shown in any graphical representation.  So the two XML snippets:

```
<foaf:Person rdf:about="http://bioimages.vanderbilt.edu/contact/kirchoff#coblea">
  <foaf:name>Ashley Coble</foaf:name>
</foaf:Person>
```

and

```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/contact/kirchoff#coblea">
  <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
  <foaf:name>Ashley Coble</foaf:name>
</rdf:Description>
```

say exactly the same thing.

It is also possible to accomplish the description of both resources (the StillImage and the Person) by nesting the XML rather than describing them separately and linking them through a URI object reference in the `foaf:maker` property:

```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:foaf="http://xmlns.com/foaf/0.1/"
>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/ac1490">
  <rdf:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>
  <foaf:maker>
    <foaf:Person rdf:about="http://bioimages.vanderbilt.edu/contact/kirchoff#coblea">
      <foaf:name>Ashley Coble</foaf:name>
    </foaf:Person>
  </foaf:maker> 
  <dcterms:created>2010-09-01T03:41:31</dcterms:created>
  <dc:rights>(c) 2011 Bruce K. Kirchoff</dcterms:rights>
</rdf:Description>

</rdf:RDF>
```

Again, this would produce exactly the same triples and graphical representation as the first example.

### 3.3.4. Notation 3 (N3) representation ###

```
@prefix foaf: <http://xmlns.com/foaf/0.1/>.
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dc: <http://purl.org/dc/elements/1.1/>.
@prefix dcterms: <http://purl.org/dc/terms/>.
<http://bioimages.vanderbilt.edu/contact/kirchoff#coblea> 
	a foaf:Person;
	foaf:name "Ashley Coble".
<http://bioimages.vanderbilt.edu/kirchoff/ac1490> 
	dcterms:created "2010-09-01T03:41:31";
	dc:rights "(c) 2011 Bruce K. Kirchoff";
	a <http://purl.org/dc/dcmitype/StillImage>;
	foaf:maker <http://bioimages.vanderbilt.edu/contact/kirchoff#coblea>.
```

Notation 3 (N3) and a more simplified version known as Terse RDF Triple Language (Turtle) is considered by some to be a more "human-friendly" way of expressing RDF.  Toolkits for creating RDF often support Turtle.

In N3, the subject is listed, followed by an indented list predicate/object pairs.  The special role of the `rdf:type` property is recognized here by using "a" in place of the `rdf:type` predicate, i.e. saying that `agents:kirchoff#coblea` is "a `foaf:Person`".

### 3.3.5. RDF validation and conversion from one serialization to another. ###

There are several tools that can be used to validate the syntax of RDF and to convert from one kind of serialization to another.

#### 3.3.5.1. XML validation and graphical visualization ####

The W3C provides a validation service at
http://www.w3.org/RDF/Validator/
which can be used to generate raw triples, a graphical visualization, or both from RDF/XML.

#### 3.3.5.2. Conversion from XML to N3 or N3 to XML ####
A converter is available at
http://www.rdfabout.com/demo/validator/

#### 3.3.5.3. Stand-alone RDF editor ####
Links to this kind of tool are found in [section 0.3.5.](Beginners#0.3.5._Software_tools.md) of this guide.

## 3.4. Learn more about RDF ##
The W3C has a Recommendation known as the RDF Primer [(8)](#8_W3C_RDF_Primer.md) which elaborates on the information provided here as well as covering a number of topics beyond the scope of this guide.  The References section [(9)](#9_RDF_Primer_Reference_section.md) provides a comprehensive list of other informational resources related to RDF.

The w3schools  website also provides an RDF tutorial [(10)](#10_w3schools.com_RDF_tutorial.md) at

http://www.w3schools.com/rdf/default.asp

# References #
### 1 Blank nodes. ###
Technically either the subject or the object can be a blank node which is not identified explicitly by a URI.  See http://www.w3.org/TR/rdf-primer/#structuredproperties for a description of blank nodes and their use.  It is generally considered a less-desirable practice to introduce blank nodes because it is not possible to link to them through external documents.  However, in some cases blank nodes are unavoidable if identifiers don't exist or if the creator of the RDF does not want to be responsible for minting and maintaining an identifier for the described resource.

### 2 Typed literals. ###
An RDF literal object can be typed using an optional attribute within the predicate tag.  These include an optional XML language attribute ([xml:lang](http://www.w3.org/TR/REC-xml/#sec-lang-tag), see also [RFC 4646](http://tools.ietf.org/html/rfc4646) ) or RDF datatype ([rdf:datatype](http://www.w3.org/TR/rdf-concepts/#section-Datatypes)).  Note: `xsd:` abbreviates `http://www.w3.org/2001/XMLSchema#`.  Presumably, any XML Schema defined datatype ( http://www.w3.org/TR/xmlschema-2/ ) such as [xsd:dateTime](http://www.w3.org/TR/xmlschema-2/#dateTime) would be widely understood and appropriate for use with the `rdf:datatype` attribute.  It is also possible for users to define their own `rdf:datatype`, although it seems likely that only custom-designed consuming applications would know how to make use of this information. The guidelines for Dublin Core as RDF specify that the `rdf:datatype` can be specified by reference to a "syntax encoding scheme URI".  Dublin Core defines URIs for a number of commonly used schemes at http://dublincore.org/documents/dcmi-terms/#H5 .

### 3 rdf:type ###
The predicate `rdf:type` has special properties that are defined in the RDF schema:

http://www.w3.org/TR/rdf-schema/#ch_type

In particular, use of that predicate implies class membership for the subject resource.  However, there is not (yet) any standard list of types and classes which should be used with particular kinds of resources in our community.  Some of the classes which have been defined by our community are listed in [section 4.7.2.](Beginners4Vocabularies#4.7.2._What_can_we_find_classes_to_use_in_rdf:type_statements?.md) of this guide.  The digital image in the example is typed as `dctype:StillImage` for illustrative purposes.

### 4 Formal definition of the RDF model ###
http://www.w3.org/TR/1999/REC-rdf-syntax-19990222/#model

### 5 Design goals of RDF ###
http://www.w3.org/TR/rdf-concepts/#section-simple-data-model

### 6 Graph data model of RDF ###
http://www.w3.org/TR/rdf-concepts/#section-data-model

### 7 XML-based syntax ###
http://www.w3.org/TR/rdf-concepts/#section-xml-serialization which references
http://www.w3.org/TR/2004/REC-rdf-syntax-grammar-20040210/

### 8 W3C RDF Primer ###
http://www.w3.org/TR/rdf-primer/

### 9 RDF Primer Reference section ###
http://www.w3.org/TR/rdf-primer/#references

### 10 w3schools.com RDF tutorial ###
http://www.w3schools.com/rdf/default.asp



---

Thanks to Paul Murray for helpful comments and suggestions on this page.

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