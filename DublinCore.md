For a brief summary of this document see [usage notes on dcterms: terms](UsageDcterms.md)

<h1>Dublin Core in RDF</h1>

Steve Baskauf - TDWG RDF/OWL Best Practices Task Group - Created: 2012-02-24; Modified: 2013-11-09

**NOTE:** This document has not been updated to reflect the recommendations of the [Darwin Core RDF Guide](DwcRdf.md) and the final version of the [Audubon Core TDWG Standard](http://terms.tdwg.org/wiki/Audubon_Core).

**Table of Contents:**



# 1. Use of Dublin Core terms in RDF #

Note: whenever possible, examples use actual URIs or persistent identifiers.  Use of these identifiers does not imply endorsement of any particular organization or style of description.  In addition, although the statements made in the RDF examples are generally true, although they may or may not have actually been made in RDF which is returned when URI is dereferenced.

The [DCMI User Guide](http://wiki.dublincore.org/index.php/User_Guide) provides a general introduction to Dublin Core and has several examples of Dublin Core as RDF.

The [DCMI Metadata as linked data](http://wiki.dublincore.org/index.php/User_Guide/Publishing_Metadata) User Guide provides RDF examples in Turtle syntax for all of the `dcterms:` terms.

The DCMI [Publishing Metadata](http://wiki.dublincore.org/index.php/User_Guide/Creating_Metadata) User Guide provides guidelines for the creation of content.

## 1.1. Background ##

### 1.1.1. Legacy `dc:` terms vs. current `dcterms:` terms ###
In 2008, the Dublin Core Metadata Initiative (DCMI) issued a new set of terms under the current DCMI namespace: `http://purl.org/dc/terms/` (commonly abbreviated as `dcterms:`) to refine the terms in the Dublin Core legacy namespace: `http://purl.org/dc/elements/1.1/` (commonly abbreviated `dc:`).  The issuing of these terms followed the specification of the DCMI Abstract Model (DCAM) in 2007.  The development of the DCAM was in part a response to the development of the RDF Schema (RDFS) which it closely mirrors (see http://dublincore.org/documents/abstract-model/#sect-1).

### 1.1.2. Range and domain assignments for terms in the dcterms: namespace ###
When the new terms in the `dcterms:` namespace were issued, some of them were assigned domain and range properties as described at http://dublincore.org/documents/2008/01/14/domain-range/#sect-3 .  The rationale for this was described in the section "Addition of domains and ranges for existing properties and creation of new properties" in http://dublincore.org/usage/decisions/2008/dcterms-changes/#sect-2 .  To avoid conflicts with existing implementations of terms from the `dc:` namespace, no domain and range properties were assigned to the terms in the `dc:` namespace.

### 1.1.3. Subproperty relationships between terms in the dcterms: and dc: namespaces ###
As described in the section "Addition of domains and ranges for existing properties and creation of new properties" in http://dublincore.org/usage/decisions/2008/dcterms-changes/#sect-2 , each of the terms in the `dcterms:` namespaces which had a corresponding term in the legacy `dc:` namespace was defined to be a subproperty of that legacy term.  Thus an assertion made in RDF such as
```
uri1  dcterms:date   "2012-02-20"
```
implies
```
uri1 dc:date  "2012-02-20"
```
while the reverse is not true because there is no subproperty relationship in the opposite direction.

### 1.1.4. Notes on terminology of the DCAM and its relationship to RDF ###
The DCAM, described at http://dublincore.org/documents/abstract-model/ is illustrated graphically by Fig. 2 from section 2.2. of that web page:
![http://dublincore.org/documents/2007/06/04/abstract-model/description-set-model.jpg](http://dublincore.org/documents/2007/06/04/abstract-model/description-set-model.jpg)

The terms used in this diagram are defined in the section http://dublincore.org/documents/abstract-model/#sect-7.  Block arrows represent "is a" relationships in the direction of the arrows.  Block diamonds represent "has a" relationships away from the diamonds.

Although the DCAM is an abstract model, it was designed considering the structure of RDF and RDFS and is therefore easily translatable to RDF terms as described below.  The DCAM makes use of the term "value" to represent a physical entity, conceptual entity or literal associated with a property.  A "value" corresponds to a resource in RDF terms.  An object in an RDF triple corresponds approximately to a DCAM "value surrogate".  The value surrogate is the thing (literal string or URI) that represents the resource as opposed to the resource itself.  Value surrogates may be of two forms: literal value surrogates and non-literal value surrogates.

#### 1.1.4.1. Structure of DCAM literal value surrogates ####
If the object resource is a literal, the value surrogate is simply the string that encodes the value as shown in this diagram from section 4.7 of http://dublincore.org/documents/dc-rdf/#sect-4
![http://dublincore.org/documents/2008/01/14/dc-rdf/literalfig.png](http://dublincore.org/documents/2008/01/14/dc-rdf/literalfig.png)

#### 1.1.4.2. Structure of DCAM non-literal value surrogates ####
In the case of object resources which are non-literal, the Description Set Model of DCAM (section 2.2) says "A non-literal value surrogate is a value surrogate for a non-literal value, and is made up of zero or one value URI (a URI that identifies the non-literal value associated with the property), zero or one vocabulary encoding scheme URI (a URI that identifies the vocabulary encoding scheme of which the non-literal value is a member), and zero or more value strings. Each value string is a literal which represents the non-literal value."  Thus,the RDF representation of a non-literal value surrogate is far more complex than that of a literal value surrogate.  The structure of a non-literal value surrogate is shown in the following figure from section 4.3 of http://dublincore.org/documents/dc-rdf/#sect-4

![http://dublincore.org/documents/2008/01/14/dc-rdf/overviewfig.png](http://dublincore.org/documents/2008/01/14/dc-rdf/overviewfig.png)

From the point of view of the abstract model, a non-literal value surrogate technically includes several features shown in the above RDF diagram which lie beyond the object node of the triple which includes the property URI.  However, since these additional features are optional, one could consider the essential feature of the non-literal value surrogate to be the node itself.  Since the value URI is optional, that node may be a blank node.

#### 1.1.4.3. The value string of a non-literal value surrogate ####

The value string component requires further elaboration.  In an RDF representation of DCAM, the value string is the object of a triple using [rdf:value](http://www.w3.org/TR/rdf-schema/#ch_value) as the predicate.  The description of `rdf:value` at http://www.w3.org/TR/rdf-primer/#rdfvalue notes that `rdf:value` has no particular meaning other than as a convenience for creating structured values.  However, as the designated means for expressing the value string in the abstract model, DCMI has assigned meaning to `rdf:value` in the context of the DCAM.  The definition of non-literal value surrogate indicates that the value string **represents** the non-literal value (i.e. the resource).  The entirety of the documents related to the history behind the development of the `dcterms:` terms and the explanation of how the DCAM should be used to describe resources clarifies to some extent what it means for the value string to represent the resource.  This material suggests that object of the triple containing `rdf:value` is a string which would have been used as a surrogate for the resource itself in the pre-DCAM versions of Dublin Core.  This is perhaps best illustrated through the history of the use of `dc:creator` as described in [section 1.3.4.1.](#1.3.4.1._dcterms:creator_(AC;_range:_dcterms:Agent_).md) below.

The name of the term `rdf:value` should not be misinterpreted to infer that the string literal object of a triple containing `rdf:value` as the predicate must be the actual "value" of the subject of that triple.  In the case of a property/value pair where the property is `dcterms:rights` (which has the range `dcterms:RightsStatement`) the non-literal value surrogate could have a value string which actually is the "value" of the `dcterms:RightsStatement` instance itself, since a rights statement can be expressed as a string literal.  However, in the case of a property/value pair where the property is `dcterms:creator` (which has the range `dcterms:Agent`) the value string cannot be the actual "value" of the `dcterms:Agent` instance because that agent is a physical person, not a string.  However, from the section "Literal values of properties without Literal ranges" of http://dublincore.org/documents/dc-rdf-notes/#sect-3 , it is clear that DCMI intends for the object of the `rdf:value` triple to be a literal which is commonly used to stand in for the resource itself in databases where all entities are strings (as opposed to databases which can include non-information resources represented by URIs).

The use of `rdf:value` as an integral component of the RDF implementation of the DCAM model is somewhat problematic because like `rdf:Bag`, `rdf:Seq`, and `rdf:Alt` (components of RDF designed to allow construction of [structured "containers"](http://www.w3.org/TR/rdf-schema/#ch_containervocab)), `rdf:value` does not seem to be in widespread use.  However, since the DCAM model considers a value string optional and permits the non-literal value surrogate to be itself described by other property/value pairs, the `rdf:value` triple could simply be replaced by another triple containing a predicate which has a well-known meaning, such as `foaf:name` (see the examples of [section 1.3.4.1.](#1.3.4.1._dcterms:creator_(AC;_range:_dcterms:Agent_).md)).  Of course, also including the value string would not cause a problem - it would simply be a predicate of meaning unknown to clients who do not ascribe to it the special meaning imparted by DCMI (i.e. part of the DCAM value surrogate).

#### 1.1.4.4. The vocabulary encoding scheme URI of a non-literal value surrogate ####

In a manner similar to the value string, the vocabulary encoding scheme designation, which involves use of the `dcam:memberOf` predicate and which has a special place in the DCAM, may or may not have any special meaning to clients.  DCMI provides URIs for several well-known vocabulary encoding schemes at http://dublincore.org/documents/dcmi-terms/#H4 , however the lack of very many other defined URIs to use with this predicate might render the use of `dcam:memberOf` somewhat less useful than predicates such as `skos:inScheme` which may have broader implementation.  Of course, as with `rdf:value`, there would be no harm in providing a `dcam:memberOf` triple and having it simply be not understood by clients who do not ascribe to it the special meaning intended by the DCAM (i.e. part of the DCAM value surrogate).

A list of encoding schemes organized according to the terms whose values they interpret is at http://dublincore.org/documents/usageguide/qualifiers.shtml .

## 1.2. Implications of the domain, range, and subproperty declarations of terms in the `dcterms:` namespace ##

### 1.2.1. Literal and non-literal range declarations ###
The range declarations of the terms in the `dcterms:` namespace were intended by DCMI to indicate whether particular properties should be associated with literal values or with non-literal values.  The notes associated with the guidelines for expressing Dublin Core metadata as RDF clarify that the Dublin Core RDF encoding specification supports RDF triple patterns where the object is a string literal representing the resource and RDF triples where the object is a URI reference (or blank node) which identifies the resource as an entity, but "bases the choice of one form over the other on the range of a property. A property with a 'literal' range will follow the former pattern, while a property with a 'non-literal' range will follow the latter." (http://dublincore.org/documents/2008/01/14/dc-rdf-notes/#sect-3)

For example, the term `dcterms:bibliographicCitation` has the range [rdfs:Literal](http://www.w3.org/2000/01/rdf-schema#Literal).  Thus it is expected that the object of a triple using this property as a predicate would be a string literal.

Likewise DCMI does not intend for a term from `dcterms:` namespace which has a non-literal range in an RDF triple to have a literal object.  For example, it would not be appropriate to make the statement
```
http://dbpedia.org/resource/The_Starry_Night  dcterms:creator  "Vincent van Gogh"
```
because `dcterms:creator` has the range `dcterms:Agent` not `rdfs:Literal`.

The intention behind these range declarations is described at http://dublincore.org/usage/decisions/2010/dcterms-changes/ .  The suggestion is made that implementers who wish to use terms with the "wrong" kind of value could use the corresponding term in the `dc:` namespace (unencumbered by a range declaration) or coin their own term.

Despite the intentions declared by DCMI, there is nothing in the formal semantics of RDFS to prohibit a term in the `dcterms:` namespace from being used with the "wrong" type of object.  Since there is no real way to enforce the "correct" type of object, application programmers should be prepared to deal with metadata where the providers have used terms with types of objects that were not intended by DCMI.

### 1.2.2. Refinement and "Dumb-Down" ###
When the `dcterms:` namespace terms were created, a number of terms were designed to "refine" the original terms in the `dc:` namespace.  A "refined" term shares the meaning of the `dc:` term that it refines, but narrows the meaning and restricts the scope of the term.  "Refines" is a generic term for the relationship between a refined term and the term that it refines because the DCAM is a generic model.  When the DCAM is applied to RDF, the "refines" relationship becomes `rdfs:subPropertyOf` since every triple having the refined term as its predicate also implies a triple having the term it refines as the predicate.  The RDF definitions of `dcterms:` terms express "refines" relationships explicitly using `rdfs:subPropertyOf`.  A list of original Dublin Core terms and the terms that refine them are at http://dublincore.org/documents/usageguide/qualifiers.shtml .

There is an understanding that implementers may define their own terms which refine DCMI terms.  If an application does not "understand" a specialized refined term, it should be able to fall back on the broader meaning of the DCMI term which the specialized term refines.  This principle is known as the "Dumb-Down Principle".  In the context of RDF, the Dumb-Down Principle means that clients should be able to infer triples based on the subproperty relationships that are expressed in the refined term definitions.  The client should then be able to use the information contained in the inferred triples in lieu of "understanding" the specialized refined terms.  (See http://dublincore.org/documents/usageguide/qualifiers.shtml for an explanation of the Dumb-Down principle.)

## 1.3. Specific examples of expressing Dublin Core metadata using RDF ##
DCMI provides some explicit guidelines for how to express Dublin Core metadata in RDF at http://dublincore.org/documents/dc-rdf/#sect-4 .

The notes on the specifications for DCMI metadata in RDF, http://dublincore.org/documents/dc-rdf-notes/#sect-3 , note that in many cases "the appropriate range of a term has become reasonably obvious through a decade of implementation practice", although there has been inconsistency in the application of other terms.  In the following sections a number of Dublin Core terms that form part of existing or proposed TDWG standards which are drawn from Dublin Core are grouped according to the ranges defined by DCMI with notes and examples of how specific terms might be represented in RDF.

Note: the following generic RDF tag contains the namespace declarations necessary to test the example descriptions given here, e.g. using the [W3C RDF Validation Service](http://www.w3.org/RDF/Validator/) which generates graphical output or the [RDF Validator and Converter](http://www.rdfabout.com/demo/validator/) which will convert to N3/Turtle.
```
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:dctype="http://purl.org/dc/dcmitype/"
xmlns:dcam="http://purl.org/dc/dcam/"
xmlns:dwc="http://rs.tdwg.org/dwc/terms/"
xmlns:foaf="http://xmlns.com/foaf/0.1/"
xmlns:bibo="http://purl.org/ontology/bibo/"
xmlns:owl="http://www.w3.org/2002/07/owl#"
xmlns:xsd ="http://www.w3.org/2001/XMLSchema#"
>
(insert description here)
</rdf:RDF>
```

### 1.3.1. Dublin Core terms which have range `rdfs:Literal` ###
![http://dublincore.org/documents/2008/01/14/dc-rdf/literalfig.png](http://dublincore.org/documents/2008/01/14/dc-rdf/literalfig.png)

The RDF representation of terms having range `rdfs:Literal` is straightforward.  The Dublin Core property is the predicate and the literal value surrogate is the object.  The RDF literal object can be typed using an optional attribute within the predicate tag.  These include an optional XML language attribute ([xml:lang](http://www.w3.org/TR/REC-xml/#sec-lang-tag)), see http://www.ietf.org/rfc/rfc4646.txt ) or RDF datatype ([rdf:datatype](http://www.w3.org/TR/rdf-concepts/#section-Datatypes)).  Note: `xsd:` abbreviates `http://www.w3.org/2001/XMLSchema#`.  Presumably, any XML Schema defined datatypes ( http://www.w3.org/TR/xmlschema-2/ ) such as [xsd:dateTime](http://www.w3.org/TR/xmlschema-2/#dateTime) would be widely understood and appropriate for use with the `rdf:datatype` attribute.  The guidelines also specify that the `rdf:datatype` can be specified by reference to a "syntax encoding scheme URI".  Dublin Core defines URIs for a number of commonly used schemes at http://dublincore.org/documents/dcmi-terms/#H5 , however, from the examples given it seems expected that users may define their own syntax encoding scheme URIs.  It seems likely that only custom-designed consuming applications would know how to make use of this information.  [Section 1.3.4.5.](#1.3.4.5._dcterms:language_(AC,_DwC;_range:_dcterms:LinguisticSys.md) contains an example using a DCMI syntax encoding scheme URI.

Two of the terms used by TDWG are subproperties of [dcterms:date](http://dublincore.org/documents/dcmi-terms/#terms-date).  The Dublin Core definition of that terms states that best practice to use encoding scheme such as [W3CDTF profile of ISO 8601](http://www.w3.org/TR/NOTE-datetime).  This profile represents a restricted subset of formats allowed in ISO 8601.  The W3CDTF profile does not elaborate on how an adopting standard should specify which of the available options it permits.  As a practical matter, using one of the XML Schema datatypes follows the model given in the DCMI RDF guide.  There are two appropriate datatypes: [xsd:date](http://www.w3.org/TR/xmlschema-2/#date), which represents one-day intervals on the timeline and `xsd:dateTime` which represents a point on the timeline.  See http://www.w3.org/TR/xmlschema-2/#date and http://www.w3.org/TR/xmlschema-2/#dateTime for the distinction between these two datatypes.  Using `xsd:dateTime` would permit representing time to any degree of precision desired and in the interest of maximum flexibility might be preferred over `xsd:date` unless it were important to make the distinction that day-long intervals were intended rather than points in time.

### 1.3.2. Some terms in the `dcterms:` namespace which have literal ranges ###

The terms listed here are those that have been incorporated into the Darwin Core standard (DwC) and the Audubon Core draft standard (AC).  The hyperlinked term name links to the `dcterms:` definition, while the hyperlinked abbreviations link to the definition in the corresponding vocabulary.

#### 1.3.2.1. `dcterms:available` (AC) and `dcterms:modified` (DwC) ####
Both [dcterms:available](http://dublincore.org/documents/dcmi-terms/#terms-available) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:available))  and [dcterms:modified](http://dublincore.org/documents/dcmi-terms/#terms-modified) ([DwC](http://rs.tdwg.org/dwc/terms/index.htm#dcterms:modified)) are subproperties of [dcterms:date](http://dublincore.org/documents/dcmi-terms/#terms-date).  Therefore, use of [xsd:dateTime](http://www.w3.org/TR/xmlschema-2/#dateTime) would be appropriate as an RDF datatype URI as shown in the following examples.
```
<dctype:StillImage rdf:about="http://bioimages.vanderbilt.edu/baskauf/10849">
     <dcterms:available rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2010-11-28</dcterms:available>
</dctype:StillImage>
```

```
<foaf:Document rdf:about="http://bioimages.vanderbilt.edu/baskauf/10849.rdf">
     <dcterms:modified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2011-08-12T06:32:43</dcterms:modified>
</foaf:Document>
```

#### 1.3.2.2. `dcterms:bibliographicCitation` (DwC) ####
No guidance is provided for the specific use of [dcterms:bibliographicCitation](http://dublincore.org/documents/dcmi-terms/#terms-bibliographicCitation) ([DwC](http://rs.tdwg.org/dwc/terms/index.htm#dcterms:bibliographicCitation)), so presumably any text string would be acceptable as long as it is unambiguous.  Indicating the XML language attribute would be appropriate, particularly if the article title is presented in multiple languages.  Note: the domain of this term is declared to be [dcterms:BibliographicResource](http://dublincore.org/documents/dcmi-terms/#classes-BibliographicResource), so the object can be inferred to be an instance of this class even if it is not explicitly stated as it is in the following example.
```
<dcterms:BibliographicResource rdf:about="http://dx.doi.org/10.1525/auk.2009.09022">
     <dcterms:bibliographicCitation xml:lang="en">S. Claramunt, et al. 2009. Polyphyly of Campylorhamphus, and Description of a New Genus for C. pucherani (Dendrocolaptinae). The Awk 127(2):430-439.</dcterms:bibliographicCitation>
     <dcterms:bibliographicCitation xml:lang="es">S. Claramunt, et al. 2009. Polifilia de Campylorhamphus y la Descripción de un Nuevo Género para C. pucherani (Dendrocolaptinae). The Awk 127(2):430-439.</dcterms:bibliographicCitation>
</dcterms:BibliographicResource>
```

#### 1.3.2.3. `dcterms:title` (AC) ####
As with `dcterms:bibliographicCitation`, XML language attributes could be used to provide multiple versions of [dcterms:title](http://dublincore.org/documents/dcmi-terms/#terms-title) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:title)).
```
<dctype:StillImage rdf:about="http://bioimages.vanderbilt.edu/baskauf/10849">
     <dcterms:title xml:lang="en">Asimina triloba (Annonaceae) - inflorescence - frontal view of flower</dcterms:title>
     <dcterms:title xml:lang="fr">Asimina triloba (Annonaceae) - inflorescence - vue frontale de la fleur</dcterms:title>
</dctype:StillImage>
```

#### 1.3.2.4. `dcterms:identifier` (AC) ####
The definition of [dcterms:identifier](http://dublincore.org/documents/dcmi-terms/#terms-identifier) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:identifier)) is "An unambiguous reference to the resource within a given context."  There is no specified means for describing the context, but the "recommended best practice is to identify the resource by means of a string conforming to a formal identification system."  Thus this would seem to be a situation where using the `rdf:datatype` attribute might be useful if a URI exists for the formal identification system.

The identifier term is useful in the situation where a globally unique or well-known identifier which is not a URI exists for the resource.  For example, if a [UUID](http://tools.ietf.org/html/rfc4122) is used as a persistent text identifier, it can be specified using `dcterms:identifier` as in the following:
```
<rdf:Description rdf:about="urn:lsid:zoobank.org:act:3A9A7F78-C144-4220-B5AD-22BD0C10F0CD">
     <owl:sameAs rdf:resource="http://zoobank.org/urn:lsid:zoobank.org:act:3A9A7F78-C144-4220-B5AD-22BD0C10F0CD"/>
     <dcterms:identifier>3A9A7F78-C144-4220-B5AD-22BD0C10F0CD</dcterms:identifier>
     <rdfs:label>Turanena demirsoyi 2012</rdfs:label>
</rdf:Description>
```

In this example, the UUID assigned to the scientific name is the literal value of dcterms:identifier, while the LSID created from the UUID is the primary URI for the subject resource.  In accordance with the [TDWG LSID Applicability Statement Standard](http://www.tdwg.org/standards/150/), the HTTP-proxied form of the LSID is declared `owl:sameAs` the LSID.

Note: since a [URN namespace has been registered for UUIDs](http://www.iana.org/assignments/urn-namespaces/urn-namespaces.xml), it is possible to express a UUID as a URI.  In this case, the URI would be
```
urn:uuid:3a9a7f78-c144-4220-b5ad-22bd0c10f0cd
```
Note that the URI scheme designator "urn", the URN namespace identifier "uuid", and the UUID itself are all case insensitive.  However, it seems as though there is little benefit to proliferate the number of available URI identifiers for this resource by adding an additional URI when UUID URNs are not dereferenceable anyway.

Note that all [Darwin Core "ID" properties](http://rs.tdwg.org/dwc/terms/index.htm) (`institutionID, collectionID, datasetID, occurrenceID, individualID, eventID, locationID, higherGeographyID, geologicalContextID, identificationID, taxonID, scientificNameID, acceptedNameUsageID, parentNameUsageID, originalNameUsageID, nameAccordingToID, namePublishedInID, taxonConceptID, resourceRelationshipID, resourceID, relatedResourceID, measurementID` are declared to be subproperties of `dcterms:identifier`.  "When a property is a subproperty of another, then the domain and range classes of the first must be the domain and range of the second." (Y. Velegrakas, Semantic Web Information Management p. 50.)
Therefore, each of those ID properties inherit the range and domain properties of `dcterms:identifier`, in particular its range declaration of  `rdfs:Literal`.
For example, if
```
dwc:scientificNameID   rdfs:subPropertyOf   dcterms:identifier
```
and if
```
dcterms:identifier  rdfs:range  rdfs:Literal
```
then
```
dwc:scientificNameID  rdfs:range  rdfs:Literal
```

A statement such as
```
<dwc:Taxon rdf:about="http://bioimages.vanderbilt.edu/taxon/28754-gleason1991">
     <dwc:scientificName>Acer pensylvanicum L.</dwc:scientificName>
     <dwc:scientificNameID rdf:resource="http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:456229"/>
     <dwc:nameAccordingTo>Gleason, Henry A. and Arthur Cronquist, 1991. Manual of Vascular Plants of Northeastern United States and Adjacent Canada. The New York Botanical Garden, Bronx, NY, US.</dwc:scientificName>
     <dwc:nameAccordingToID rdf:resource="urn:isbn:0893273651"/>
</dwc:Taxon>
```
where the objects of the ID terms are URIs rather than a literals would be inconsistent with the DCMI guidelines for use of `dcterms:identifier`.  The following form would be consistent
```
<dwc:Taxon rdf:about="http://bioimages.vanderbilt.edu/taxon/28754-gleason1991">
     <dwc:scientificName>Acer pensylvanicum L.</dwc:scientificName>
     <dwc:scientificNameID>http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:456229</dwc:scientificNameID>
     <dwc:nameAccordingTo>Gleason, Henry A. and Arthur Cronquist, 1991. Manual of Vascular Plants of Northeastern United States and Adjacent Canada. The New York Botanical Garden, Bronx, NY, US.</dwc:scientificName>
     <dwc:nameAccordingToID>urn:isbn:0893273651</dwc:nameAccordingToID>
</dwc:Taxon>
```
although the benefit of this might be questionable since expressing an HTTP URI as a literal would not allow a client to "follow" the link.

### 1.3.3. Dublin Core terms which have non-literal ranges ###

See [section 1.1.4.](#1.1.4._Notes_on_terminology_of_the_DCAM_and_its_relationship_to.md) for a discussion of the structuring of non-literal value surrogates.

The guidelines for expressing Dublin Core in RDF note that the typed literals that represent value strings have exactly the same characteristics as literal value surrogates.  So the same attributes can be used with value strings (i.e. language tags, XML Schema datatype URIs, and syntax encoding scheme URIs).  See [section 1.3.1.](#1.3.1._Dublin_Core_terms_which_have_range_rdfs:Literal.md) for more information.

### 1.3.4. Some terms in the `dcterms:` namespace which have non-literal ranges ###
The terms listed here are those that have been incorporated into the Darwin Core standard (DwC) and the Audubon Core draft standard (AC).

#### 1.3.4.1. `dcterms:creator` (AC; range: `dcterms:Agent`) ####
The use of [dcterms:creator](http://dublincore.org/documents/dcmi-terms/#terms-creator) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:creator)) has been discussed extensively.  The most straightforward summary and the one which provides the clearest indication of how DCMI intends for the DCAM to apply in RDF is the section entitled "[Literal values of properties without Literal ranges](http://dublincore.org/documents/dc-rdf-notes/#sect-3)".  This approach is an attempt to fix years of confusion involving the use of the `dc:creator` term.  See http://wiki.foaf-project.org/w/UsingDublinCoreCreator for historical background.  The suggestion that FOAF create a term [foaf:maker](http://xmlns.com/foaf/spec/#term_maker) came to pass, and the point of view discussed in the historical FOAF document came to be accepted, namely that `foaf:maker` should have an object which represents the agent itself, while `dc:creator` could be used for textual names that stand for the creator.  Because the range of the "new" term `dcterms:creator` is [dcterms:Agent](http://dublincore.org/documents/dcmi-terms/#classes-Agent) rather than `rdfs:Literal`, it clearly should not be used with textual names.  There is a unique connection between DCMI and FOAF in that `dcterms:creator` and `foaf:maker` are declared to be related by an [owl:equivalentProperty](http://www.w3.org/TR/owl-ref/#equivalentProperty-def) relationship.

The section "Literal values of properties without Literal ranges" describes the use in RDF of `rdf:value` to express the name of the agent and this is consistent with the abstract DCAM's description of the optional value string which "is a literal which represents the non-literal value" of the non-literal value surrogate.  Under this model, one would say
```
<bibo:Webpage rdf:about="http://lod.taxonconcept.org/ses/dwAmr.html">
     <dcterms:creator>
          <foaf:Person rdf:about="http://lod.taxonconcept.org/ontology/people.owl#Peter_J_DeVries">
               <rdf:value>Peter J. DeVries</rdf:value>
          </foaf:Person>
     </dcterms:creator>
</bibo:Webpage>
```
However, given that use of `rdf:value` seems to be somewhat limited and that the value string is considered optional in the DCAM (see also the discussion in [section 1.1.4.3.](#1.1.4.3._The_value_string_of_a_non-literal_value_surrogate.md)), it may be desirable to express the agent's name using a well-known property like `foaf:name` instead of or in addition to `rdf:value`, e.g.
```
<bibo:Webpage rdf:about="http://lod.taxonconcept.org/ses/dwAmr.html">
     <dcterms:creator>
          <foaf:Person rdf:about="http://lod.taxonconcept.org/ontology/people.owl#Peter_J_DeVries">
               <foaf:name>Peter J. DeVries</foaf:name>
          </foaf:Person>
     </dcterms:creator>
</bibo:Webpage>
```

#### 1.3.4.2. `dcterms:rightsHolder` (DwC; range: `dcterms:Agent` ####

The use of the term [dcterms:rightsHolder](http://dublincore.org/documents/dcmi-terms/#terms-rightsHolder) ([DwC](http://rs.tdwg.org/dwc/terms/index.htm#dcterms:rightsHolder)) is straightforward.  As with `dcterms:creator`, the object of the triple could simply be the URI of a FOAF profile, or a description of the agent as in the previous example.
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/em2132">
     <dcterms:rightsHolder rdf:resource="http://bioimages.vanderbilt.edu/contact/kirchoff" />
</rdf:Description>
```

#### 1.3.4.3. `dcterms:type` (AC, DwC; range: `rdfs:Class`) ####

The recommended best practice for [dcterms:type](http://dublincore.org/documents/dcmi-terms/#terms-type) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:type)) ([DwC](http://rs.tdwg.org/dwc/terms/index.htm#dcterms:type)) is to use a controlled vocabulary such as the DCMI Type Vocabulary (http://dublincore.org/documents/dcmi-type-vocabulary/).  The DCMI Type Vocabulary terms are defined as instances of `rdfs:Class`, so using them with `dcterms:type` (which has a range of `rdfs:Class`) is appropriate.  The DCMI Type Vocabulary is a Vocabulary Encoding Scheme, so following the recommendation for expressing non-literal value surrogates can be accomplished as shown in the following example:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/16626">
     <dcterms:type>
          <rdf:Description rdf:about="http://purl.org/dc/dcmitype/StillImage">
               <dcam:memberOf rdf:resource="http://purl.org/dc/terms/DCMIType"/>
          </rdf:Description>
     </dcterms:type>
</rdf:Description>
```
However, the `dcam:memberOf` statement is actually redundant, since the defining RDF for terms in the DCMI Type Vocabulary (http://dublincore.org/2010/10/11/dctype.rdf) already include the statement `<dcam:memberOf rdf:resource="http://purl.org/dc/terms/DCMIType"/>` for each term.

There might be some utility in using a vocabulary encoding scheme URI and value string in cases where a term definition suggests recommended values but does not create URIs to identify them (i.e. necessitating a blank node for the object).  For example, Audubon Core recommends a value of "PanAndZoomImage" for use with `dcterms:type` but has not (at the present) defined a URI for it.  So one could say
```
<rdf:Description rdf:about="http://example.org/coolImage">
     <dcterms:type>
          <rdfs:Class>
               <dcam:memberOf rdf:resource="http://rs.tdwg.org/ac/terms"/>
               <rdf:value>PanAndZoomImage</rdf:value>
          </rdfs:Class>
     </dcterms:type>
</rdf:Description>
```
This essentially says that there is a class in Audubon Core not identified by a URI which has the value string "PanAndZoomImage".  The DCMI model allows this (i.e. zero value URI) but whether that is appropriate is debatable, and whether any client would be sophisticated enough to understand what it meant is not known.

A more succinct way of expressing this would be
```
<rdf:Description rdf:about="http://example.org/coolImage">
     <dcterms:type rdf:parseType="Resource">
          <dcam:memberOf rdf:resource="http://rs.tdwg.org/ac/terms"/>
          <rdf:value>PanAndZoomImage</rdf:value>
     </dcterms:type>
</rdf:Description>
```
which follows the syntax described at http://www.w3.org/TR/REC-rdf-syntax/#section-Syntax-parsetype-resource.  In this case, the `rdf:type` of the object of the `dcterms:type` triple (which is `rdfs:Class`) would have to be inferred from the range of `dcterms:type` since it is not explicitly stated.

**Special note about `dcterms:type`:**  Section 5.2. of http://dublincore.org/documents/dc-rdf/#sect-5 , says "It is recommended that RDF applications implementing this specification primarily use and understand `rdf:type` in place of `dcterms:type` when expressing Dublin Core metadata in RDF, as most RDF processors come with built-in knowledge of `rdf:type`."  Thus, although it may be desirable to include the property `dcterms:type` in the RDF description of a resource due to requirements such as the Audubon Core required terms designation (see http://species-id.net/wiki/Audubon_Core_Non_normative_document), terms in the `dctype:` namespace should be declared as a `rdf:type` property of the resource.

#### 1.3.4.4. `dcterms:rights` (AC, DwC; range: `dcterms:RightsStatement`) and `dcterms:accessRights` (DwC; range: `dcterms:RightsStatement`) ####

The definition of [dcterms:rights](http://dublincore.org/documents/dcmi-terms/#terms-rights) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:rights)) ([DwC](http://rs.tdwg.org/dwc/terms/index.htm#dcterms:rights)) notes that typically "rights information includes a statement about various property rights".  However, since the range of `dcterms:rights` is a non-literal value, it would not be appropriate given the DCMI RDF guidelines to simply provide a text statement as a literal object.  Here would be an option for expressing this property:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/em2132">
     <dcterms:rights>
          <dcterms:RightsStatement>
               <dcterms:created>2011</dcterms:created>
               <rdf:value>(c) 2011 Bruce K. Kirchoff</rdf:value>
          </dcterms:RightsStatement>
     </dcterms:rights>
</rdf:Description>
```

Following the model described in [section 1.3.4.3.](#1.3.4.3._dcterms:type_(AC,_DwC;_range:_rdfs:Class_).md), this could be written more succinctly as
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/em2132">
     <dcterms:rights rdf:parseType="Resource">
          <dcterms:created>2011</dcterms:created>
          <rdf:value>(c) 2011 Bruce K. Kirchoff</rdf:value>
     </dcterms:rights>
</rdf:Description>
```

Note that this creates a blank node for the `dcterms:RightsStatement` instance.

As is also the case with `dcterms:extent` ([section 1.3.4.8.](#1.3.4.8._dcterms:extent_(AC;_range:_dcterms:SizeOrDuration.md)) this level of complexity seems unnecessary if the metadata provider wants only to provide a simple text rights statement and is not interested in describing other properties of the rights statement.  Using `dc:rights` might be more appropriate when a simple literal value would suffice.  However, if the provider wishes to create more complex rights statements which are applicable to many resources, using `dcterms:RightsStatement` with a URI reference might be beneficial.

#### 1.3.4.5. `dcterms:language` (AC, DwC; range: `dcterms:LinguisticSystem`) ####

The comment listed in the definition of [dcterms:language](http://dublincore.org/documents/dcmi-terms/#terms-language) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:language)) ([DwC](http://rs.tdwg.org/dwc/terms/index.htm#dcterms:language)) says "Recommended best practice is to use a controlled vocabulary such as RFC 4646."  However, since RFC 4656 has been obsoleted by RFC 5646 it would be best to use the latter - although as a practical matter the tags are not going to differ in most instances.  Given that the range of is [dcterms:LinguisticSystem](http://dublincore.org/documents/dcmi-terms/#classes-LinguisticSystem) rather than `rdfs:literal`, it would not be appropriate under the DCMI RDF guidelines to simply provde  a string object which conforms to RFC 5646 in the form of an ISO639-1 (Alpha-2 code) or ISO639-2 (Alpha-3 code) tag (described at http://tools.ietf.org/html/rfc5646#section-2.2.1 ).

One option would be to provide no value URI (i.e. create a blank node) and simply provide the tag as a literal object of `rdf:value`.  However, there are a number of web pages on the topic of languages as RDF resources, including http://www.w3.org/wiki/Languages_as_RDF_Resources , http://www.lingvoj.org/ , and http://id.loc.gov/vocabulary/iso639-1.html which suggest URIs that can be used for languages.  What seems to be the most authoritative references are Library of Congress URIs of the form
```
http://id.loc.gov/vocabulary/iso639-1/en
```
(where the last two characters are the ISO 639-1 two-letter language code) or
```
http://id.loc.gov/vocabulary/iso639-2/eng
```
(where the last three characters are the ISO 639-2 three-letter language code).  These URIs dereference to RDF and HTML depending on the content-type requested.  The RDF metadata returned when the URIs are dereferenced declare a `skos:exactMatch ` relationship between the URIs which correspond to the two and three letter codes, provide a variety of labels identified using various SKOS label properties, and identify the actual ISO 639 string using the `skos:notation` property.  These metadata actually provide useful information that might be helpful in allowing a client to relate the 2 and 3 character tags if different kinds of tags were used by different data providers.

A possible way to represent the language property in RDF which would conform to the DCAM model and RDF guidelines might be:
```
<rdf:Description rdf:about="http://dx.doi.org/10.1525/auk.2009.09022">
     <dcterms:language>
          <dcterms:LinguisticSystem rdf:about="http://id.loc.gov/vocabulary/iso639-1/en">
               <dcam:memberOf rdf:resource= "http://id.loc.gov/vocabulary/iso639-1"/>
               <rdf:value rdf:datatype="http://purl.org/dc/terms/RFC5646">en</rdf:value>
          </dcterms:LinguisticSystem>
     </dcterms:language>
</rdf:Description>
```
In this RDF example `http://id.loc.gov/vocabulary/iso639-1/en` is declared explicitly to be an `dcterms:LinguisticSystem` instance, although that could be inferred implicitly from the range of `dcterms:language`.  It could be questioned whether `http://id.loc.gov/vocabulary/iso639-1/en` is actually an instance of a linguistic system or if it represents an instance of a **label** for a linguistic system.  The RDF types `http://id.loc.gov/vocabulary/iso639-1/en` as "http://www.loc.gov/mads/rdf/v1#Authority" which is "A concept with a controlled label." and also as an `skos:Concept` so it is clearly a concept of something if not a concept of the language English.  To some extent this question may be moot since the URI gets the job done (i.e. identifies the intended language, provides labels for it, and connects equivalent labels).

The `rdf:datatype` attribute of `http://purl.org/dc/terms/RFC5646` used with the value string is a DCMI-created syntax encoding scheme URI for RFC 5646. See http://tools.ietf.org/html/rfc5646 which explains the relationship between RFC 5646 and ISO 639-2 / ISO 639-3 (http://www.loc.gov/standards/iso639-2/langhome.html and http://www.sil.org/iso639-3/) which have their own DCMI syntax encoding scheme URIs (`http://purl.org/dc/terms/ISO639-2` and `http://purl.org/dc/terms/ISO639-3`).

In the example, the object of the triple containing `dcam:memberOf` declares `http://id.loc.gov/vocabulary/iso639-1` to be a `dcam:VocabularyEncodingScheme` ("An enumerated set of resources.").  One could argue about whether `http://id.loc.gov/vocabulary/iso639-1/en` is actually a member of any coding scheme, since it seems to represent the language English, not a code for English.  However, this could be said for any resource which is described using the DCAM - it's actually the literal object of `rdf:value` that is part of the coding scheme, not the actual subject of `dcam:memberOf`.  That just seems to be the way DCAM works.  Since the RDF describing `http://id.loc.gov/vocabulary/iso639-1` declares it to be both an instance of `skos:ConceptScheme` and `http://www.loc.gov/mads/rdf/v1#MADSScheme`, then it is reasonable to consider `http://id.loc.gov/vocabulary/iso639-1` to be a `dcam:VocabularyEncodingScheme` as well.

#### 1.3.4.6. `dcterms:temporal` (AC; range: `dcterms:PeriodOfTime`) ####
[dcterms:temporal](http://dublincore.org/documents/dcmi-terms/#terms-temporal) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:temporal)) is a problematic term, defined as "temporal characteristics of the resource."  The definition of the class `dcterms:PeriodOfTime` is "An interval of time that is named or defined by its start and end dates", yet under the DCMI RDF guidelines, this should not be expressed as a `rdfs:Literal` since the object of `dcterms:temporal` is declared by DCMI to be a non-literal value.

[ISO 8601](http://en.wikipedia.org/wiki/ISO_8601#Time_intervals) allows the expression of time intervals by specifying the dateTime instances of the beginning and end of the interval separated by a solidus (forward slash).  This is not supported in the more narrowly defined [W3C Date and Time Format note](http://www.w3.org/TR/NOTE-datetime) which is based on ISO 8601.  Although there is a Syntax Encoding Scheme URI defined by DCMI for the W3C Date and Time Format ( http://purl.org/dc/terms/W3CDTF ), it cannot be used as a `rdf:datatype` attribute in this case because of the lack of support in the W3C DTF of dateTime ranges.  The [xsd:dateTime](http://www.w3.org/TR/xmlschema-2/#dateTime) datatype, which is also based on ISO 8601 does not support date ranges either.  DCMI defines its own [Period Encoding Scheme](http://dublincore.org/documents/dcmi-period/) (URI: `http://purl.org/dc/terms/Period`).  However, in a review of the legacy DCSV syntax ( http://dublincore.org/usage/decisions/2006/2006-01.DCSV-revisions.html ), DCMI encouraged implementers to consider using "related descriptions" (see http://dublincore.org/groups/agents/AgentsWG_MeetingReport.doc for a vague description of what a "related description" is - apparently just referencing URIs of related resources) rather than DCSV syntax.  This effectively depricated the DCMI Period Encoding Scheme.  So we are left with little guidance from DCMI about how to encode a period of time.

Audubon Core allows just about anything as a string value for `dcterms:temporal`:

"The coverage (extent or scope) of the content of the resource. Temporal coverage will typically include temporal period (a period label, date, or date range) to which the subjects of the media or media collection relate."

with examples
```
"Jurassic", "Elizabethan", "Spring, 1957". 2008-01-01/2008-06-30
```
The absence of either a corresponding `dc:` term which is suitable for a simple string literal object, or a well-known set of properties for describing a non-literal `dcterms:PeriodOfTime` instance leaves few options for a simple RDF description using the `temporal` property.  The following example would be consistent with the DCAM:
```
<dctype:MovingImage rdf:about="http://dbpedia.org/resource/Gone_with_the_Wind_(film)">
     <dcterms:temporal>
          <dcterms:PeriodOfTime>
	     <rdf:value>1861/1868</rdf:value>
          </dcterms:PeriodOfTime>
     </dcterms:temporal>
</dctype:MovingImage>
```
but introduces a blank node and unnecessary complexity for what could otherwise be expressed simply as a literal object.

#### 1.3.4.7. `dcterms:format` (AC; range: `dcterms:MediaTypeOrExtent`) ####
The following diagram is Fig. 2 from the webpage [Domains and Ranges for DCMI Properties](http://dublincore.org/documents/domain-range/):
![http://dublincore.org/documents/2007/07/02/domain-range/format-classes.jpg](http://dublincore.org/documents/2007/07/02/domain-range/format-classes.jpg)

This diagram shows that the property [dcterms:format](http://dublincore.org/documents/dcmi-terms/#terms-format) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:format)) is part of the complex group of property/class relationships defined by Dublin Core.   It has a rather broad definition: "the file format, physical medium, or dimensions of the resource" with the recommended best practice of using "a controlled vocabulary such as the list of Internet Media Types" (i.e. MIME types).  The following example illustrates how a format could be specified in terms of the Internet Media Type.

```
<dctype:Text rdf:about="http://example.org/document.html">
     <dcterms:format>
          <dcterms:MediaTypeOrExtent>
               <dcam:memberOf rdf:resource="http://purl.org/dc/terms/IMT"/>
               <rdf:value>text/html</rdf:value>
          </dcterms:MediaTypeOrExtent>
     </dcterms:format>
</dctype:Text>
```
Note that this introduces a blank node in the absence of a well-recognized URI for media types.  DCMI defines a URI for the Internet Media Type vocabulary encoding scheme but it is not clear how to indicate other format description systems such as file extensions like `.jpg`, `.gif`, etc.

Again, as was done in [section 1.3.4.3.](#1.3.4.3._dcterms:type_(AC,_DwC;_range:_rdfs:Class_).md), the RDF could be written more succinctly as:
```
<dctype:Text rdf:about="http://example.org/document.html">
     <dcterms:format rdf:parseType="Resource">
          <dcam:memberOf rdf:resource="http://purl.org/dc/terms/IMT"/>
          <rdf:value>text/html</rdf:value>
     </dcterms:format>
</dctype:Text>
```
Alternatively, the term `dc:format` could be used with a literal object.

#### 1.3.4.8. `dcterms:extent` (AC; range: `dcterms:SizeOrDuration`) ####

[dcterms:extent](http://dublincore.org/documents/dcmi-terms/#terms-extent) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:extent)) is defined as "the size or duration of the resource."  Little guidance is given about how to specify the units or encoding scheme.

```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/04005#tn">
     <dcterms:extent>
          <dcterms:SizeOrDuration>
               <rdf:value>70 x 100 px</rdf:value>
          </dcterms:SizeOrDuration>
     </dcterms:extent>
</rdf:Description>
```

Note: `dcterms:extent` is a subproperty of `dcterms:format` while `dcterms:SizeOrDuration` is a subclass of `dcterms:MediaTypeOrExtent`.  So the description above also would imply the following:

```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/04005#tn">
     <dcterms:format>
          <dcterms:MediaTypeOrExtent>
               <rdf:value>70 x 100 px</rdf:value>
          </dcterms:MediaTypeOrExtent>
     </dcterms:format>
</rdf:Description>
```
As in [section 1.3.4.3.](#1.3.4.3._dcterms:type_(AC,_DwC;_range:_rdfs:Class_).md), the RDF could be written more succinctly as:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/04005#tn">
     <dcterms:extent rdf:parseType="Resource">
          <rdf:value>70 x 100 px</rdf:value>
     </dcterms:extent>
</rdf:Description>
```

An advantage of providing a value string as shown in the examples above is that it would allow the same property (`dcterms:extent`)to describe the format of a wide variety of media (e.g. pixel dimensions for an image, length in seconds for a video,number of pages for a print book, etc.)  However, given the lack of a standardized syntax encoding scheme or vocabulary encoding scheme, clients would have little guidance in interpreting the value.

The strategy of utilizing terms with specific kinds of literal objects (discussed in the last paragraph of [section 4.4](http://www.w3.org/TR/rdf-primer/#rdfvalue) of the RDF Primer) having defined units may be more beneficial than the generic `dcterms:extent` if the metadata provider wants to provide clarity on how to interpret the provided. In the following example
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/04005#tn">
     <mix:imageWidth>70</mix:imageWidth>
     <mix:imageHeight>100</mix:imageHeight>
</rdf:Description>
```
a consuming application which is aware of the `mix:` properties will "know" that these properties are defined to refer to a number of pixels.  The following modification

```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/04005#tn">
     <mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">70</mix:imageWidth>
     <mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">100</mix:imageHeight>
</rdf:Description>
```
would provide additional clarity to consuming applications about the nature of the values.

### 1.3.5. Dublin Core terms having no declared range ###
There are a number of terms in the in the `dcterms:` namespace which do not have a declared range, but whose metadata notes "This term is intended to be used with non-literal values as defined in the DCMI Abstract Model (http://dublincore.org/documents/abstract-model/).  As of December 2007, the DCMI Usage Board is seeking a way to express this intention with a formal range declaration."  As of February 2012, these terms still do not have formal `rdfs:range` declarations.  To be consistent with the expressed intent of DCMI, it would seem to be best to use them with non-literal objects and to use the corresponding terms in the `dc:` namespace (if available) for literal objects (see [section 1.3.7.](#1.3.7._Achieving_consistency_with_DCMI_guidelines_by_using_terms.md)).

### 1.3.6. Some terms in the `dcterms:` namespace having no declared range ###

#### 1.3.6.1. `dcterms:references` (DwC; intended to be used with non-literal values) ####
The term [dcterms:references](http://dublincore.org/documents/dcmi-terms/#terms-references) ([DwC](http://rs.tdwg.org/dwc/terms/index.htm#dcterms:references)) is defined as "a related resource that is referenced, cited, or otherwise pointed to by the described resource."  It is also declared to be a subproperty of `dcterms:relation`.  It has no corresponding term in the `dc:` namespace, so there is no appropriate way to use a literal with this term.  `dcterms:references` is a subproperty of `dc:relation` which could have a literal object.  So it would be possible to use `dc:relation` as a substitute for which a literal value would be appropriate.  However, `dc:relation` does not indication the direction of the relationship and its use would therefore make it difficult to distinguish the type of relationship from `dcterms:isReferencedBy` which is apparently (but not declared formally in the RDF to be) an inverse property of `dcterms:references`, and which is also a subproperty of `dc:relation`.

#### 1.3.6.2.  `dcterms:source` (AC; intended to be used with non-literal values) ####
The term [dcterms:source](http://dublincore.org/documents/dcmi-terms/#terms-source) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:source)) is defined as "a related resource from which the described resource is derived."  It is also declared to be a subproperty of `dcterms:relation`.  In this case, the term `dc:source` could be used of the user preferred to provide a literal rather than a non-literal value.

#### 1.3.6.3. `dcterms:description` (AC; no indication given whether the value should be literal or non-literal) ####
The lack of a range declaration for [dcterms:description](http://dublincore.org/documents/dcmi-terms/#terms-description) ([AC](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:description)) and the comment that it may include "a free-text account of the resource" indicates that it could be appropriate to use this term with a literal value.  However, since it is possible that some users might want to link to a description which is a separate resource under its own URI, it might be a better practice to reserve `dcterms:description` for use with non-literal objects and to use `dc:description` for use with literal objects.

### 1.3.7. Achieving consistency with DCMI guidelines by using terms in the `dc:` namespace ###
If one preferred to use literal value surrogates, the corresponding terms in the `dc:` namespace could be used rather than the terms in the `dcterms:`namespace.  For example:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/em2132">
     <dc:rights>(c) 2011 Bruce K. Kirchoff</dc:rights>
     <dc:type>StillImage</dc:type>
</rdf:Description>
```
Because the `dc:` terms have no defined ranges, this example is consistent with the intent of DCMI as expressed in ["Literal values of properties without Literal ranges"](http://dublincore.org/documents/2008/01/14/dc-rdf-notes/#sect-3).  It could be a suitable alternative in cases such as Audubon Core which (in [draft form as of 2012-03-24](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:rights)) explicitly states that `dcterms:rights` should be a "full-text, readable copyright statement", given that `dc:rights` is a superproperty of `dcterms:rights`.  Whether clients would be able to interpret these `dc:` statements more easily than the examples in [section 1.3.4.](#1.3.4._Some_terms_in_the_dcterms:_namespace_which_have_non-liter.md) or not is unknown.

It is also possible to provide descriptions of a resource using both literal (using `dc:` terms) and non-literal (using `dcterms:`) versions of a term:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/em2132">
     <rdf:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>
     <dc:rights>(c) 2011 Bruce K. Kirchoff</dc:rights>
     <dcterms:rights>
          <dcterms:RightsStatement>
               <dcterms:created>2011</dcterms:created>
               <rdf:value>(c) 2011 Bruce K. Kirchoff</rdf:value>
          </dcterms:RightsStatement>
     </dcterms:rights>
     <dc:type>StillImage</dc:type>
     <dcterms:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>
</rdf:Description>
```
Since the Dublin Core type vocabulary is well known, there might be some advantage to using `dctype:StillImage` as the non-literal object of `dcterms:type` rather than simply providing a text literal object of `dc:type`.  However, it may be questionable as to whether there is a benefit to providing a non-literal object to `dcterms:rights` when that object is not identified by a URI (i.e. a blank node) and is therefore not likely to be reused or referenced by others.  Unless there is a need to describe the conceptual entity using other properties (e.g. to indicate creation date, authorship, etc.) there seems to be little benefit over simply relaying the information in the form of a literal.

### 1.3.8. `dc:` counterparts for Dublin Core terms used in the TDWG community ###
The following terms in the `dcterms:` namespace have  superproperties in the `dc:` namespace and could therefore be used in the manner suggested in the previous section: `creator`, `type`, ` rights`, `language`, and `format`.

The following terms in the `dcterms:` namespace do not have counterparts in the `dc:`namespace:  `rightsHolder`, `accessRights`, `temporal`, and `extent`.  The strategy outlined in the previous section could not be applied to them.

# 2. Implications of Dublin Core RDF Guidelines for the TDWG vocabularies #

This section addresses the question of the extent to which the DCMI guidelines dictate how the Dublin Core terms should be applied and interpreted in other vocabularies that adopt them.

## 2.1. Description of the models which underlie TDWG vocabularies ##
Both Darwin Core and Audubon Core include terms that are defined as DCMI metadata terms.  Each of these TDWG vocabularies provides guidelines for how its terms can be applied by users in particular situations (e.g. as fielded text or XML).

Audubon Core states clearly that it intends for its terminology to be "flat" and that the specification is independent of how the vocabulary may be represented for machine use (see http://species-id.net/wiki/Audubon_Core_Non_normative_document and http://species-id.net/wiki/Audubon_Core#Multiplicity ).  Thus Audubon Core seeks to escape complications which would result from being wedded to a complex and highly normalized data structure which might be demanded by a particular encoding system.

Likewise, Darwin Core provides guidelines for creating "Simple Darwin Core" records which are completely "flat" ( http://rs.tdwg.org/dwc/terms/simple/index.htm ) as well as an XML guide ( http://rs.tdwg.org/dwc/terms/guides/xml/index.htm ).  An underlying syntax-neutral abstract metadata model is also described at http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#abstractmodel .

The DCAM guidelines http://dublincore.org/documents/abstract-model/#sect-6 specify that guidelines for particular encodings of Dublin Core terms do not need to incorporate all aspects of the DCAM, but they should refer to the DCAM and indicate which parts are encoded and which are not.  In particular, they should indicate how non-literal values can be treated as a described resource when these values don't have a URI.

In the case of Audubon Core, the current draft (as of 2012-02-25) states at http://species-id.net/wiki/Audubon_Core that "we will follow closely (sometimes verbatim) a portion of the Dublin Core Metadata Initiative (DCMI) metadata nomenclature as described in Section 2.3 of the DCMI Abstract Model" ( dublincore.org/documents/abstract-model/#sect-2 ).  Section 2.3 describes the basic terminology of the DCAM in terms of properties and classes and property/value pairs.  It also lays out how properties are related to classes through range and domain relationships.

The Darwin Core abstract model "follows the Dublin Core Metadata Initiative Abstract Model [ABSTRACTMODEL](http://dublincore.org/documents/abstract-model/) except that the Darwin Core record is roughly equivalent to the Dublin Core resource."

So both Audubon Core and Darwin Core claim that their underlying models follow the DCAM to some extent. They accept the idea of property/value pairs and some loose aspects of class organization, but do not reference any range or domain restrictions that would force class membership through the use of particular properties.  For simple text-based representations (e.g. CSV) this is fine because no complex relationships are implied or required.

## 2.2. Problems with adaptation of TDWG vocabularies for use in RDF ##
If the Audubon Core and Darwin Core vocabulary terms are used as RDF predicates, the property/class associations declared for the "adopted" Dublin Core terms should not be ignored.  Section 5.1 of the RDF guidelines for Dublin Core, http://dublincore.org/documents/dc-rdf/#sect-5 , state "The RDF expression of the DCMI Abstract Model has a special status among the DCMI encoding specifications. As the semantics of the notions DCMI Abstract Model is based on the semantics of the corresponding notions in RDF (as defined by [RDF-SEMANTICS](http://www.w3.org/TR/rdf-mt/)), it is of fundamental importance that the RDF expression preserves any semantics of the DCAM. Also, any valid inferences that can be made using RDF semantics need to be valid when interpreted in terms of the DCMI Abstract Model."

So adoption of the DCMI metadata terms comes with the responsibility to use them in accordance with the semantics ascribed to them by their definitions relative to the DCAM.  This causes a problem when the described application of a DCMI term within a TDWG vocabulary conflicts with the range declared for that term in the Dublin Core term definition, i.e. if a TDWG vocabulary description states that the value should be text where Dublin Core defines a non-literal range, or where the TDWG vocabulary implies that the value should be a URI (presumably capable of being a non-literal value surrogate URI) where Dublin Core defines a literal range.

## 2.3. Possible courses of action where TDWG vocabularies suggest using literal objects with DCMI terms having non-literal ranges ##

In some instances, TDWG definitions for DCMI terms specify that values should be text (or at least don't prohibit text) for terms that have non-literal ranges.  The following are several options to avoid the inconsistencies with the DCMI RDF guidelines that this may cause when metadata are converted to RDF.

### 2.3.1. Change the namespaces of problematic DCMI terms from `dcterms:` to `dc:` wherever possible ###
The terms `creator`, `type`, ` rights`, `language`, and `format` which have non-literal ranges in the `dcterms:` namespace have corresponding `dc:` terms which do not have range declarations.  This could be considered semantically consistent if the term namespaces were simply changed, since each `dcterms:` term is `rdfs:subPropertyOf` the corresponding `dc:` term. So any preexisting statement of
```
subjectResource  dcterm:term  "literalValue"
```
automatically implies the new (consistent with DCMI RDF guidelines) term relationship
```
subjectResource  dc:term  "literalValue"
```
From the standpoint of text-based records, there might be no problem since the only change required would be changing the field name string in the database.  From the standpoint of XML based records, things would be badly broken since the system would not see `dcterm:term` as the same thing as `dc:term`.  In addition to the problem of "breaking" things, this would also require changes to the terms through the DwC Namespace Policy, which could take eons.

The terms `rightsHolder`, `accessRights`, `temporal`, and `extent` in the `dcterms:` namespace do not have corresponding `dc:` namespace counterparts.  However, only `rightsHolder` and `accessRights` are used by Darwin Core.  Since Audubon Core is not yet adopted, alternatives to `dcterms:temporal` and `dcterms:extent` could be found or perhaps created as a literal analogue within the Audubon Core namespace (i.e. `ac:temporal` and `ac:extent`.  Since `dcterms:rightsHolder` and `dcterms:accessRights` are related to intellectual property issues, which are not the major focus of Darwin Core, it is possible that they are not in wide-enough use that changing their term URIs to `dwc:rightsHolder` and `dwc:accessRights` would cause much of a problem.

### 2.3.2. Declare a `dc:` conversion of problematic DCMI terms as a Best Practice for converting TDWG metadata to RDF ###
Under this scenario, one would simply not attempt to "fix" term URIs in existing text- or XML- based records.  Instead, declare it a Best Practice to map all `creator`, `type`, ` rights`, `language`, and `format` property/value pairs in DwC records from `dcterms:` to `dc:` when converting to an RDF representation.  Again, since Audubon Core is still a draft standard, this problem could be avoided before adoption by changing the term URIs to the `dc:` namespace.

This would not fix the problem for `dcterms:rightsHolder` and `dcterms:accessRights`.  However, it would be possible to declare new DwC terms `dwc:rightsHolder` and `dwc:accessRights` (with no range declarations) for use in RDF and specify in that an equivalent mapping be made to those terms during RDF conversion.

### 2.3.3. Express the literal values of problematic Dublin Core terms as `rdf:value` properties of a blank node ###
An alternative that would be valid and consistent with the DCAM would be to leave the term URIs as they are and when converting to RDF let the text values form the literal objects of an `rdf:value` (see [section 1.1.4.3.](#1.1.4.3._The_value_string_of_a_non-literal_value_surrogate.md)).  For example:

Database:
|GUID|dcterms:rights|dcterms:format|
|:---|:-------------|:-------------|
|http://bioimages.vanderbilt.edu/baskauf/15313#bq|(c) 2002 Steven J. Baskauf|image/jpeg    |
|http://bioimages.vanderbilt.edu/kirchoff/ac1501#bq|(c) 2011 Bruce K. Kirchoff|image/gif     |

RDF model 1 based on DCAM:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/15313#bq">
     <dcterms:rights>
          <dcterms:RightsStatement>
               <rdf:value>(c) 2002 Steven J. Baskauf</rdf:value>
          </dcterms:RightsStatement>
     </dcterms:rights>
     <dcterms:format>
          <dcterms:MediaTypeOrExtent>
               <dcam:memberOf rdf:resource="http://purl.org/dc/terms/IMT"/>
               <rdf:value>image/jpeg</rdf:value>
          </dcterms:MediaTypeOrExtent>
     </dcterms:format>
</rdf:Description>
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/ac1501#bq">
     <dcterms:rights>
          <dcterms:RightsStatement>
               <rdf:value>(c) 2011 Bruce K. Kirchoff</rdf:value>
          </dcterms:RightsStatement>
     </dcterms:rights>
     <dcterms:format>
          <dcterms:MediaTypeOrExtent>
               <dcam:memberOf rdf:resource="http://purl.org/dc/terms/IMT"/>
               <rdf:value>image/gif</rdf:value>
          </dcterms:MediaTypeOrExtent>
     </dcterms:format>
<</rdf:Description>
```
as opposed to a much simpler and less verbose RDF model 2 based on conversion to `dc:` terms:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/15313#bq">
     <dc:rights>(c) 2002 Steven J. Baskauf</dc:rights>
     <dc:format>image/jpeg</dc:format>
</rdf:Description>
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/kirchoff/ac1501#bq">
     <dc:rights>(c) 2011 Bruce K. Kirchoff</dc:rights>
     <dc:format>image/gif</dc:format>
<</rdf:Description>
```

A SPARQL query under model 1 could be:
```
SELECT DISTINCT ?image WHERE {
 ?image dcterms:format?x.
 ?x rdf:value "image/gif".
}
```
vs.
```
SELECT DISTINCT ?image WHERE {
 ?image dc:format "image/gif".
}
```
under model 2.  In addition to being simpler, model 2 does not require people performing queries to think of the possibility that someone might be using the `rdf:value` property.

### 2.3.4. Find alternative properties in other vocabularies ###
Use terms from other vocabularies that are equivalent to the ones which can't be used with literals.  This strategy would be contingent on such properties actually existing.

### 2.3.5. Tell people they can't convert those property values to RDF ###
Dumb idea but still one of the options.

### 2.3.6. Do nothing and use the `dcterms:` terms in a manner inconsistent with DCMI RDF guidelines ###
Under this scenario, people just use `dcterm:` properties which have non-literal ranges to create triples with literal objects.  This would have the advantage of being the easiest solution given that it would require no changes or additions to any TDWG standard and wouldn't "break" anything that anyone has done so far.  Most validators would not complain and "dumb" applications (i.e. simple SPARQL queries) would never know the difference.  On the negative side, this would place an additional burden on application programmers who would have to assume that some people would be using the terms consistently with the DCMI guidelines and that some people might not.  But that would probably be a wise course of action anyway.  See the discussion at https://groups.google.com/d/topic/tdwg-rdf/GQ9zoMC9RF0/discussion and https://groups.google.com/d/topic/tdwg-rdf/h2Sq5nu7Ja8/discussion for more on this topic.

## 2.4. Possible courses of action where users may be inclined to use terms having literal ranges with non-literal objects ##

[Audubon Core](http://species-id.net/wiki/Audubon_Core_Term_List#dcterms:identifier) suggests using `dcterms:identifier` with URIs (i.e. "http-URL, and lsid-URI") that are typically used as URI references in RDF.  There isn't necessarily any problem with this as long as metadata providers understand that this requires expressing the identifiers as literals:
```
<dcterms:identifier>urn:lsid:biocol.org:col:15574</dcterms:identifier>
```
rather than
```
<dcterms:identifier rdf:resource="urn:lsid:biocol.org:col:15574"/>
```
if the intent of the DCMI RDF guidelines are to be followed.

In the RDF definitions of the DwC ID terms, they are declared to be `rdfs:subPropertyOf dcterms:identifier` which has a range of `rdfs:Literal`.  See [section 1.3.2.4.](#1.3.2.4._dcterms:identifier_(AC).md) for more details.

### 2.4.1. Remove subproperty declarations for DwC ID terms ###
The most straightforward solution would be to remove the subproperty declarations for all of the "ID" terms.  However, this would require going through the term change process for DwC which is long and time-consuming.

### 2.4.2. Don't use the ID terms in RDF ###
This may be the preferred solution.  In the example shown at http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#classes the term `dwc:locationID` is used both as in indication of the identifier of the subject Location resource `http://guid.mvz.org/sites/arg/127`, but also as an ID reference to the Location as an object of a property of the Occurrence.  The `dwc:occurrenceID` is similarly used in both ways.  If it is unclear how the ID terms are to be used, it might be better to create new terms that are not ambiguous (the approach taken by [Darwin-SW](http://code.google.com/p/darwin-sw/)).