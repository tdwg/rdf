# Possible ways to handle dwc:associatedWhatever terms #

Steve Baskauf - 2014-11-15

The [current version of the RDF Guide](DwcRdfGuideProposalRevised.md) places the terms [dwc:associatedMedia](http://rs.tdwg.org/dwc/terms/associatedMedia), [dwc:associatedOccurrences](http://rs.tdwg.org/dwc/terms/associatedOccurrences), [dwc:associatedSequences](http://rs.tdwg.org/dwc/terms/associatedSequences), [dwc:associatedTaxa](http://rs.tdwg.org/dwc/terms/associatedTaxa), [dwc:associatedReferences](http://rs.tdwg.org/dwc/terms/associatedReferences) and [dwc:associatedOrganisms](http://rs.tdwg.org/dwc/terms/associatedOrganisms) into the category "[Darwin Core terms whose function cannot be duplicated by a dwciri: object property](#3.8_Darwin_Core_terms_whose_function_cannot_be_duplicated_by_a_d.md)".

In an off-list email conversation that included Bob Morris, Paul Morris, and me, we discussed the reasons why these terms were placed in this category and why there we chose not to just create dwciri: versions of each of them.

It would certainly be possible to create the dwciri: analogs.  The object would be the IRI of a resource of the appropriate type, and the property could be repeated as necessary to include all of the resources concatenated in the dwc:associatedWhatever string value.  This would not capture all of the information potentially included in the string, since the term definitions for several of these terms specify that the nature of the association should be included in the string, e.g. "mother of MXA-231" for dwc:associatedOrganisms and "parasitoid of:Cyclocephala signaticollis" for dwc:associatedTaxa.

Creating these 6 analogs does not feel right to me for the same reason that creating dwciri: analogs for all of the "ID" terms did not seem right.  In addition to implying an association between the subject and object, the dwc:associatedWhatever terms also imply the type of the object resource. There is no reason to overload an object property in that way, since there is a well-known method for specifying the type of a resource: assign it a rdf:type property. In lieu of creating six dwciri: analogs of the existing dwc:associatedWhatever terms, one could simply create a single term (something like dwciri:associatedWith) that one would use as an object property replacement for any of the dwc:associatedWhatever terms along with a separate type declaration for the object resource.  This would still not solve the problem of not capturing the nature of the association, but then the dwciri:associatedMedia, dwciri:associatedTaxa, etc. solution wouldn't solve that problem either.  But it would allow a provider to indicate to a consumer that they could "follow their nose" to find related resources of various sorts.  It would also be possible for a provider to use additional properties outside of DwC, such as foaf:depiction, dcterms:hasPart, dcterms:isReferencedBy, dsw:hasEvidence, etc., to specify the nature and direction of the relationship more precisely. Even if such more specfic terms did not exist at the time the provider made the assertion of association, dwciri:associatedWith would allow the association to be captured in the RDF metadata and possibly be refined at a future point.

# Possible options #

## Option 1: do nothing ##
Do nothing.  Leave the guide as it is and leave this as a problem for the future.

**Pros:** This would be the easy way out and would not slow down the process of adoption of the guide.

**Cons:** This is a problem that really needs to be dealt with since the dwc:associateWhatever terms are actually used by providers.  Paul already need some resolution of this issue for his current work.

## Option 2: create six dwciri:associatedWhatever terms ##
Create dwciri:associatedMedia, dwciri:associatedOccurrences, dwciri:associatedSequences, dwciri:associatedTaxa, dwciri:associatedReferences, and dwciri:associatedOrganisms.

**Pros:** This would also be very easy to do.  Just move the four dwc:associatedWhatever terms from [the table in section 3.8](#3.8_Darwin_Core_terms_whose_function_cannot_be_duplicated_by_a_d.md) to [the table in section 3.7](#3.7_dwc:_namespace_terms_which_have_analogues_in_the_dwciri:_nam.md).  This also would not slow down the process of the adoption of the guide, unless it was questioned in the 30 day comment period and a later revision of the guide were required.

**Cons:** This feels like a hack to me for the reasons I described above. I feel like it will create a problem that will have to be fixed later.

## Option 3: create a single dwciri:associatedWith term ##
Create the single term dwciri:associatedWith and specify that it should be used as the IRI analog for all of the dwc:associatedWhatever terms.

**Pros** This would make it possible for providers to "translate" existing dwc:associatedWhatever properties into RDF with the creation of only a single new term rather than six terms that essentially mean the same thing.  The guide as it currently stands leaves users with no guidance.

**Cons:** A new section would have to be added to the guide explaining the rationale for this approach and a new table would need to be created in the tables section at the end of the Guide, since this would really be a different category of terms.  I am willing to do this writing on a fast track, but it will delay initiation of public comment, which otherwise could probably begin as early as several days from now.  On the other hand, if the Task Group signs off on this approach, I think that there is little chance that the general TDWG public will object to it and we may end up saving time in the long time if there is a complex email exchange on the topic during public comment.

# Examples #

In these examples, `<iri1>` identifies an organism, `<iri2>` identifies some other organism with an unspecified relationship to the first organism, `<iri3>` identifies a reference document (e.g. publication) that refers to the organism, `<iri4>` identifies a photograph of the organism, and `<iri5>` identifies some other photograph of the organism that is associated in an unspecified way (perhaps a photograph of the organism's habitat).

## Examples using dwciri:associatedWhatever terms ##
```
<iri1> a dwc:Organism.
<iri1> dwciri:associatedOrganisms <iri2>.
<iri1> dwciri:associatedReferences <iri3>.
<iri1> dwciri:associatedMedia <iri4>.
<iri1> dwciri:associatedMedia <iri5>.
<iri1> dcterms:isReferencedBy <iri3>.
<iri1> foaf:depiction <iri4>.
```

A SPARQL query that would find the images.
```
SELECT ?resource WHERE {
 <uri1>  dwciri:associatedMedia ?resource.
 }
```
Of course, there is nothing to prevent the metadata providers of `<iri2>` through `<iri5>` from specifying a specific type for those resources.  But this mechanism doesn't require it.

## Example using dwciri:associatedWith ##
```
<iri1> dwciri:associatedWith <iri2>.
<iri1> dwciri:associatedWith <iri3>.
<iri1> dwciri:associatedWith <iri4>.
<iri1> dwciri:associatedWith <iri5>.
<iri1> dcterms:isReferencedBy <iri3>.
<iri1> foaf:depiction <iri4>.
<iri1> a dwc:Organism.
<iri2> a dwc:Organism.
<iri3> a foaf:Document.
<iri4> a dcmitype:StillImage.
<iri5> a dcmitype:StillImage.
```

A SPARQL query that would find the images.
```
SELECT ?resource WHERE {
 <uri1>  dwciri:associatedWith ?resource.
 ?resource a dcmitype:StillImage.
 }
```