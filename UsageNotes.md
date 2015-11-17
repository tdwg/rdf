![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

<h1>RDF/OWL Usage Notes</h1>

**Date:** (Created) 17 February 2012; (Last modified) 9 November 2013

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/standards/147/) document)

**Permanent URL:** http://code.google.com/p/tdwg-rdf/wiki/UsageNotes

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=UsageNotes) (TDWG RDF/OWL Task Group)

**Abstract:** This is a series of documents which are intended to provide information about the application of RDF in particular circumstances.  They also include examples.  The usage notes are not best-practices documents because they do not necessarily represent a consensus view of the Task Group.  However, over time they may evolve into best practice documents.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) All documents in this series are licensed under a [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

## List of usage notes ##
[Darwin Core RDF Guide and ancillary documents](DwcRdf.md)
This is the cover page for the draft Darwin Core RDF Guide and ancillary documents that describe strategies for dealing with Darwin Core terms that can't easily be handled using the strategies described in the guide.  There are also examples.

[Terms in the dcterms: namespace](UsageDcterms.md)

This document summarizes the use of Dublin Core terms in the `dcterms:` namespace and provides examples of their use in RDF.  A more extensive document examining the DCMI Abstract model and its implications for RDF is [here](DublinCore.md). However, it has not been updated to reflect the recommendations of the [Darwin Core RDF Guide](DwcRdf.md) and the final version of the [Audubon Core TDWG Standard](http://terms.tdwg.org/wiki/Audubon_Core).

[Expressing License Properties as RDF](LicenseProperties.md)

This document discusses terms which can be used to express the license properties of a resource and the circumstances under which the various terms might be used.

[owl:sameAs, LSIDs, and identifier proliferation](SameAsLSID.md)

This document provides describes the implications of using `owl:sameAs` to link several URI identifiers that refer to the same resource. The particular example of LSIDs is considered.

[Notes on appropriate use of owl:FunctionalProperty? and owl:InverseFunctionalProperty](UsageFunctionalProperty.md)

This document is a stub in which notes could be placed on using functional and inverse functional properties.  Somebody should write it!

[Taxon Concepts landing page](TaxonConcepts.md)

This is a page with links to a number of documents whose topic is taxon concepts as RDF

[Comparison of Open Annotation data model with TDWG terms](OpenAnnotationAndTDWG.md)

This page contains diagrams that compare the W3C Open Annotation (OA) data model with the Darwin Core ResourceRelationship terms and the TDWG TaxonConcept Ontology Relationship model.  It includes links to emails from Robert Sanderson, a lead author of the recommendation which discuss the appropriateness of using OA in unconventional ways.  This discussion led to [this document](ResourceRelationship.md) which is included in the ancillary documents associated with the draft Darwin Core RDF Guide.  Note: Paul Morris does not think the recommendation of the ancillary document is consistent with the OA model.  See also [this email thread](OAThread.md) which led up to the creation of the comparison document linked above.

[Under what circumstances is it more beneficial to use many classes vs. few in a model?](FewClassesVsMany.md)

This is a rather incomplete page which links to some documents and emails on the subject of few classes vs. many.  There are more emails about this on tdwg-content that aren't linked here.

[Strategies for appropriate use of Darwin Core terms with literals and URI references](DwcStringTermsAsRdf.md)

This document is included here for historical purposes.  It contains notes from an informal meeting in which the problem of inconsistent use of Darwin Core terms with strings and URIs was discussed.  Since the time when this document was written, the [Audubon Core standard](http://terms.tdwg.org/wiki/Audubon_Core) was adopted.  It chose to differentiate between literal and URI-reference terms by appending a "Literal" suffix to the names of terms intended to be used with literals.  In contrast, the [Darwin Core RDF Guide](DwcRdfGuideProposal#2.5_Terms_in_the_dwcuri:_namespace.md) differentiates between the two by creating a new namespace "dwcuri:" whose terms are intended to be used exclusively with URI-reference values (or blank nodes).  Also relevant is [this document](UsageDcterms.md) which discusses the approach Dublin Core has taken with the issue.