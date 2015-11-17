![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# owl:sameAs, LSIDs, and identifier proliferation (draft) #

**Date:** (Created) 27 April 2013; (Last modified) 9 November 2013

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** This document provides describes the implications of using owl:sameAs to link several URI identifiers that refer to the same resource.  The particular example of LSIDs is considered.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**


The following namespace abbreviations are used in this document:

|vocabulary name|namespace abbreviation|full prefix|
|:--------------|:---------------------|:----------|
|Resource Description Framework|rdf:                  |http://www.w3.org/1999/02/22-rdf-syntax-ns#|
|Web Ontology Language|owl:                  |http://www.w3.org/2002/07/owl#|
|Darwin Core terms (string literal objects)|dwc:                  |http://rs.tdwg.org/dwc/terms/|
|Darwin Core type vocabulary|dwctype:              |http://rs.tdwg.org/dwc/dwctype/|
|Darwin Core terms (URI reference objects)|dwcuri:               |http://rs.tdwg.org/dwc/uri/|
|Dublin Core legacy terms|dc:                   |http://purl.org/dc/elements/1.1/|
|Dublin Core type vocabulary|dcmitype:             |http://purl.org/dc/dcmitype/|
|uBio predicates|ubio:                 |urn:lsid:ubio.org:predicates:|

## 1 Introduction ##
This document is not specifically related to the implementation of Darwin Core terms, but since TDWG has previously stated that deployment of LSIDs is a priority, and since the resources of some LSID-using providers in the TDWG community will be linked using Darwin Core properties, the means by which LSIDs are referenced in RDF will affect the implementation of Darwin Core as RDF.  The implications described below are not unique to LSIDs, but would also apply to other non-resolvable URIs such as UUIDs that are proxied using HTTP, e.g. declaring that

```
<urn:uuid:6e8bc430-9c3a-11d9-9669-0800200c9a66> owl:sameAs <http://res.org/6e8bc430-9c3a-11d9-9669-0800200c9a66>
```

When a resource is identified by an LSID, it is a best practice to associate the LSID with an http-proxied version of the LSID using `owl:sameAs`, `owl:equivalentProperty`, or `owl:equivalentClass` (Section 4) below.  However, the frequency of use of these terms of equivalence, and way in which the declarations of equivalence are made have important implications which will be discussed below.  Although the examples below use `owl:sameAs`, the implications are the same for the other terms of equivalence.

## 2 What does owl:sameAs mean? ##

In order to understand the significance of this section, one must first understand the significance of `owl:sameAs`.  `owl:sameAs` is a built-in property of the Web Ontology Language ([OWL](http://www.w3.org/TR/owl-ref/#sameAs-def)) which is used to indicate that two instances (“individuals” in the terminology of OWL) are identical.  Thus `owl:sameAs` is often used to state that two URI references refer to “the same thing”.  Persons who use `owl:sameAs` in this way may simply consider the term a convenient way to make a link to a similar resource in order to allow a client to discover additional metadata through dereferencing the URI of the other resource.

Although it is possible that client applications might use `owl:sameAs` simply as a way to traverse the web of data, `owl:sameAs` has a more powerful use when reasoning is applied to RDF.  As [Halpin et al.](http://www.w3.org/2009/12/rdf-ws/papers/ws21) point out, when `owl:sameAs` is applied to two URIs, the resources they identify are asserted to be exactly the same and they share all the same properties.  Thus ”any statement that is given to a single URI is true for every other URI that has an `owl:sameAs` link.”  Whether or not these additional inferred statements (in the form of RDF triples) are actually made depends on whether a reasoner (software capable of drawing conclusions based on RDF statements) is called upon to carry out inferencing based on `owl:sameAs` triples.  The problem described in Section 3 below occurs if reasoners do infer all possible triples based on `owl:sameAs`, while the problem described in Section 4 below occurs if reasoners are not called upon to infer triples based on `owl:sameAs`.

## 3 Proliferation of identifiers (a issue when inferencing is done) ##

The metadata for _Pternistis leucoscepus_ in the uBio Namebank [UBIO](http://www.ubio.org/) includes the following RDF:

Example 1:

In RDF/XML:
```
<rdf:Description rdf:about="urn:lsid:ubio.org:namebank:11815">
    <dc:subject>Pternistis leucoscepus (Gray, GR) 1867</dc:subject>
    <ubio:taxonomicGroup>Aves</ubio:taxonomicGroup>
</rdf:Description>
```

In RDF/Turtle:
```
<urn:lsid:ubio.org:namebank:11815> 
	dc:subject "Pternistis leucoscepus (Gray, GR) 1867";
	ubio:taxonomicGroup "Aves".
```

which would translate into the following triples:

Table 1

|subject|predicate|object|
|:------|:--------|:-----|
|<urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|

If the Recommendation 30 of the TDWG LSID Applicability Statement standard [LSID-STANDARD](http://www.tdwg.org/standards/150/) regarding an `owl:sameAs` declaration were applied, the RDF could be:

Example 2:

In RDF/XML:
```
<rdf:Description rdf:about="urn:lsid:ubio.org:namebank:11815">
    <owl:sameAs rdf:resource="http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815"/>    
   <dc:subject>Pternistis leucoscepus (Gray, GR) 1867</dc:subject>
   <ubio:taxonomicGroup>Aves</ubio:taxonomicGroup>
</rdf:Description>
```

In RDF/Turtle:
```
<urn:lsid:ubio.org:namebank:11815> 
	dc:subject "Pternistis leucoscepus (Gray, GR) 1867";
	owl:sameAs <http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>;
	ubio:taxonomicGroup "Aves".
```

where `http://lsid.tdwg.org/` is the prefix which provides actionability to the LSID via the TDWG LSID resolution service.  The added property directly adds a single triple about the subject resource:

Table 2

|subject|predicate|object|
|:------|:--------|:-----|
|<urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|
|<urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|

However, a client capable of reasoning could infer additional triples based on the `owl:sameAs` statement.  An `owl:sameAs` statement effectively asserts that in any triple, one URI can be substituted for the other.  Thus the set of triples which includes those that can be inferred by a reasoner would be:

Table 3

|subject|predicate|object|
|:------|:--------|:-----|
|<urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|
|<urn:lsid:ubio.org:namebank:11815>|owl:sameAs|http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<urn:lsid:ubio.org:namebank:11815>|

Including the `owl:sameAs` statement doubles the number of triples about the resource in a store which includes all possible inferred triples.  Although Example 2 shows only two triples provided directly by uBio, the actual RDF metadata provided by uBio includes 34 triples.  So an `owl:sameAs` statement would actually increase the number of triples to 70.

It turns out that uBio itself provides an HTTP-based LSID resolution service through by prefixing the LSID with `http://www.ubio.org/authority/metadata.php?lsid=`.  So an additional `owl:sameAs` statement could be added:

Example 3:

In RDF/XML:
```
<rdf:Description rdf:about="urn:lsid:ubio.org:namebank:11815">
   <owl:sameAs rdf:resource="http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815"/>    
   <owl:sameAs rdf:resource="http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:11815"/>    
   <dc:subject>Pternistis leucoscepus (Gray, GR) 1867</dc:subject>
   <ubio:taxonomicGroup>Aves</ubio:taxonomicGroup>
</rdf:Description>
```

In RDF/Turtle:
```
<urn:lsid:ubio.org:namebank:11815> 
	dc:subject "Pternistis leucoscepus (Gray, GR) 1867";
	owl:sameAs 
		<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>,
		<http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:11815>;
	ubio:taxonomicGroup "Aves".
```

In a triple store without inferencing, the number of triples in the example would increase from 3 to 4.  However, in a triple store with inferencing, the following triples would be present:

Table 4

|subject|predicate|object|
|:------|:--------|:-----|
|<urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|
|<urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|
|<urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:11815>|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<urn:lsid:ubio.org:namebank:11815>|
|<http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|
|<http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<urn:lsid:ubio.org:namebank:11815>|
|<http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|

which includes 4 directly asserted and 7 inferred triples.  If all 34 triples asserted by uBio were included, there would be 107 triples (36 directly asserted triples and 71 inferred triples) about the name in the triple store.

From this example, it is clear that each additional `owl:sameAs` statement can cause a dramatic proliferation of triples if a consuming application performs all possible inferencing based on `owl:sameAs`.  For this reason, it is best for the provider maintaining the LSID to pick a particular proxy URI and use it in RDF exclusively with the base LSID.  The provider should also advertise to consumers the preferred HTTP-proxied LSID to which consumers should refer in their own RDF.

## 4 Which URI form should be used to identify the subject resource in RDF metadata for an LSID-identified resource? (an issue when inferencing is NOT done) ##

In Example 3, the unproxied version of the LSID is given in the `rdf:about` attribute of the container element and the non-proxied version is the object of the `owl:sameAs` predicate.  The example could just have easily been:

Example 4:

In RDF/XML:
```
<rdf:Description rdf:about="http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815">
   <owl:sameAs rdf:resource="urn:lsid:ubio.org:namebank:11815"/>    
   <dc:subject>Pternistis leucoscepus (Gray, GR) 1867</dc:subject>
   <ubio:taxonomicGroup>Aves</ubio:taxonomicGroup>
</rdf:Description>
```

In RDF/Turtle:
```
<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815> 
	dc:subject "Pternistis leucoscepus (Gray, GR) 1867";
	owl:sameAs <urn:lsid:ubio.org:namebank:11815>;
	ubio:taxonomicGroup "Aves".
```

where the form of URI used in the `rdf:about` attribute (the subject resource) and the form used as the object of the `owl:sameAs` statement are reversed.

If a semantic client used reasoning to generate inferred triples, it would make no difference which form were used in the rdf:about attribute.  Both forms would generate the same triples, i.e. those shown in Table 3.

However, a client that does not perform reasoning would generate only the triples which were explicitly stated in the XML.  The triples generated directly from Example 3 (shown in Table 2) are not the same as the triples generated directly from Example 4 (shown in Table 5):

Table 5

|subject|predicate|object|
|:------|:--------|:-----|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|
|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<urn:lsid:ubio.org:namebank:11815>|

Consider what would happen if the following RDF would were provided to link an identification to a taxon:

Example 5:

In RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/identifications/12345">
   <rdf:type rdf:resource="http://rs.tdwg.org/dwc/terms/Identification"/>
   <dwc:identifiedBy>Juan Taxonomist</dwc:identifiedBy>
   <dwc:dateIdentified>2006</dwc:dateIdentified>
   <dwcuri:toTaxonConcept rdf:resource="http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815"/>
</rdf:Description>
<rdf:Description rdf:about="urn:lsid:ubio.org:namebank:11815">
   <owl:sameAs rdf:resource="http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815"/>    
   <dc:subject>Pternistis leucoscepus (Gray, GR) 1867</dc:subject>
   <ubio:taxonomicGroup>Aves</ubio:taxonomicGroup>
</rdf:Description>
```

In RDF/Turtle:
```
http://museum.org/identifications/12345> 
	dwc:dateIdentified "2006";
	dwc:identifiedBy "Juan Taxonomist";
	dwcuri:toTaxonConcept <http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>;
	a dwc:Identification.
<urn:lsid:ubio.org:namebank:11815> 
	dc:subject "Pternistis leucoscepus (Gray, GR) 1867";
	owl:sameAs <http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>;
	ubio:taxonomicGroup "Aves".
```

Note that the description of the identification follows the recommendation discussed in Section 2.4.2.1.1 of the Darwin Core RDF Guide (that the proxied form of an LSID be used as the object of triples) and that the description of the taxon follows the recommendation discussed in section 2.2.3 (that for resources identified by LSIDs an `owl:sameAs` statement must be used to express equivalence to its http proxy).  Also note that this example is for illustration purposes only and is not intended to express an opinion about whether or not uBio namebank instances are actually taxon concepts (and should therefore serve as the object of a `dwcuri:toTaxonConcept` object property).   The following triples would be derived directly from the XML:

Table 6

|subject|predicate|object|
|:------|:--------|:-----|
|<http://museum.org/identifications/12345>|dwc:identifiedBy|"Juan Taxonomist"|
|<http://museum.org/identifications/12345>|dwc:dateIdentified|"2006"|
|<http://museum.org/identifications/12345>|dwcuri:toTaxonConcept|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|
|<http://museum.org/identifications/12345>|rdf:type |dwctype:Identification|
|<urn:lsid:ubio.org:namebank:11815>|owl:sameAs|<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>|
|<urn:lsid:ubio.org:namebank:11815>|dc:subject|"Pternistis leucoscepus (Gray, GR) 1867"|
|<urn:lsid:ubio.org:namebank:11815>|ubio:taxonomicGroup|"Aves"|

The first four triples are derived from the description of the Identification and the last three triples describing the taxon are the same as in Table 2.

Imagine a simple client which collected triples in a store and then allowed a user to perform simple queries in the form of SPARQL [BEGINNERS-SPARQL](http://code.google.com/p/tdwg-rdf/wiki/Beginners6SPARQL), but which did not infer any triples based on `owl:sameAs` statements.  If a user wanted to query the triple store to find out what taxonomic groups which Juan Taxonomist had used in identifications, the following query could be used:

Example 6:

```
PREFIX dwc: <http://rs.tdwg.org/dwc/terms/>
PREFIX dwcuri: <http://rs.tdwg.org/dwc/uri/>
PREFIX ubio: <urn:lsid:ubio.org:predicates:>

SELECT DISTINCT ?group WHERE {
?id dwc:identifiedBy "Juan Taxonomist".
?id dwcuri:toTaxonConcept ?tax.
?tax ubio:taxonomicGroup ?group.
}
```

The query would not locate the "Aves" identification because the URI of the object of the triple having the `dwcuri:toTaxonConcept` predicate does not match the URI of the subject of the triple having the `ubio:taxonomicGroup` predicate.  However, if we substitute the taxon description given in Example 27 (having the proxied version of the URI as the `rdf:about` attribute) for the taxon description in Example 28,

Example 7:

In RDF/XML:
```
<rdf:Description rdf:about="http://museum.org/identifications/12345">
   <rdf:type rdf:resource="http://rs.tdwg.org/dwc/terms/Identification"/>
   <dwc:identifiedBy>Juan Taxonomist</dwc:identifiedBy>
   <dwc:dateIdentified>2006</dwc:dateIdentified>
   <dwcuri:toTaxonConcept rdf:resource="http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815"/>
</rdf:Description>
<rdf:Description rdf:about="http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815">
   <owl:sameAs rdf:resource="urn:lsid:ubio.org:namebank:11815"/>    
   <dc:subject>Pternistis leucoscepus (Gray, GR) 1867</dc:subject>
   <ubio:taxonomicGroup>Aves</ubio:taxonomicGroup>
</rdf:Description>
```

In RDF/Turtle:
```
<http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815> 
	dc:subject "Pternistis leucoscepus (Gray, GR) 1867";
	owl:sameAs <urn:lsid:ubio.org:namebank:11815>;
	ubio:taxonomicGroup "Aves".
<http://museum.org/identifications/12345> 
	dwc:dateIdentified "2006";
	dwc:identifiedBy "Juan Taxonomist";
	dwcuri:toTaxonConcept <http://lsid.tdwg.org/urn:lsid:ubio.org:namebank:11815>;
	a dwc:Identification.
```

the triples in Table 5 replace the last three triples in Table 6.  Now if the query in Example 6 were made, the taxonomic group `"Aves"` would be returned because there would be a URI-reference value of `?tax` that was both the object of a triple containing `dwcuri:toTaxonConcept` and the subject of a triple containing `ubio:taxonomicGroup`.

Recommendation 30 of the TDWG LSID Applicability Statement states that the proxied and unproxied forms of an LSID must be related by a statement of identity, but it does not specify which must be used as the subject in descriptive triples.  What this example shows is that it is best for providers use HTTP proxies as subjects and objects in the RDF that they provide in preference over the non-proxied version of a non-actionable URI identifier such as an LSID.

## 5 Alternatives to owl:sameAs ##

If the intent of a metadata provider is simply to make a connection between similar or related resources that are not identical, there are other well-known properties that may used instead of owl:sameAs.  The [Simple Knowledge Organization System (SKOS)](http://www.w3.org/2004/02/skos/) vocabulary provides terms such as `skos:closeMatch`, `skos:exactMatch`, and `skos:related` which might be appropriate alternatives to `owl:sameAs` in some situations.

## 6 When is owl:sameAs the best alternative? ##

In order to prevent the proliferation of identifiers and ensure that resources are found during querying in the absence of inferencing, it is a best practice to reuse well-known identifiers (e.g. [VIAF](http://viaf.org/)) rather than minting new ones.  For example, if one wishes to assert that a specimen was collected by a well-known collector, it is better to use a well-known URI for that collector than to mint a new URI.  That will allow the specimen to be linked directly to other specimens collected by the same collector even if an aggregator does not perform inferencing on the triples which are aggregated.

However, in some circumstances it is desirable to mint a URI, then use owl:sameAs to link the minted URI to a well-known URI.  For example, an institution may want to provide more extensive and current data (e.g. contact information and current projects) about a collector than are provided by a centralized authority that manages more well-known URIs.  If collection records referred only to the well-known URI, consumers of the collection records would not discover the extensive data about the collector by dereferencing the well-known URI because only the file created by the authority controlling the namespace of the well-known URI would be served.

Collection record referring only to well-known URI:

In RDF/XML:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/11722#occ">
    <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/dwctype/Occurrence" />
    <dwcuri:recordedBy rdf:resource ="http://viaf.org/viaf/63557389" />

    . . .

</rdf:Description>  
```

In RDF/Turtle:
```
<http://bioimages.vanderbilt.edu/baskauf/11722#occ> 
	dwcuri:recordedBy <http://viaf.org/viaf/63557389>;
...
	a dwctype:Occurrence.
```

Entire contents of record served by VIAF:

In RDF/XML:
```
<rdf:Description rdf:about="http://viaf.org/viaf/63557389">
    <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
    <rdf:type rdf:resource="http://rdvocab.info/uri/schema/FRBRentitiesRDA/Person"/>
    <foaf:name>Baskauf, Steven J.</foaf:name>
</rdf:Description>
```

In RDF/Turtle:
```
<http://viaf.org/viaf/63557389> 
	a 	<http://rdvocab.info/uri/schema/FRBRentitiesRDA/Person>,
		foaf:Person;
	foaf:name "Baskauf, Steven J.".
```

However, if the collection records referred to a URI minted by the organization that managed the collection, dereferencing that URI would serve the RDF file containing the extensive information.

Collection record referring to minted URI:

In RDF/XML:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/11722#occ">
    <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/dwctype/Occurrence" />
    <dwcuri:recordedBy rdf:resource ="http://bioimages.vanderbilt.edu/contact/baskauf"/>
</rdf:Description>  
```

In RDF/Turtle:
```
<http://bioimages.vanderbilt.edu/baskauf/11722#occ> 
	dwcuri:recordedBy <http://bioimages.vanderbilt.edu/contact/baskauf>;
	a dwctype:Occurrence.
```

Contents of extensive record served by organization minting the URI:

In RDF/XML:
```
<foaf:Person rdf:about="http://bioimages.vanderbilt.edu/contact/baskauf">
    <owl:sameAs rdf:resource="http://viaf.org/viaf/63557389"/>
    <foaf:name>Steven J. Baskauf, Ph.D.</foaf:name>
    <foaf:family_name>Baskauf</foaf:family_name>
    <foaf:nick>Steve</foaf:nick>
    <foaf:mbox rdf:resource="mailto:steve.baskauf@vanderbilt.edu"/>
    <foaf:homepage rdf:resource="http://bioimages.vanderbilt.edu/"/>
    . . .
</foaf:Person>
```

In RDF/Turtle:
```
http://bioimages.vanderbilt.edu/contact/baskauf> 
	owl:sameAs <http://viaf.org/viaf/63557389>;
	foaf:family_name "Baskauf";
	foaf:homepage <http://bioimages.vanderbilt.edu/>;
	foaf:mbox <mailto:steve.baskauf@vanderbilt.edu>;
	foaf:name "Steven J. Baskauf, Ph.D.";
	foaf:nick "Steve";
...
	a foaf:Person.
```

Notice that the extensive record contains an `owl:sameAs` property linking the minted URI to the well-known URI.  So clients that dereference the minted URI can also discover that the resource it identifies is identical to the resource identified by the well-known URI.

## 7 Summary Recommendations ##

In light of the issues raised in this section, the following are recommended:
  * When providers mint non-resolvable URIs, they should select a single HTTP proxy service to reference in the RDF which they create.
  * Providers minting non-resolvable URIs should advertise their choice of preferred proxy form to potential Linked Data users.
  * Providers who simply want to provide links to related resources rather than asserting identity should use terms appropriate terms from a vocabulary such as SKOS rather than `owl:sameAs` or other terms of identity that may be used to create inferred triples.
  * Providers should generally reuse well-known URIs.