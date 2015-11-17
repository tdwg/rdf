![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Ancillary documents related to the Darwin Core RDF Guide #

**Date:** (Created) 29 June 2013; (Last modified) 26 November 2014

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** This document explains the relationship between the Darwin Core RDF Guide and a number of ancillary documents which provide suggestions for strategies for exposing biodiversity data as RDF using vocabularies outside of Darwin Core.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

## 1 Rationale ##

The draft Darwin Core RDF Guide describes how to use Darwin Core terms as predicates in RDF triples.  However, there are some aspects of text-based Darwin Core data that may be too complex to express as RDF using only terms found in the Darwin Core standard.  Since the Darwin Core RDF Guide is part of the Darwin Core standard itself and is restricted primarily to describing the use of Darwin Core terms, the additional documents provided here are intended to help data providers and consumers express relationships that are beyond the scope of Darwin Core itself.

## 2 Documents ##

[Sources of IRIs recommended for use as controlled values](RecommendedIRISources.md)

A number of terms in the _dwciri:_ namespace recommend the use of well-known, controlled value IRIs.  This document lists terms that are intended for use with IRI values and sources of IRIs that are appropriate values for those terms.

[Examples using TaxonConcept Ontology object properties](DwcRdfExamplesTaxonConcept.md)

These examples follow the Darwin Core RDF Guide. They assume the data model of the TaxonConcept? Ontology (http://www.taxonconcept.org/) and use its object properties to link the class instances.

[Examples using Darwin-SW object properties](DwcRdfExamplesDarwinSW.md)

These examples follow the Darwin Core RDF Guide. They assume the data model of Darwin-SW (version 0.3; http://code.google.com/p/darwin-sw/) and use its object properties to link the class instances.

[Examples using BiSciCol object properties](DwcRdfExamplesBiSciCol.md)

These examples assume the data model of BiSciCol (http://biscicol.blogspot.com/ ) and use its object properties to link the class instances.

[Examples of representing occurrences in RDF using "pure" Darwin Core](DwcRdfOccurrences.md)

These examples assume no data model other than the one explicitly defined by Darwin Core, and use the RDF properties defined by Darwin Core to link class instances.

[Describing Taxon Concepts as RDF](TaxonInRDF.md)

Note: this document is being maintained for reference purposes.  It does not contain recommended strategies for expressing Taxon Concepts as RDF.

There is currently no TDWG standard which contains terms that are suitable for expressing taxon concepts as RDF. The Darwin Core RDF Guide discusses how `dwc:Taxon` terms can be used as convenience terms to provide metadata about taxa, but it does not specify how the taxa themselves should be described as RDF. Although not ratified standards, the TaxonConcept and TaxonName parts of the TDWG Ontology (based on the TCS Standard http://www.tdwg.org/standards/117/) can be used to express taxon concepts as RDF. This document discusses how some basic aspects of taxon concepts (sensu TCS) can be expressed as RDF using terms from the TDWG Ontology.