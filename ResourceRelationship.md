![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Darwin Core Resource Relationship terms as RDF (vaporware) #

**Date:** (Created) 27 April 2013; (Last modified) 15 November 2013

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** This document shows how to express Darwin Core ResourceRelationship properties as RDF (vaporware)

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

# Note: the approach suggested in this document is no longer recommended due to concerns expressed by task group members about use of the Open Annotations model in this way #

**The content has been left here for the record and as a starting point for future discussion on how to handle ResourceRelationship class Darwin Core terms.**

The following namespace abbreviations are used in this document:

|vocabulary name|namespace abbreviation|full prefix|
|:--------------|:---------------------|:----------|
|Resource Description Framework|rdf:                  |http://www.w3.org/1999/02/22-rdf-syntax-ns#|
|Darwin Core terms (string literal objects)|dwc:                  |http://rs.tdwg.org/dwc/terms/|
|Darwin Core type vocabulary|dwctype:              |http://rs.tdwg.org/dwc/dwctype/|
|Dublin Core type vocabulary|dcmitype:             |http://purl.org/dc/dcmitype/|
|Open Annotation Data Model|oa:                   |http://www.w3.org/ns/oa#|

## 1 Introduction ##

The terms in the `dwc:ResourceRelationship` class are designed to allow for the creation of `dwc:ResourceRelationship` instances having assigned identifiers.  The following example based on an example in the [XML Guide](http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#classes) shows how the terms may be used to describe that the specimen with catalog number 14524 is the mother of a specimen with catalog number 14523:

Table 1

|term|dwc:resourceRelationshipID|dwc:resourceID|dwc:relatedResourceID|dwc:relationshipOfResource|dwc:relationshipEstablishedDate|dwc:relationshipAccordingTo|
|:---|:-------------------------|:-------------|:--------------------|:-------------------------|:------------------------------|:--------------------------|
|value|"http://guid.mvz.org/relations/23423"|"urn:catalog:MVZ:Mammals:14524"|"urn:catalog:MVZ:Mammals:14523"|"mother of"               |"2001-09-14"                   |"James L Patton"           |

Because the ID terms cannot be used as object properties, Darwin Core does not provide a means to express this relationship as RDF.  The [Open Annotation Data Model](http://www.openannotation.org/spec/core/core.html) should be used instead as shown in the following example which relates the same resources as in Table 1.

Example 1:

RDF/XML:
```
<rdf:Description rdf:about="http://guid.mvz.org/relations/23423">
   <rdf:type rdf:resource="http://rs.tdwg.org/dwc/terms/ResourceRelationship"/>
   <dwc:relationshipOfResource>mother of</dwc:relationshipOfResource>
   <dwc:relationshipEstablishedDate>2001-09-14</dwc:relationshipEstablishedDate>
   <dwc:relationshipAccordingTo>James L Patton</dwc:relationshipAccordingTo>
   <rdf:type rdf:resource="http://www.w3.org/ns/oa#Annotation"/>
   <oa:hasBody rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:14524"/>
   <oa:hasTarget rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:14523"/>
   <oa:motivatedBy rdf:resource="http://guid.mvz.org/relationshipType/motherOf"/>
   <oa:annotatedAt>2001-09-14</oa:annotatedAt>
   <oa:annotatedBy rdf:resource="http://guid.mvz.org/agents/James_L_Patton"/>
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:14523">
   <rdf:type rdf:resource="http://purl.org/dc/dcmitype/PhysicalObject"/>
   <rdf:type rdf:resource="http://rs.tdwg.org/dwc/dwctype/PreservedSpecimen"/>
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:14524">
   <rdf:type rdf:resource="http://purl.org/dc/dcmitype/PhysicalObject"/>
   <rdf:type rdf:resource="http://rs.tdwg.org/dwc/dwctype/PreservedSpecimen"/>
</rdf:Description>
```

RDF/Turtle:
```
<http://arctos.database.museum/guid/MVZ:Mamm:14523> 
	a 	dcmitype:PhysicalObject,
		dwctype:PreservedSpecimen.
<http://arctos.database.museum/guid/MVZ:Mamm:14524> 
	a 	dcmitype:PhysicalObject,
		dwctype:PreservedSpecimen.
<http://guid.mvz.org/relations/23423> 
	dwc:relationshipAccordingTo "James L Patton";
	dwc:relationshipEstablishedDate "2001-09-14";
	dwc:relationshipOfResource "mother of";
	a 	dwc:ResourceRelationship,
		oa:Annotation;
	oa:annotatedAt "2001-09-14";
	oa:annotatedBy <http://guid.mvz.org/agents/James_L_Patton>;
	oa:hasBody <http://arctos.database.museum/guid/MVZ:Mamm:14524>;
	oa:hasTarget <http://arctos.database.museum/guid/MVZ:Mamm:14523>;
	oa:motivatedBy <http://guid.mvz.org/relationshipType/motherOf>.
```

The following points should be noted about Example 1:

  * the `oa:hasBody` property has as its object the resource whose identifier is the value of `dwc:resourceID` in Table 1.
  * the `oa:hasTarget` property has as its object the resource whose identifier is the value of `dwc:relatedResourceID` in Table 1.
  * In accordance with Recommendation 7 of the TDWG GUID Applicability Statement, the identifiers for the two related specimens have been provided in their HTTP-proxied form.
  * It might have been possible for a consuming application to determine the `rdf:type` of the specimen instances by dereferencing their HTTP URIs.  However, in accordance with the [Open Annotation recommendations](http://www.openannotation.org/spec/core/core.html#BodyTargetType), the RDF provides information about the nature of the related resources which can allow the application to determine that they are non-information resources (i.e. `dcmitype:PhysicalObject`) which cannot be rendered in a browser.
  * Because there is a well-known object property for linking the relationship to the URI-referenced agent that noted it, `oa:annotatedBy` is used rather than `dwcuri:relationshipAccordingTo`.  Similarly, `oa:motivatedBy` is used rather than `dwcuri:relationshipOfResource`.  The value given for `oa:motivatedBy` should be from a controlled vocabulary which uses SKOS to relate the motivation of the annotation (i.e. the nature of the relationship) to one of the standard [high level Motivation](http://www.openannotation.org/spec/core/core.html#Motivations) instances such as `oa:linking`.