# General notes #
The following abbreviations are used for namespaces on this page:
|oa:|http://www.w3.org/ns/oa#|
|:--|:-----------------------|
|dcmitype:|http://purl.org/dc/dcmitype/|
|dwc:|http://rs.tdwg.org/dwc/terms/|
|tc:|http://rs.tdwg.org/ontology/voc/TaxonConcept#|

# Open Annotation (OA) Core data model #
The following diagram illustrates the core model of OA:
![http://www.openannotation.org/spec/core/images/motivations.png](http://www.openannotation.org/spec/core/images/motivations.png)
(image from `http://www.openannotation.org/spec/core/images/motivations.png`) as described at http://www.openannotation.org/spec/core/core.html#SimpleAnnotations .

The body is a comment or descriptive resource and the target is a resource that the body is somewhat "about".

The body and target resources "may be of any media type, and contain any type of content" and are recommended to have `rdf:type` which is a class described by the Dublin Core type vocabulary (`dcmitype:Image`, `dcmitype:Text`, etc.).  Thus the OA core model implies that the body and target resources are information resources which are retrievable via the Internet.

# Darwin Core ResourceRelationship model #
The Darwin Core TDWG Standard (http://www.tdwg.org/standards/450/ ) includes auxiliary terms (http://rs.tdwg.org/dwc/terms/#relindex) which can be used to describe the relationship between two identified resources.  Because Darwin Core in its present form is designed to facilitate metadata transfer in text or XML format and not in RDF, the terms listed under the ResourceRelationship class cannot be directly "translated" into RDF, particularly because of the problem associated with the use of the "ID" terms in RDF (described [elsewhere](http://code.google.com/p/tdwg-rdf/wiki/DublinCore#2.4._Possible_courses_of_action_where_users_may_be_inclined_to_u)).  However, the the model underlying the use of ResourceRelationship terms can be illustrated using an RDF graph-like diagram:

![http://tdwg-rdf.googlecode.com/svn/trunk/file/resource-relationship.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/resource-relationship.png)

where the angle brackets indicate identifiers identifying resource instances.

# TDWG TaxonConcept Ontology Relationship model #

The TaxonConcept ontology of the TDWG ontology (viewable at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.rdf) provides a mechanism for describing the relationship between taxa using `tc:Relationship` instances.  The predicates `tc:fromTaxon` and `tc:toTaxon` are used to specify the related taxa as well as the directionality of the relationship.  The nature of the relationship itself is specified using a controlled vocabulary which is defined as part of the ontology and which is based on the TCS standard (http://www.tdwg.org/standards/117/).

![http://tdwg-rdf.googlecode.com/svn/trunk/file/taxonconcept-relationship.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/taxonconcept-relationship.png)

Unlike the previous two models, the TaxonConcept Ontology has a term (`tc:hasRelationship`) which can be used to link the related resources to the instance of the relationship.

# Comparison of the three models #

From these three diagrams, we can see that there is a common strategy that is employed by the three ontologies/vocabularies as summarized in the following table:

|ontology/vocabulary|rdf:type|subject resource|object resource|relationship described by|
|:------------------|:-------|:---------------|:--------------|:------------------------|
|Darwin Core        |dwc:ResourceRelationship|identified by dwc:resourceID|identified by dwc:relatedResourceID|literal value of dwc:relationshipOfResource|
|Open Annotation model|oa:Annotation|value of oa:hasBody|value of oa:hasTarget|URI reference controlled value of oa:motivatedBy (an oa:Motivation instance)|
|TaxonConcept ontology|tc:Relationship|value of tc:fromTaxon|value of tc:toTaxon|URI reference controlled value of tc:relationshipCategory (a tc:TaxonRelationshipTerm instance)|

In each case, the purpose of the terms are to describe how two resources are related to each other by describing a relationship instance.  Thus the relationship is a separately described resource from the two related resources.  This is in contrast to an RDF predicate which describes a relationship between two resources by its incorporation in a single triple.  Unlike a relationship described simply by a triple, this kind of model allows for tracking the provenance of the asserted relationship since the relationship instance can have provenance-tracking properties (e.g. `oa:annotatedBy`, `dwc:relationshipAccordingTo`, etc.).

# Examples #

TaxonConcept relationship:

Simplified from http://biodiversity.org.au/apni.taxon/118883.rdf which uses the TDWG TaxonConcept ontology terms to describe relationships:

XML serialization:
```
<tc:TaxonConcept rdf:about="http://biodiversity.org.au/apni.taxon/118883">
   <tc:hasRelationship rdf:parseType="Resource">
      <rdf:type rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#Relationship"/>
      <tc:relationshipCategory rdf:resource="http://rs.tdwg.org/ontology/voc/TaxonConcept#IsChildTaxonOf"/>
      <tc:fromTaxon rdf:resource="http://biodiversity.org.au/apni.taxon/118883"/>
      <tc:toTaxon rdf:resource="http://biodiversity.org.au/apni.taxon/115971"/>
   </tc:hasRelationship>
</tc:TaxonConcept>
```

N3 serialization:
```
<http://biodiversity.org.au/apni.taxon/118883> tc:hasRelationship _:bnode;
	a tc:TaxonConcept.
_:bnode tc:fromTaxon <http://biodiversity.org.au/apni.taxon/118883>;
	tc:relationshipCategory tc:IsChildTaxonOf;
	tc:toTaxon <http://biodiversity.org.au/apni.taxon/115971>;
	a tc:Relationship.
```

OA examples at http://www.openannotation.org/spec/core/examples.html

Non-RDF example of use of Darwin Core ResourceRelationship terms as XML (from Darwin Core XML Guide http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#classes ):
```
<dwc:ResourceRelationship>
    <dwc:resourceRelationshipID>http://guid.mvz.org/relations/23423</dwc:resourceRelationshipID>
    <dwc:resourceID>urn:catalog:MVZ:Mammals:14523</dwc:resourceID>
    <dwc:relatedResourceID>urn:catalog:MVZ:Mammals:14524</dwc:relatedResourceID>
    <dwc:relationshipOfResource>offspring of</dwc:relationshipOfResource>
</dwc:ResourceRelationship>
<dwc:ResourceRelationship>
 <dwc:resourceRelationshipID>http://guid.mvz.org/relations/23424</dwc:resourceRelationshipID>
    <dwc:resourceID>urn:catalog:MVZ:Mammals:14524</dwc:resourceID>
    <dwc:relatedResourceID>urn:catalog:MVZ:Mammals:14523</dwc:relatedResourceID>
    <dwc:relationshipOfResource>mother of</dwc:relationshipOfResource>
</dwc:ResourceRelationship>
```
Note: HTTP URIs are made up.

# Questions #
## 1. How are these terms related to each other? ##

Because the Darwin Core ResourceRelationship vocabulary can be used to relate the most generic resources, its scope is the broadest.  So one could assert:
```
oa:Annotation  rdfs:subClassOf dwc:ResourceRelationship
```
and
```
tc:Relationship rdfs:subClassOf dwc:ResourceRelationship
```
The object properties oa:hasBody and tc:fromTaxon could be considered subproperties of an undefined object property which relates dwc:ResourceRelationship instances to instances identified by dwc:resourceID.  Similar subproperty relationships could be defined for the other properties listed in the table above.  It is questionable whether there would be value in this other than as an academic exercise, although one could use subproperty declarations in an Informed Dumb-Down" operation (http://wiki.dublincore.org/index.php/Glossary/Dumb-Down_Principle).

Does this question actually matter?  Could the dwc:ResourceRelationship class be declared rdfs:subClassOf oa:Annotation or would that be bad since OA assumes information resources?  (See example of `oa:linking` at http://www.openannotation.org/spec/core/core.html#Motivations)

## Answer ##
Refer to http://lists.w3.org/Archives/Public/public-openannotation/2013Feb/0174.html

```
<http://guid.mvz.org/relations/23423> a dwc:ResourceRelationship, oa:Annotation;
                                     oa:hasBody <http://arctos.database.museum/guid/MVZ:Mamm:14523>;
                                     oa:hasTarget <http://arctos.database.museum/guid/MVZ:Mamm:14524>;
                                     oa:motivatedBy <http://rs.tdwg.org/relations/offpringOf>;
                                     oa:annotatedAt "2001-09-14";
                                     oa:annotatedBy <http://guid.mvz.org/agents/James_L_Patton>.

<http://arctos.database.museum/guid/MVZ:Mamm:14523> a dcmitype:PhysicalObject, dwctype:PreservedSpecimen.

<http://arctos.database.museum/guid/MVZ:Mamm:14524> a dcmitype:PhysicalObject, dwctype:PreservedSpecimen. 
```
Apparently this example (containing the metadata from the non-RDF ResourceRelationship example in the Example section above, but expressed using the OA model) is a valid use of OA.  The OA model description uses words like "typically" and "generally" to allow for broader uses of OA than those that are described in the specification.


## 2. Is there a need for this level of complexity in describing relationships? ##
What are the advantages and disadvantages of creating relationship instances?  Do they facilitate reasoning better than simple predicates?  Are there non-RDF precedents for modeling relationships this way?  In modeling relationships between `tc:TaxonConcept` instances, is this approach better than simply defining predicates such as `tc:hasParentTaxon`.  In other words, do we recommend use of the TDWG TaxonConcept ontology as it is or create something simpler?

## Answer ##
Based on discussion in the thread https://groups.google.com/d/topic/tdwg-rdf/Z6p1Q02v-cQ/discussion it appears that the primary benefit of creating relationship instances using this model is to allow the tracking of provenance and to provide a URI for the relationship so that it can be linked to other resources (documentation, etc.).  Given the historical importance of documenting the details of assertions of taxonomic relationships, it may be important to facilitate recording of such details.  It was also noted that in the absence of a need for those kind of details there is no need to "reinvent RDF within RDF" (i.e. using a complex relationship model to say what could be said well directly with a single triple).  So there could be a place for a simpler model as well.

## 3. Given the lack of available object predicates in Darwin Core, how should the use of ResourceRelationship terms be described in a Darwin Core RDF Guide? ##
Do we create new terms?  Would it be appropriate to use existing (narrower) terms from OA (`oa:hasBody` and `oa:hasTarget`) to describe the subject and object resources?

## Answer ##
Apparently it is OK to use `oa:hasBody` and `oa:hasTarget` to link ResourceRelationship instances to subject and object resources (again, see http://lists.w3.org/Archives/Public/public-openannotation/2013Feb/0174.html )