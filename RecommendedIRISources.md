![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Sources of well-known controlled value IRIs (draft) #

**Date:** (Created) 13 November 2014; (Last modified) 15 November 2014

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** This document lists sources of well-known IRIs that are recommended to be used as controlled values for object properties that are part of the Darwin Core standard.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**


The following namespace abbreviations are used in this document:

|vocabulary name|namespace abbreviation|full prefix|
|:--------------|:---------------------|:----------|
|Resource Description Framework|rdf:                  |http://www.w3.org/1999/02/22-rdf-syntax-ns#|
|Web Ontology Language|owl:                  |http://www.w3.org/2002/07/owl#|
|Darwin Core terms (string literal objects)|dwc:                  |http://rs.tdwg.org/dwc/terms/|
|Darwin Core terms (IRI reference objects)|dwciri:               |http://rs.tdwg.org/dwc/iri/|
|Dublin Core legacy terms|dc:                   |http://purl.org/dc/elements/1.1/|
|Dublin Core terms|dcterms:              |http://purl.org/dc/terms/|
|Dublin Core type vocabulary|dcmitype:             |http://purl.org/dc/dcmitype/|

## 1 Introduction ##
Terms in the Darwin Core _dwciri:_ namespace and some terms imported from the Dublin Core _dcterms:_ namespace should have values that are IRIs.  It is considered a best practice to use well-known IRIs for this purpose rather than minting ad hoc IRIs that are not likely to be reused.  The purpose of this document is to provide an up-to-date list of sources of IRIs that are recommended for use as values for properties in Darwin Core.

## 2 Recommended sources of IRIs ##
| **Term intended for use in RDF with non-literal objects** | **source** | **access URL** |
|:----------------------------------------------------------|:-----------|:---------------|
|dcterms:language                                           |MARC ISO 639-2 language codes|http://id.loc.gov/vocabulary/iso639-2.html|
|dcterms:license                                            |Creative Commons 4.0 International licenses|http://creativecommons.org/licenses/|
|dcterms:type                                               |DCMI Type Vocabulary|http://dublincore.org/documents/dcmi-terms/#H7|
|<dl><dt>dwciri:earliestGeochronologicalEra</dt><dt>dwciri:latestGeochronologicalEra</dt></dl>|International Commission on Stratigraphy (http://www.stratigraphy.org/ )|http://resource.geosciml.org/vocabulary/timescale/isc2014.rdf|
|dwcuri:inCollection                                        |Global Registry of Biorepositories|http://grbio.org/|
|dwcuri:inDescribedPlace                                    |GeoNames geographical database|http://www.geonames.org/|
|<dl><dt>dwc:recordedBy</dt><dt>dwc:identifiedBy</dt><dt>dwc:georeferencedBy</dt><dt>dwc:locationAccordingTo (if agent is a person)</dt></dl>|<dl><dt>Virtual International Authority File (VIAF)</dt><dt>Open Researcher and Contributor ID (ORCID)</dt></dl>|<dl><dt><a href='http://viaf.org/'>http://viaf.org/</a></dt><dt><a href='http://orcid.org/'>http://orcid.org/</a></dt></dl>|