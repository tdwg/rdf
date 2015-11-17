[return to list of usage notes](UsageNotes.md)

<h1>Usage Note: Terms in the <code>dcterms:</code> namespace</h1>

**Date:** (Created) 2012-02-17; (Last modified) 2012-03-24

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Table of Contents**


# 1. Issue description #
Many Dublin Core terms in the namespace `http://purl.org/dc/terms/` (`dcterms:`) have been defined by DCMI (Dublin Core Metadata Initiative) to have ranges which are either `rdfs:Literal` or a specific non-literal class.  There is an expectation that when these terms are used in RDF that the resulting RDF will follow particular patterns, in contrast to Dublin Core terms in the `http://purl.org/dc/elements/1.1/` (`dc:`) namespace which do not have defined ranges.

A more in-depth discussion of this issue is at the page [Dublin Core in RDF](DublinCore.md).

# 2. Background #
Historically, some terms in the legacy (`dc:`) Dublin Core namespace (1) have been used with literals which were intended to represent a non-information resource.  For example, the name of the creator of a resource is often given for the term `dc:creator`.  As best-practices for creating machine-processable metadata developed, the use of `dc:` terms was inconsistent, with some implementers using those terms to represent the name of the entity and others using it to represent the entity itself. (2)

The DCMI Abstract Model (DCAM) was developed to formalize components used in Dublin Core metadata and it described how those components are combined to create information structures. (3)  In the DCAM, the object resource of a property is called a "value".  Values are broken down into two categories.  _Literal values_ are encoded by string literals and _non-literal values_ are physical, digital or conceptual entities which may be identified by URIs.  The guidelines for "Expressing Dublin Core metadata using the Resource Description Framework (RDF)" describe how the abstract DCAM should be expressed as RDF. (4)  The notes associated with those guidelines for expressing Dublin Core metadata as RDF clarify that the Dublin Core RDF encoding specification supports RDF triple patterns where the object is a string literal representing the resource and RDF triples where the object is a URI reference (or blank node) which identifies the resource as an entity, but "bases the choice of one form over the other on the range of a property. A property with a 'literal' range will follow the former pattern, while a property with a 'non-literal' range will follow the latter." (5)  Terms in the `dcterms:` namespace (6) were in some cases assigned ranges that were `rdfs:Literal` (7) or a non-literal Dublin Core class, and in other cases declared to be intended to be used with non-literal values that were instances of unspecified classes. (8)  Terms in the `dc:` namespace were left without a specified range, so using any `dc:` term with a literal object would be appropriate under the DCMI guidelines.

# 3. Notes for metadata consumers #
Although the human-readable guidelines for expressing terms in the `dcterms:` namespace in RDF specify that terms with non-literal ranges should have objects that are URI references (or blank nodes), nothing in the formal semantics of RDF requires that the class `rdfs:Literal` be disjoint from other classes whose instances are typically represented by URI references.(9)  Thus if a metadata provider specifies a literal object for a term from the `dcterms:` namespace having a non-literal range, the object will simply be implied to have `rdf:type` which is the class in the range declaration. (10)

Because there are few (if any) mechanisms to enforce the DCMI guidelines which suggest whether literals should or should not be used with particular terms, application programmers and metadata aggregators should be prepared to deal with RDF which does not follow those guidelines.

# 4. Some terms in the `dcterms:` namespace which have declared literal ranges and usage examples #
```
dcterms:available
dcterms:modified
dcterms:bibliographicCitation
dcterms:title
dcterms:identifier
```
Note: these examples refer to "real" subject resources and the statements made by the triples are generally true.  However, the RDF associated with the example subject resources may not actually contain the triples given in the examples.

## 4.1. Example of plain literals with language tags ##
![http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-title.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-title.png)

**Note:** a literal cannot simultaneously have a language tag and a datatype.
### RDF/XML ###
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF 
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dcterms="http://purl.org/dc/terms/"
>
  <rdf:Description rdf:about="http://dx.doi.org/10.1525/auk.2009.09022">
     <dcterms:title xml:lang="en">Polyphyly of Campylorhamphus, and Description of a New Genus for C. pucherani (Dendrocolaptinae)</dcterms:title>
     <dcterms:title xml:lang="es">Polifilia de Campylorhamphus y la Descripción de un Nuevo Género para C. pucherani (Dendrocolaptinae)</dcterms:title>
  </rdf:Description>
</rdf:RDF>
```

### Turtle ###
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.

<http://dx.doi.org/10.1525/auk.2009.09022> dcterms:title "Polifilia de Campylorhamphus y la Descripción de un Nuevo Género para C. pucherani (Dendrocolaptinae)"@es,
                                                         "Polyphyly of Campylorhamphus, and Description of a New Genus for C. pucherani (Dendrocolaptinae)"@en.
```

## 4.2. Example using a typed literal ##
![http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-modified.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-modified.png)

**Note:** a literal cannot simultaneously have a language tag and a datatype.
### RDF/XML ###
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF 
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dcterms="http://purl.org/dc/terms/"
>
  <rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/10849.rdf">
     <dcterms:modified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2011-08-12T06:32:43</dcterms:modified>
  </rdf:Description>
</rdf:RDF>
```

### Turtle ###
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.

<http://bioimages.vanderbilt.edu/baskauf/10849.rdf> dcterms:modified "2011-08-12T06:32:43"^^<http://www.w3.org/2001/XMLSchema#dateTime>.
```

# 5. Some terms in the `dcterms:` namespace which have declared non-literal ranges #
This list also includes terms that do not have declared ranges, but which are intended to be used with non-literal values.

|term|range|
|:---|:----|
|dcterms:creator|dcterms:Agent|
|dcterms:rightsHolder|dcterms:Agent|
|dcterms:type|rdfs:Class|
|dcterms:rights|dcterms:RightsStatement|
|dcterms:accessRights|dcterms:RightsStatement|
|dcterms:language|dcterms:LinguisticSystem|
|dcterms:temporal|dcterms:PeriodOfTime|
|dcterms:format|dcterms:MediaTypeOrExtent|
|dcterms:extent|dcterms:SizeOrDuration|
|dcterms:references|(none)|
|dcterms:source|(none)|
|dcterms:description|(none)|

## 5.1. Example with URI reference only ##
![http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-type.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-type.png)

**Notes:**

In this example, the resource identified by the object URI is described by RDF which is external to the RDF that describes the subject resource.

With regards to the term `dcterms:type`, [section 5.2.](http://dublincore.org/documents/dc-rdf/#sect-5) of the DCMI RDF guide, says "It is recommended that RDF applications implementing this specification primarily use and understand rdf:type in place of dcterms:type when expressing Dublin Core metadata in RDF, as most RDF processors come with built-in knowledge of rdf:type." Thus, although it may be desirable to include the property `dcterms:type` in the RDF description of a resource due to requirements such as the Audubon Core required terms designation (see http://species-id.net/wiki/Audubon_Core_Non_normative_document), class terms in the `http://purl.org/dc/dcmitype/` (`dcmitype:`) namespace should also be declared as objects of a `rdf:type` property of the resource rather than relying on clients to understand `dcterms:type` alone.
### RDF/XML ###
Note: use of `dcmitype:StillImage` as the XML container name asserts an `rdf:type` statement even though it does not appear as a separate statement within the container element.
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF 
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dcmitype="http://purl.org/dc/dcmitype/"
xmlns:dcterms="http://purl.org/dc/terms/"
>
<dcmitype:StillImage rdf:about="http://bioimages.vanderbilt.edu/baskauf/16626">
     <dcterms:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>
</dcmitype:StillImage>
</rdf:RDF>
```

### Turtle ###
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcmitype: <http://purl.org/dc/dcmitype/>.
@prefix dcterms: <http://purl.org/dc/terms/>.

<http://bioimages.vanderbilt.edu/baskauf/16626> dcterms:type dcmitype:StillImage;
                                                a dcmitype:StillImage.
```


## 5.2. Example with URI reference and optional value string ##
![http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-language.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-language.png)

**Notes:**

The DCAM value string is specified using the predicate `rdf:value` which does not have a specified meaning in RDF, but which has been given a meaning in the context of the DCAM, i.e. the object of `rdf:value` is a string which can represent the subject resource. (11)

This example includes the optional `dcam:memberOf` property which specifies the Vocabulary Encoding Scheme used to encode the value string.   DCMI defines URIs for some Vocabulary Encoding Schemes, but assumes that others will be defined outside of Dublin Core.
### RDF/XML ###
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF 
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:dcam="http://purl.org/dc/dcam/"
>
<rdf:Description rdf:about="http://dx.doi.org/10.1525/auk.2009.09022">
     <dcterms:language>
          <rdf:Description  rdf:about="http://id.loc.gov/vocabulary/iso639-1/en">
               <dcam:memberOf rdf:resource= "http://id.loc.gov/vocabulary/iso639-1"/>
               <rdf:value rdf:datatype="http://purl.org/dc/terms/RFC5646">en</rdf:value>
          </rdf:Description>
     </dcterms:language>
</rdf:Description>
</rdf:RDF>
```

### Turtle ###
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix dcam: <http://purl.org/dc/dcam/>.

<http://dx.doi.org/10.1525/auk.2009.09022> dcterms:language <http://id.loc.gov/vocabulary/iso639-1/en>.
<http://id.loc.gov/vocabulary/iso639-1/en> dcam:memberOf <http://id.loc.gov/vocabulary/iso639-1>;
                                           rdf:value "en"^^dcterms:RFC5646.
```

## 5.3. Example with a blank node ##
![http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-format.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-format.png)

**Note:** `dcterms:IMT` is the vocabulary encoding scheme URI for Internet Media Types

### RDF/XML ###
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF 
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:dcam="http://purl.org/dc/dcam/"
>
<rdf:Description rdf:about="http://rs.tdwg.org/dwc/terms/index.htm">
     <dcterms:format>
          <rdf:Description>
               <dcam:memberOf rdf:resource="http://purl.org/dc/terms/IMT"/>
               <rdf:value>text/html</rdf:value>
          </rdf:Description>
     </dcterms:format>
</rdf:Description>
</rdf:RDF>
```
### Turtle ###
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix dcam: <http://purl.org/dc/dcam/>.

<http://rs.tdwg.org/dwc/terms/index.htm> dcterms:format [rdf:value "text/html" ; 
                                                         dcam:memberOf dcterms:IMT].
```

## 5.4. Alternative which uses `dc:format` rather than `dcterms:format` ##
![http://tdwg-rdf.googlecode.com/svn/trunk/file/dc-format.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/dc-format.png)

**Note:** although this RDF is simpler than the previous example, the value of `dc:format` is an untyped string with no indication of the vocabulary encoding scheme.  So it provides less information to clients about how to interpret the value.

### RDF/XML ###
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF 
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
>
<rdf:Description rdf:about="http://rs.tdwg.org/dwc/terms/index.htm">
     <dc:format>text/html</dc:format>
</rdf:Description>
</rdf:RDF>
```

### Turtle ###
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dc: <http://purl.org/dc/elements/1.1/>.

<http://rs.tdwg.org/dwc/terms/index.htm> dc:format "text/html".
```

## 5.5. Example where a Dublin Core property describes a resource which is also described by other well-known terms ##
![http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-creator.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/dcterms-creator.png)

**Notes:**
In this example, the value of `dcterms:creator` has both a value URI and a value string in accordance with the DCAM.  However, the object resource is also described using a term from the FOAF vocabulary (`foaf:name`) and is typed as a `foaf:Person`.

The object is also typed as a `dcterms:Agent`.  This could be inferred from the range of `dcterms:creator`, but the `rdf:type` is given explicitly for the benefit of clients which might have limited capabilities for reasoning.

Stating that the `dcterms:creator` is also the `foaf:maker` of the document is unnecessary for clients which can perform more complex reasoning since the definition of `dcterms:creator` states that it is an equivalent property to `foaf:maker`.(12)  However, there may be a benefit in doing so anyway for the benefit of clients that cannot infer triples based on equivalent properties.

### RDF/XML ###
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF 
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:foaf="http://xmlns.com/foaf/0.1/">
<rdf:Description rdf:about="http://lod.taxonconcept.org/ses/dwAmr.html">
     <dcterms:creator>
          <rdf:Description rdf:about="http://lod.taxonconcept.org/ontology/people.owl#Peter_J_DeVries">
               <rdf:type rdf:resource="http://purl.org/dc/terms/Agent"/>
               <rdf:value>Peter J. DeVries</rdf:value>
               <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
               <foaf:name>Peter J. DeVries</foaf:name>
          </rdf:Description>
     </dcterms:creator>
     <foaf:maker rdf:resource="http://lod.taxonconcept.org/ontology/people.owl#Peter_J_DeVries"/>
</rdf:Description>
</rdf:RDF>
```

### Turtle ###
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix foaf: <http://xmlns.com/foaf/0.1/>.

<http://lod.taxonconcept.org/ontology/people.owl#Peter_J_DeVries> a dcterms:Agent,
                                                                    foaf:Person;
                                                                  rdf:value "Peter J. DeVries";
                                                                  foaf:name "Peter J. DeVries".
<http://lod.taxonconcept.org/ses/dwAmr.html> dcterms:creator <http://lod.taxonconcept.org/ontology/people.owl#Peter_J_DeVries>;
                                             foaf:maker <http://lod.taxonconcept.org/ontology/people.owl#Peter_J_DeVries>.
```

# 6. Examples in the wild #
Biodiversity Collections Index example of [RDF for http://biocol.org/urn:lsid:biocol.org:col:12599](http://www.biodiversitycollectionsindex.org/collection/rdf/id/12599) which uses Dublin Core terms from the `dc:` namespace exclusively.

HTTP-proxied DOIs dereferenced as RDF (by CrossRef). The RDF can't be downloaded directly as a file.  Go to [the W3C RDF validator](http://www.w3.org/RDF/Validator/) and enter `http://dx.doi.org/10.1525/auk.2009.09022` into the "Check by URI" box.  This example uses `dcterms:identifier`, `dcterms:title`, and `dcterms:creator`.  In the case of `dcterms:creator`, the agents are typed as `foaf:Person` and are described using `foaf:` properties.  `rdf:value` is not used.


# 7. References #
(1) dc: = `http://purl.org/dc/elements/1.1/`, see http://dublincore.org/documents/dces/

(2) See http://wiki.foaf-project.org/w/UsingDublinCoreCreator for a discussion of the term `dc:creator` in this context.

(3) http://dublincore.org/documents/abstract-model/

(4) http://dublincore.org/documents/dc-rdf/#sect-4

(5) http://dublincore.org/documents/2008/01/14/dc-rdf-notes/#sect-3

(6) http://dublincore.org/documents/dcmi-terms/

(7) http://www.w3.org/TR/rdf-schema/#ch_literal

(8) http://dublincore.org/documents/domain-range/#sect-3

(9) Even if the Dublin Core terms were defined as object properties or datatype properties in OWL (and they are not), object properties and datatype properties are not disjoint in OWL Full.  See http://www.w3.org/TR/owl-ref/#Property .  So forcing a particular property to be used with a literal or non-literal object is not easy.

(10) It is not currently possible to achieve this through a direct assertion, since literals cannot be the subject of RDF triples.

(11) The description of `rdf:value` at http://www.w3.org/TR/rdf-primer/#rdfvalue notes that `rdf:value` has no particular meaning other than as a convenience for creating structured values. However, as the designated means for expressing the value string in the abstract model, DCMI has assigned meaning to `rdf:value` in the context of the DCAM. The definition of non-literal value surrogate indicates that the value string represents the non-literal value (i.e. the resource). The entirety of the documents related to the history behind the development of the `dcterms:` terms and the explanation of how the DCAM should be used to describe resources clarifies to some extent what it means for the value string to represent the resource. This material suggests that object of the triple containing `rdf:value` is a string which would have been used as a surrogate for the resource itself in the pre-DCAM versions of Dublin Core.

(12) http://dublincore.org/2010/10/11/dcterms.rdf#creator