# Introduction #

This was instigated by a thread on the RDF TG mailing list under the subject line: "`[tdwg-rdf: 316]` [What is the meaning of the object of a triple?](https://groups.google.com/d/msg/tdwg-rdf/2Ahae48_myg/F4FDMcMBoPQJ)"

# Quotes from RFC 3986 (the URI spec) and W3C recs on RDF #

"An identifier embodies the information required to distinguish  what is being identified from all other things within its scope of identification.  Our use of the terms "identify" and "identifying" refer to this purpose of distinguishing one resource from all other resources, regardless of how that purpose is accomplished  (e.g., by name, address, or context). ... A URI is an identifier consisting of a sequence of characters   matching the syntax rule named `<URI>` in Section 3." `[1]`

"The underlying structure of any expression in RDF is a collection of triples, each consisting of a subject, a predicate and an object. ... Each triple represents a statement of a relationship between the things denoted by the nodes that it links. Each triple has three parts:  a subject, an object, and a predicate (also called a property) that denotes a relationship.  ... The nodes of an RDF graph are its subjects and objects.  The assertion of an RDF triple says that some relationship, indicated by the predicate, holds between the things denoted by subject and object of the triple. ... A node may be a URI with optional fragment identifier (URI reference, or URIref), a literal, or blank (having no separate form of identification). Properties are URI references. ...  A URI reference or literal used as a node identifies what that node represents.  A URI reference used as a predicate identifies a relationship between the things represented by the nodes it connects. ... Literals may be plain or typed :
  * A plain literal is a string combined with an optional language tag. This may be used for plain text in a natural language. As recommended in the RDF formal semantics `[RDF-SEMANTICS]`, these plain literals are self-denoting.
  * A typed literal is a string combined with a datatype URI. It denotes the member of the identified datatype's value space obtained by applying the lexical-to-value mapping to the literal string." `[2]`

The normative sections 5 and 6 of the rdf-concepts document define these terms more formally but abstractly.  They say little about what the components of triples denote/represent.  The RDF Semantics document uses the defintions found in `[2]`, it repeatedly uses the terms "denotes" or "denotation" to refer to the relationship between names (URIs, literals, etc.) and the things they represent.`[3]`  Things denoted by RDF names are called "resources".

`[1]` http://tools.ietf.org/html/rfc3986#section-1.1

`[2]` http://www.w3.org/TR/rdf-concepts/#section-data-model

`[3]` http://www.w3.org/TR/2004/REC-rdf-mt-20040210/#urisandlit

[An email discussing the distinction between "identifies" and "denotes"](http://lists.w3.org/Archives/Public/public-rdf-comments/2013Oct/0096.html)

# Conclusions #
  1. URIs are a sequence of characters that identify resources (things, entities).
  1. "URI" and "URI reference" and "URIref" mean the same thing.
  1. An RDF triple has "subject","predicate", and "object" as parts.  "Subject" and "object" are "nodes".
  1. An RDF triple represents a statement of a relationship between resources (things, entities) denoted by the nodes it links.
  1. The various RDF triple parts can be: URIs (almost always referred to as "URI references" in the context of triples), typed literals, untyped literals, and blank nodes.  Subjects and predicates are restricted to subsets of these.
  1. URIs identify resources.  URIs used as nodes denote related resources.  URIs used as predicates denote relationships.  "identify" and "denote" are both used to indicate the relationship between URIs and resources.  "represents" is also used.
  1. The kinds of triple parts denote various things:
  * URIs identify resources and properties.  A URI reference (a.k.a. URI) used as a node identifies what the node represents.  A URI reference used as a predicate identifies a relationship.
  * A typed literal denotes a member of the identified datype's value space (i.e., a literal typed as xsd:integer denotes an integer number)
  * An untyped literal is self-denoting (i.e., it denotes the text that it consists of)
  * A blank node denotes a related resource that is unnamed (because the node does not have a URI or literal value).

# Example #
## RDF/Turtle snippet ##

```
<http://bioimages.vanderbilt.edu/baskauf/67045#loc>
     a dcterms:Location;
     dwc:countryCode "US";
     dwc:minimumElevationInMeters "190"^^xsd:int;
     dwcuri:inDescribedPlace <http://sws.geonames.org/5339268/>.
_:bnode1
     a dwc:Event;
     dwc:eventDate "2008-07-20T17:17:41-07:00"^^xsd:dateTime;
     dsw:locatedAt <http://bioimages.vanderbilt.edu/baskauf/67045#loc>.
```
## Statements about the example ##
The URI `<http://sws.geonames.org/5339268/>` is composed of 32 characters.

The URI `<http://sws.geonames.org/5339268/>` is the object of a triple.

The URI `<http://sws.geonames.org/5339268/>` is a URI reference.

The URI `<http://sws.geonames.org/5339268/>` identifies the place named "Contra Costa County, California".

The URI `<http://sws.geonames.org/5339268/>` denotes the place named "Contra Costa County, California".

The blank node `_:bnode1` denotes an event that happened at 5:17:41 PM Pacific Daylight time on 20 July 2008.

The typed literal "190"^^xsd:int denotes the integer number whose value is 190.

The untyped literal "US" denotes the sequence of unicode characters "U" and "S".

---

The object of the triple:
```
<http://bioimages.vanderbilt.edu/baskauf/67045#loc> dwcuri:inDescribedPlace <http://sws.geonames.org/5339268/>.
```
  * is a URI.
  * is a URI reference.
  * is a node.
  * denotes the place named "Contra Costa County, California".
  * identifies the place named "Contra Costa County, California".

---

The object of the triple:
```
<http://bioimages.vanderbilt.edu/baskauf/67045#loc> dwc:minimumElevationInMeters "190"^^xsd:int.
```
  * is a literal.
  * is a typed literal.
  * is a node.
  * denotes an integer number.

---

The object of the triple:
```
<http://bioimages.vanderbilt.edu/baskauf/67045#loc> dwc:countryCode "US".
```
  * is a literal.
  * is an untyped literal.
  * is a node.
  * denotes two unicode characters.

---

The subject of the triple:
```
_:bnode1 dwc:eventDate "2008-07-20T17:17:41-07:00"^^xsd:dateTime.
```
  * is a node.
  * is a blank node.
  * denotes an event that happened at 5:17:41 Pacific Daylight time on 20 July 2008.
  * is not identified.

---

The predicate of the triple:
```
<http://bioimages.vanderbilt.edu/baskauf/67045#loc> dwc:countryCode "US".
```
  * is a property.
  * is a URI.

---

```
_:bnode1 dsw:locatedAt <http://bioimages.vanderbilt.edu/baskauf/67045#loc>.
```
  * is an RDF triple.
  * has a subject that is a blank node.
  * has a subject that is a unidentified.
  * has a predicate that is a URI.
  * has an object that is a URI.
  * has an object that is a URI reference.
  * has a subject that denotes an event.
  * has an object that denotes a location.
  * represents a statement of the relationship between an event and a location.

