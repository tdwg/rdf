![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Describing Taxon Concepts as RDF (draft) #

**_Note: since this document was originally written, the definition of dwc:Taxon was changed to make it more clear.  In addition, there is a growing consensus that the TDWG Ontologies are effectively deprecated.  Therefore, this document should be considered as a starting point for discussion rather than a recommendation.  It is uncertain whether it will undergo further revisions._**

**Date:** (Created) 27 April 2013; (Last modified) 13 November 2014

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** There is currently no TDWG standard which contains terms that are suitable for expressing taxon concepts as RDF.  The Darwin Core RDF Guide discusses how dwc:Taxon terms can be used as convenience terms to provide metadata about taxa, but it does not specify how the taxa themselves should be described as RDF.  Although not ratified standards, the TaxonConcept and TaxonName parts of the TDWG Ontology (based on the TCS Standard http://www.tdwg.org/standards/117/) can be used to express taxon concepts as RDF. This document discusses how some basic aspects of taxon concepts (sensu TCS) can be expressed as RDF using terms from the TDWG Ontology.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**


The following namespace abbreviations are used in this document:

|vocabulary name|namespace abbreviation|full prefix|
|:--------------|:---------------------|:----------|
|Resource Description Framework|rdf:                  |http://www.w3.org/1999/02/22-rdf-syntax-ns#|
|RDF Schema     |rdfs:                 |http://www.w3.org/2000/01/rdf-schema#|
|Darwin Core terms (string literal objects)|dwc:                  |http://rs.tdwg.org/dwc/terms/|
|Darwin Core terms (URI reference objects)|dwcuri:               |http://rs.tdwg.org/dwc/uri/|
|Darwin Core type vocabulary|dwctype:              |http://rs.tdwg.org/dwc/dwctype/|
|Dublin Core terms|dcterms:              |http://purl.org/dc/terms/|
|Dublin Core legacy terms|dc:                   |http://purl.org/dc/elements/1.1/|
|TDWG Taxon Concept ontology|tc:                   |http://rs.tdwg.org/ontology/voc/TaxonConcept#|
|TDWG Taxon Name ontology|tn:                   |http://rs.tdwg.org/ontology/voc/TaxonNamet#|
|TDWG Common ontology|tcom:                 |http://rs.tdwg.org/ontology/voc/Common#|
|Bibliographic Ontology|bibo:                 |http://purl.org/ontology/bibo/|
|Representing Content in RDF|cnt:                  |http://www.w3.org/2011/content#|

## 1 Introduction ##

The class `dwc:Taxon` is defined to be a category that includes information about both names and taxon concepts.  The ambiguity in this definition reflects a general lack of clarity in the TDWG community about the exact definition of a taxon.  This degree of ambiguity is not suitable for descriptions in RDF.  The TDWG Taxon Concept Transfer Schema ([TCS; http://www.tdwg.org/standards/117/](http://www.tdwg.org/standards/117/)) Standard describes a more well-defined entity, the Taxon Concept, which contains both a name and a reference component.   These name and reference components correspond to two parts of concept names under the convention of “name sec. reference” (or “name sensu reference”).

At the time of the adoption of the Darwin Core RDF Guide, there was no existing standard for expressing the TCS Standard as RDF (TCS itself is a non-RDF XML schema).  Two parts of the TDWG Ontology, the TaxonConcept ontology and the TaxonName ontology, are based on the TCS standard.  However, given that no part of the TDWG Ontology has yet become a ratified TDWG Standard, the TDWG Ontology terms have not been recommended for use as part of the Darwin Core RDF Guide.  Nevertheless, because the TDWG Ontologies are described using RDF, they provide a means to illustrate how the metadata provided through dwc:Taxon class convenience terms (Section 2.7 of the Guide) could be rendered in a structured manner consistent with the TCS Standard.

Other models similar to TCS define taxon name usages (TNUs) or assertions [(Pyle 2004)](http://systbio.org/files/phyloinformatics/1.pdf) which allow for a broader class of references which include those that don’t explicitly define the concept.  TCS itself allows for taxon concepts to be circumscribed by specimens or sets of characters in addition to references.  The TaxonConcept OWL Ontology [(DeVries 2009)](http://www.taxonconcept.org/) describes taxon concepts even more broadly by linking them to a variety of tagged resources rather than specifying a particular secundum reference.  There are also models for mapping relationships among taxon concepts [(Franz and Peet 2009)](http://dx.doi.org/10.1017/S147720000800282X).  The exact nature of a future standard model for taxon concepts is yet to be determined and is likely to contain some or all of the complexities described above.  However, the model is likely to contain some variation on the basic structure described in this section.

The TaxonConcept ontology and the TaxonName ontology provide two defined classes (tc:TaxonConcept and tn:TaxonName) which correspond to basic components of the TCS model.  They also define object properties which can be used to relate instances of these classes and the third component, the reference, which may be an instance of one of several classes.

The general model can be represented by this graph:

<img src='http://tdwg-rdf.googlecode.com/svn/trunk/file/taxon-concept-graph.png' align='center' />

The three resources (`<concept1>`, `<reference1>`, and `<name1>`) are non-information resources which may be identified by URIs.  They may each be related to other resources by object properties.  Ideally, a provider of RDF occurrence metadata could use the property `dwcuri:toTaxonConcept` to link a `dwctype:Identification` instance to the URI of a `tc:TaxonConcept` instance found in a community repository.  However, in the absence of such a repository, providers could use terms from the TaxonConcept and TaxonName ontologies to translate text-based Darwin Core records described by `dwc:Taxon` class convenience properties into RDF that is structured in such a way that would allow their metadata to be consumed in a manner which would facilitate matching the `tc:TaxonConcept` that they describe with others in a community repository.  It is also possible that metadata described in this more structured way could be machine-translated into a future standard model for taxon concepts.

## 2 Name entities ##

A `tn:TaxonName` instance should not be considered to represent a name string, but rather be considered to represent a “name entity” which is a non-information (i.e. non-literal) resource. Although neither the TCS Standard nor the TDWG TaxonName Ontology define the `tn:TaxonName` class in the following way, a `tn:TaxonName` corresponds approximately to a protonym as defined in [Pyle 2004](http://systbio.org/files/phyloinformatics/1.pdf).   By modeling the taxon name as a non-literal, the `tn:TaxonName` instance may be the object of additional triples that describe its properties.

A metadata provider has three options for describing name entities when translating text-based Darwin Core records to RDF:

  * use a value string to represent the name entity
  * use a blank node to represent the entity
  * create a URI-referenced instance to represent the entity

Each of these approaches will be described in the sections that follow.

### 2.1 Non-literal value string representing the name entity ###

As discussed in Section 2.4.3 of the Darwin Core RDF Guide, strings have traditionally been used as a proxy for non-literal resources.  The TDWG TaxonConcept ontology defines a term, `tc:nameString`, which can be used as a `tc:TaxonConcept` instance property of whose value is a value string literal that represents the name entity associated with the concept.  It should be understood that the value of `tc:nameString` is intended to provide a means for the consumer to attempt to identify the name entity in lieu of a GUID for the entity.  Therefore, it should be understood that the value of `tc:nameString` is NOT itself the name in string form.  For this reason, a consumer may be able to conclude that various values for `tc:nameString`, such as “Hypomachilodes forthaysi Packauskas & Shofner, 2010”, “Hypomachilodes forthaysi Packauskas & Shofner”, and “ Hypomachilodes forthaysi” represent the same name entity even though they are not identical strings.  The following example illustrates the approach of referring to a name entity by a value string:

Example 1:

The following database record identifies fields using Darwin Core Taxon class terms:

|dwc:basisOfRecord|dwc:taxonID|dwc:scientificName|dwc:nameAccordingToID|
|:----------------|:----------|:-----------------|:--------------------|
|Taxon            |87694      |Hypomachilodes forthaysi|doi:10.2317/JKES1003.02.1|

This serialization expresses the same metadata using Taxon Concept ontology terms:

As RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/taxonconcepts/87694">
   <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#TaxonConcept"/>
   <tc:nameString>Hypomachilodes forthaysi</tc:nameString>
   <tc:accordingTo rdf:resource="http://dx.doi.org/10.2317/JKES1003.02.1"/>
</rdf:Description>
```

As RDF/Turtle:
```
<http://museum.org/taxonconcepts/87694> 
	tc:accordingTo <http://dx.doi.org/10.2317/JKES1003.02.1>;
	tc:nameString "Hypomachilodes forthaysi";
	a tc:TaxonConcept.
```

Notes:

  * Although the `dwc:basisOfRecord` value is reported as Taxon, for clarity the `rdf:type` value is given as `tc:TaxonConcept`.
  * The local identifier has been transformed into an HTTP URI.  This presupposes that the local identifier was intended to actually identify a taxon concept and not a name.
  * The value of the Darwin Core convenience term `dwc:scientificName` has been used as the value string that refers to the name entity through the property `tc:nameString`.
  * Because `dwc:nameAccordingToID` cannot be used in RDF, the corresponding Taxon Concept ontology term, `tc:accordingTo` is used instead, along with the HTTP-proxied version of the DOI.

### 2.2 Representing the name entity using a blank node ###

If the metadata provider is able to provide more detailed information about the name entity but is unable or unwilling to mint and maintain a URI to identify the name entity, a `tn:TaxonName` instance can be represented by a blank node whose properties describe the name entity.

Example 2:

In this example the database record contains more information about the taxon parsed into additional fields identified by `dwc:Taxon` class convenience terms:

|dwc:basisOfRecord|dwc:taxonID|dwc:scientificName|dwc:genus|dwc:specificEpithet|dwc:scientificNameAuthorship|dwc:namePublishedInYear|dwc:nameAccordingToID|
|:----------------|:----------|:-----------------|:--------|:------------------|:---------------------------|:----------------------|:--------------------|
|Taxon            |87694      |Hypomachilodes forthaysi Packauskas & Shofner, 2010|Hypomachilodes|forthaysi          |Packauskas & Shofner        |2010                   |doi:10.2317/JKES1003.02.1|

This serialization expresses the same metadata using Taxon Concept ontology terms:

As RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/taxonconcepts/87694">
   <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#TaxonConcept"/>
   <tc:hasName>
        <tn:TaxonName>
             <dcterms:title>Hypomachilodes forthaysi Packauskas &amp; Shofner, 2010</dcterms:title>
             <tn:genusPart>Hypomachilodes</tn:genusPart>
             <tn:specificEpithet>forthaysi</tn:specificEpithet>
             <tn:authorship>Packauskas &amp; Shofner</tn:authorship>
             <tn:year>2010</tn:year>
             <tn:rank rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonRank#Species"/>
        </tn:TaxonName>
   </tc:hasName>
   <tc:accordingTo rdf:resource="http://dx.doi.org/10.2317/JKES1003.02.1"/>
</rdf:Description>
```

As RDF/Turtle:
```
<http://museum.org/taxonconcepts/87694> 
	tc:accordingTo <http://dx.doi.org/10.2317/JKES1003.02.1>;
    tc:hasName [a tn:TaxonName ; 
                dcterms:title "Hypomachilodes forthaysi Packauskas & Shofner, 2010" ; 
                tn:genusPart "Hypomachilodes" ; 
                tn:specificEpithet "forthaysi" ; 
                tn:authorship "Packauskas & Shofner" ; 
                tn:year "2010" ; 
                tn:rank <http://rs.tdwg.org/ontology/voc/TaxonRank#Species>];
    a tc:TaxonConcept.
```

Notes:
  * This example follows the recommendation from the Taxon Name ontology that a string for the complete name be provided as a `dcterms:title` value.  That string is taken from the Darwin Core convenience term `dwc:scientificName`.
  * The values of the convenience terms `dwc:genus`, `dwc:specificEpithet`, `dwc:scientificNameAuthorship`, and `dwc:namePublishedInYear` are provided as values of corresponding properties that describe the `tc:TaxonName` instance.
  * When an ampersand (“&”) is used in XML it must be escaped as “&amp;”.

### 2.3 Referring to the name entity through a URI reference ###

If `tn:TaxonName` instances which are identified by URIs are available, the `tc:TaxonConcept` instance can be linked to the URI without the necessity to provide additional information about the name, as in this example:

Example 3:

As RDF/XML:
```
<rdf:Description rdf:about="http://biodiversity.org.au/apni.taxon/118883">
   <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#TaxonConcept"/>
   <tc:hasName rdf:resource="http://biodiversity.org.au/apni.name/36530"/>
   <tc:accordingTo rdf:resource="http://biodiversity.org.au/apni.reference/65103"/>
</rdf:Description>
```

As RDF/Turtle:
```
<http://biodiversity.org.au/apni.taxon/118883> 
	tc:accordingTo <http://biodiversity.org.au/apni.reference/65103>;
	tc:hasName <http://biodiversity.org.au/apni.name/36530>;
	a tc:TaxonConcept.
```

In this circumstance, the consuming application would need to dereference any previously unknown name entity URIs in order to discover the properties of the name.

## 3 Secundum (sec.) references ##

If the reference which circumscribes the taxon concept is known, it should be associated with the taxon concept using one of the methods listed in the following sections.  If no information about the reference is available (i.e. in the case of a nominal taxon concept), this information may be omitted.

### 3.1 Non-literal value string representing the reference ###

A _tc:TaxonConcept_ instance can have the property _tc:accordingToString_ whose value is a value string that represents the secundum reference. The following example illustrates the use of _tc:accordingToString_ for the reference "Gleason, Henry A. and Arthur Cronquist, 1991. Manual of Vascular Plants of Northeastern United States and Adjacent Canada. The New York Botanical Garden, Bronx, NY, US, p. 352.":

Example 4:

As RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/taxonconcepts/37524">
   <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#TaxonConcept"/>
   <tc:nameString>Acer nigrum</tc:nameString>
   <tc:accordingToString>Gleason Cronquist 1991</tc:accordingToString>
</rdf:Description>
```

As RDF/Turtle:
```
<http://museum.org/taxonconcepts/37524> 
	tc:accordingToString "Gleason Cronquist 1991";
	tc:nameString "Acer nigrum";
	a tc:TaxonConcept.
```

Because of the wide variety of formats for citing references, the TCS standard specifies the use of "signature fields" to attempt to standardize the literal values of secundum references.  The signature field is an abbreviated form of the author and year of publication.  See Section 17.2.1 of the [TCS User Guide](http://bioimages.vanderbilt.edu/pages/TCS-Schema-UserGuide-v1.3.pdf) for more information.  (Note: the user guide identifies the field as /DataSet/TaxonConcepts/TaxonConcept/AccordingTo/AuthorTeam/Simple.  However, the actual field is specified to be /DataSet/TaxonConcepts/TaxonConcept/AccordingTo/Simple in the [RDF that defines](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.rdf) _tc:accordingToString_.  This is consistent with the actual [XML schema](http://bioimages.vanderbilt.edu/pages/xmlspy_documentation_01.pdf).)  Because signature fields are not guaranteed to be globally unique, it is recommended that providers not rely exclusively on _tc:accordingToString_ as a means of identifying  the secundum reference but that they also use one of the following two methods to reduce the ambiguity of the reference and to reduce the burden on the consumer of parsing and interpreting the value string which represents the reference.  Note: if the provider wishes to provide a full literature reference, that is permissible as a value of _dwc:nameAccordingTo_.  However, the Darwin Core RDF Guide specifies that since _dwc:nameAccordingTo_ is a [convenience property](DwcRdfGuideProposal#2.7_Darwin_Core_convenience_terms.md), it should be a property of the identification instance rather than of the taxon concept.

### 3.2 Representing the reference using a blank node ###

If the metadata provider is able to provide discrete metadata properties of the reference in addition to a free-text value string, the likelihood that the reference may be matched with other instances of the same reference is increased.  The property `tc:accordingTo` should be used as a predicate whose object is the reference instance.  If the provider is unable or unwilling to maintain an identifier for the reference, the reference can be represented by a blank node.  The reference documenting the use of the name may provide only minimal (or no) information regarding the circumscription of the `tc:TaxonConcept` instance (i.e. the `tc:TaxonConcept` is a taxon name use that does not provide a circumscription).  Nevertheless, it is better to provide the information that is known rather than no information at all.

In the following example there is no known assigned identifier that is globally unique for the reference, so the reference is not identified by a URI:

Example 5:

As RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/taxonconcepts/37524">
   <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#TaxonConcept"/>
   <tc:nameString>Tilia heterophylla</tc:nameString>
   <tc:accordingTo>
        <bibo:DocumentPart>
             <dcterms:title>The Trees of Vanderbilt: Seven walks through the Vanderbilt University Arboretum</dcterms:title>
             <dc:creator>Vanderbilt University</dc:creator>
             <dc:publisher>Office of Publications and Design, Vanderbilt University, Nashville, TN, USA</dc:publisher>
             <dcterms:date>1994</dcterms:date>
             <bibo:pageStart>77</bibo:pageStart>
             <bibo:pageEnd>77</bibo:pageEnd>
        </bibo:DocumentPart>
   </tc:accordingTo>
</rdf:Description>
```

As RDF/Turtle:
```
<http://museum.org/taxonconcepts/37524> 
	tc:accordingTo 
		[a bibo:DocumentPart ; 
		dcterms:title "The Trees of Vanderbilt: Seven walks through the Vanderbilt University Arboretum" ; 
		dc:creator "Vanderbilt University" ; 
		dc:publisher "Office of Publications and Design, Vanderbilt University, Nashville, TN, USA" ; 
		dcterms:date "1994" ; 
		bibo:pageStart "77" ; 
		bibo:pageEnd "77"];
	tc:nameString "Tilia heterophylla";
	a tc:TaxonConcept.
```

Notes:

  * There is no one particular class for a reference.  Any well-known type may be asserted (in this example, `bibo:DocumentPart`).
  * Standard Dublin Core and Bibliographic Ontology terms are recommended for use as properties of the reference

### 3.3 Referring to the reference through a URI reference ###

If a URI has been assigned to the reference, the `tc:TaxonConcept` instance can be linked to the URI without the necessity to provide additional information about the reference, as shown in Example 1.  If the URI is an HTTP URI, a consumer may be able to discover additional information about the resource by dereferencing the URI.  If the URI is not an HTTP URI, the consumer would be able to unambiguously match the reference to other instances of the same reference, but would not necessarily be able to infer additional information about the reference unless it were included in the same document as the description of the concept, or if the consumer had pre-existing information about the reference from another source.

Example 6:

As RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/taxonconcepts/37525">
   <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#TaxonConcept"/>
   <tc:nameString>Acer nigrum</tc:nameString>
   <tc:accordingTo>
        <bibo:Book rdf:about="urn:isbn:0893273651">
             <dcterms:title>Manual of Vascular Plants of Northeastern United States and Adjacent Canada</dcterms:title>
             <dc:creator>Henry A Gleason</dc:creator>
             <dc:creator>Arthur Cronquist</dc:creator>
             <dc:publisher>The New York Botanical Garden, Bronx, NY, US</dc:publisher>
             <dcterms:date>1991</dcterms:date>
        </bibo:Book>
   </tc:accordingTo>
</rdf:Description>
```

As RDF/Turtle:
```
<http://museum.org/taxonconcepts/37525> 
	tc:accordingTo <urn:isbn:0893273651>;
	tc:nameString "Acer nigrum";
	a tc:TaxonConcept.
<urn:isbn:0893273651> 
	dc:creator 
		"Arthur Cronquist",
		"Henry A Gleason";
	dc:publisher "The New York Botanical Garden, Bronx, NY, US";
	dcterms:date "1991";
	dcterms:title "Manual of Vascular Plants of Northeastern United States and Adjacent Canada";
	a bibo:Book.
```

In Example 6, a valid URI has been constructed from the ISBN of the book.  Since it is a URN, it is not dereferenceable via HTTP, although it serves as an identifier for the book which is globally unique.  If a DOI is available for the reference, it should be used in its HTTP-proxied form (i.e. beginning with http://dx.doi.org/ ).

If the reference information is unpublished, it is unlikely that a separate URI will have been assigned to the reference.  In this case, a blank node may be appropriate. However, a blank node cannot be the object of a triple external to the document which defines it.  The following example shows how the [Content-in-RDF vocabulary](http://www.w3.org/TR/Content-in-RDF10/) may be used to link an unpublished reference to a `tc:TaxonConcept` instance:

Example 7:

As RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/taxonconcepts/122678">
   <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#TaxonConcept"/>
   <tc:nameString>Castilleja coccinea</tc:nameString>
   <tc:accordingTo>
        <bibo:Email rdf:about="http://museum.org/taxonconcepts/122678#reference">
             <rdf:type rdf:resource="http://www.w3.org/2011/content#ContentAsText"/>
             <dc:creator>Andrea Cardinal</dc:creator>
             <dcterms:date>2007-05-10</dcterms:date>
             <cnt:characterEncoding>UTF-8</cnt:characterEncoding>
             <cnt:chars>Steve,
That plant that we saw over in the Big Swan Creek watershed yesterday was Castilleja coccinea.  It’s really common around all of the seeps in Lewis County.
Andrea</cnt:chars>
        </bibo:Email>
   </tc:accordingTo>
</rdf:Description>
```

As RDF/Turtle:
```
<http://museum.org/taxonconcepts/122678> 
	tc:accordingTo <http://museum.org/taxonconcepts/122678#reference>;
	tc:nameString "Castilleja coccinea";
	a tc:TaxonConcept.
<http://museum.org/taxonconcepts/122678#reference> 
	dc:creator "Andrea Cardinal";
	dcterms:date "2007-05-10";
	a    bibo:Email,
	     cnt:ContentAsText;
	cnt:characterEncoding "UTF-8";
	cnt:chars """Steve,
That plant that we saw over in the Big Swan Creek watershed yesterday was Castilleja coccinea.  It’s really common around all of the seeps in Lewis County.
Andrea""".
```

Note: The method of generating a reference URI shown in this example allows the reference URI to be distinguished from the taxon concept URI without requiring the provider to manage a separate identifier record.  By identifying the reference using a fragment identifier whose base URI is that of the taxon concept, the RDF describing the reference will be included when the URI for the taxon concept is dereferenced.

## 4 Taxon Concepts which are represented by blank nodes ##

It is possible to define a taxon concept without assigning it a URI (i.e. to represent it by a blank node):

Example 8:

As RDF/XML:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/ind-baskauf/50747#2006-03-28baskauf">
   <rdf:type rdf:resource="http://rs.tdwg.org/dwc/dwctype/Identification"/>
   <dwcuri:toTaxonConcept>
        <tc:TaxonConcept>
             <tc:nameString>Acer nigrum</tc:nameString>
             <tc:accordingToString>Gleason Cronquist 1991</tc:accordingToString>
        </tc:TaxonConcept>
   </dwcuri:toTaxonConcept>
</rdf:Description>
```

As RDF/Turtle:
```
<http://bioimages.vanderbilt.edu/ind-baskauf/50747#2006-03-28baskauf> 
	dwcuri:toTaxonConcept 
		[a tc:TaxonConcept ; 
		tc:nameString "Acer nigrum" ; 
		tc:accordingToString "Gleason Cronquist 1991"];
	a dwctype:Identification.
```

However, it is questionable whether there is a significant advantage over simply using Darwin Core `dwc:Taxon` class convenience terms since in this example clients would have to perform the same kind of string matching in order to link related taxon concept instances as they would if the convenience terms were provided.

## 5 Reference ##

The following table suggests how some Darwin Core convenience terms might be represented using the TDWG TaxonConcept and TaxonName ontologies.  It is possible that as best practices evolve, there may be better alternatives for expressing Darwin Core `dwc:Taxon` terms than using the TDWG ontology terms.

|Darwin Core term|Notes on expressing using TDWG Ontology|
|:---------------|:--------------------------------------|
|dwc:nameAccordingTo|Use the object property `tc:accordingTo` to link from the taxon concept to a non-literal literature reference instance.  |
|dwc:scientificName|Use the object property `tc:hasName` to link to a non-literal name entity instance for the name. Use the datatype property `tc:nameString` to link to a literal value string which represents the name entity.|
|dwc:taxonRank   |Use `tn:rank` to indicate the rank of the object of a `tn:TaxonName` instance. See the comments in the ontology about the deprecated term `tc:rank`.|
|dwc:scientificNameAuthorship|Use `tn:authorship` as the property of a `tn:TaxonName` instance. Used with a string literal object.|
|dwc:nomenclaturalStatus|The `tn:TaxonName` instance should have the property `tn:hasAnnotation` with an object which is an instance of `tn:NomenclaturalNote`.  This note should have the property `tn:type` with value `tn:PublicationStatus` and the property `tn:note` with the text describing the status.  Consider using the Content-in-RDF vocabulary?|
|dwc:namePublishedIn|Use `tcom:publishedInCitation` as the property of a `tn:TaxonName` instance.|
|dwc:namePublishedInYear|Use `tn:year` as the property of a `tn:TaxonName` instance.|
|dwc:nomenclaturalCode|Use `tn:nomenclaturalCode` as the property of a `tn:TaxonName` instance with an appropriate controlled value URI-reference object from the `tn:NomenclaturalTerm` class, e.g. `tn:ICZN`|
|dwc:originalNameUsage|Perhaps use the term `tn:hasBasionym` to relate a `tn:TaxonName` instance to another `tn:TaxonName instance`.  This may only be appropriate for plants. |