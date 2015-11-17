[![](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)](http://www.tdwg.org/)  http://www.tdwg.org

# Beginner's Guide to RDF #

**Date:** (Created) 17 February 2012; (Last modified) 19 Feb 2014

**Document Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document)

**Permanent URL:** http://code.google.com/p/tdwg-rdf/wiki/Beginners

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** This document provides concise information about topics related to RDF and OWL in the context of the biodiversity informatics community.  It is intended as an introduction for persons who are not already familiar with RDF and OWL and as a reference for persons who are familiar but would like organized access to additional reference material.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**

[0. Introduction (this page)](#Beginner%27s_guide_to_RDF:_0._Introduction.md)

[1. Resources and URIs](Beginners1URIs.md)

[2. What is RDF and what is it for?](Beginners2WhatIsRDF.md)

[3. RDF basics](Beginners3RDFbasics.md)

[4. Vocabularies, DCAM, and RDFS](Beginners4Vocabularies.md)

[5. Discovery, Transmission, and Storage of RDF data](Beginners5RDFdata.md)

[6. Querying with SPARQL](Beginners6SPARQL.md)

[7. Ontologies and OWL](Beginners7OWL.md)

---


# Beginner's guide to RDF: 0. Introduction #

**Contents**



## 0.1. Purpose ##

The purpose of this guide is to provide concise information about topics related to RDF and OWL which are significant to the work of the [TDWG](http://www.tdwg.org/) RDF/OWL Task Group (RDF/OWL TG) in particular and to the biodiversity informatics community in general.  It is intended as an introduction for persons who are not already familiar with RDF and OWL and as a reference for persons who are familiar but would like organized access to additional reference material.  Although it is intended that the information provided be correct, because it is intended as an introduction the amount of technical jargon and formal language has been kept to a minimum.  For those who are interested in normative descriptions of the concepts and technologies discussed here, footnotes are provided to hyperlinks to more detailed information.

It should also be noted that in almost every instance, the URIs that are used in the examples are "real" URIs (no fake "example.org" URIs) from the wild which in most cases will actually dereference (at least in the case of HTTP URIs and LSIDs).  This is not to imply that there is something special about those URIs or that the examples that they provide are a model of any sort, but rather it is to give the reader an opportunity to actually try out the tools that have been provided for validating, describing, browsing, etc.

## 0.2. Format ##

The guide is laid out into sections, each of which deals with a major issue relevant to the work of the RDF/OWL TG.  This allows users who wish to access the guide as a reference to jump quickly to the point of interest.  However, the later sections presuppose knowledge of concepts discussed in earlier sections, so a beginner may have difficulty starting at a later section.

Within each section, subsections are laid out hierarchically and linked in a Table of Contents at the top of the section page.  At the end of each section is a numbered reference list which is also linked to the Table of Contents as well as the actual references in the text.

A beginner who wants to gain a basic understanding of RDF and OWL should start with section 1 and work through the guide sequentially.  However, it is not intended that this guide be a tutorial capable of enabling a beginner to write RDF or OWL.  Consulting additional references will undoubtedly be required.



## 0.3 Significant documents, tools, and RDF implementations ##
The mention of any document or tool in this guide does not imply the endorsement of TDWG or the RDF/OWL TG.  (The exception to this is ratified [TDWG standards](http://www.tdwg.org/standards/) which are official recommendations of TDWG.)  The referenced items below are simply ones which have been found to be helpful.  The lists are not exhaustive; resources may be added when discovered or removed if they cease to be available.

An important general reference is [Architecture of the World Wide Web](http://www.w3.org/TR/webarch/), a W3C Recommendation.

The document [Linked Data: Evolving the Web into a Global Data Space](http://linkeddatabook.com/book) provides a general overview of Linked Data issues and implementation strategies.

See also a list of [design issues](http://www.w3.org/DesignIssues/) intended to avoid repetition of discussions once resolved.

The [Pedantic Web](http://pedantic-web.org/) group is concerned with the quality of RDF data and has created a list of [Frequently Observed Problems on the Web of Data](http://pedantic-web.org/fops.html).

Information Standards Quarterly had a special issue (Vol. 24, No. 2/3, [doi:10.3789/isqv24n2-3.2012](http://dx.doi.org/10.3789/isqv24n2-3.2012) devoted to Linked Data in Libraries, Archives, and Museums.

A PowerPoint presentation for an RDF Primer session at TDWG 2013 is [here](http://tdwg-rdf.googlecode.com/svn/trunk/file/Baskauf_RdfPrimer.pdf).  The background video for the session is [here](http://youtu.be/XAGifYBiXMY).

### 0.3.1. Related to Uniform Resource Identifier (URI) and GUID/Persistent Identifier ###
[RFC 3986. Uniform Resource Identifier (URI): Generic Syntax](http://tools.ietf.org/html/rfc3986)  ([section 1.2.2. defining "dereference", "resolution", and "representation"](http://tools.ietf.org/html/rfc3986#section-1.2.2))

[RFC 3987. Internationalized Resource Identifiers (IRIs)](http://tools.ietf.org/html/rfc3987)

[Compact URI (CURIE) Syntax 1.0 W3C Working Group Note](http://www.w3.org/TR/curie/)

[Cool URIs for the Semantic Web](http://www.w3.org/TR/cooluris/)

[RFC 2616. Hypertext Transfer Protocol -- HTTP/1.1](http://tools.ietf.org/html/rfc2616)  ([section 1.3 Terminology including definition of "resource" and "representation"](http://tools.ietf.org/html/rfc2616#section-1.3))  ([section 12 on Content Negotiation](http://tools.ietf.org/html/rfc2616#section-12))

[Apache mod\_rewrite (URL rewriting)](http://httpd.apache.org/docs/current/rewrite/)

[Best Practice Recipes for Publishing RDF Vocabularies](http://www.w3.org/TR/swbp-vocab-pub/) (content negotiation and URI dereferencing)

[GUID Applicability Statement - Current TDWG Standard](http://www.tdwg.org/standards/150/)  ([click here for PDF viewable via browser](http://bioimages.vanderbilt.edu/pages/guid-applicability-final-2011-01.pdf))

[A Beginner's Guide to Persistent Identifiers](http://www.gbif.org/orc/?doc_id=2428) published by the [Global Biodiversity Information Facility(GBIF)](http://www.gbif.org/)

[Integrated Digital Biocollections (iDigBio) GUID Statement](https://www.idigbio.org/content/idigbio-guid-statement)

[Life Sciences Identifiers Applicability Statement - Current TDWG Standard](http://www.tdwg.org/standards/150/)   ([click here for PDF viewable via browser](http://bioimages.vanderbilt.edu/pages/LSID%20AS_2011_01_final.pdf))

[LSID Best Practices](http://www.ibm.com/developerworks/opensource/library/os-lsidbp/)

[LSID Specification](http://www.omg.org/cgi-bin/doc?dtc/04-05-01.pdf)

[Jones et al. 2011. Identifying and relating biological concepts in the Catalogue of Life.](http://www.jbiomedsem.com/content/2/1/7) Journal of Biomedical Semantics 2011,2:7. doi:10.1186/2041-1480-2-7

[DOIs as HTTP URIs](http://www.crossref.org/CrossTech/2011/04/content_negotiation_for_crossr.html)

To locate DOIs for _titles_ (books, monographs, or whole journal runs) in the [Biodiversity Heritage Library](http://www.biodiversitylibrary.org/) (BHL), locate the title through searching, then access the URL
```
http://www.biodiversitylibrary.org/bibliography/[title_number]
```
or
```
http://www.biodiversitylibrary.org/title/[title_number]
```
where `[title_number]` is the BHL-assigned identifying number for the title.  Currently, BHL does not assign DOIs to individual articles unless they happen to correspond to a monograph.

DOIs can be exported _en masse_ through BHLs data export at http://biodivlib.wikispaces.com/Data+Exports and are exposed at the BHL API and OpenURL resolver http://biodivlib.wikispaces.com/Developer+Tools+and+API .

Thanks to Rod Page and Chris Freeland for this information.

[An example of DOIs used with specimens](http://iphylo.blogspot.co.uk/2013/04/a-decadal-view-of-biodiversity.html#comment-904886746)

### 0.3.2. Related to the Resource Description Framework (RDF) model ###
[RDF Primer (intended for beginners)](http://www.w3.org/TR/2004/REC-rdf-primer-20040210/)

[RDF Concepts and Abstract Syntax (normative description of namespace, datatypes, and abstract syntax)](http://www.w3.org/TR/rdf-concepts/)

[RDF/XML Syntax Specification (normative)](http://www.w3.org/TR/rdf-syntax-grammar/)

[Terse RDF Triple Language (Turtle)](http://www.w3.org/TR/turtle/)

[RDFa Core 1.1](http://www.w3.org/TR/rdfa-syntax/)

[JSON-LD JSON-based Serialization for Linked Data](http://www.w3.org/TR/json-ld/)

[RDF Semantics (normative)](http://www.w3.org/TR/rdf-mt/)

[RDF Vocabulary Description Language 1.0: RDF Schema (RDFS)](http://www.w3.org/TR/rdf-schema/)

[RSS specification (view source to see RDF)](http://web.resource.org/rss/1.0/)

[SPARQL 1.1 Query Language](http://www.w3.org/TR/sparql11-query/) ([communication protocol](http://www.w3.org/TR/sparql11-protocol/))

[Page 2006 "Taxonomic names, metadata, and the Semantic Web" (modeling taxonomic metadata relationships in RDF)](https://journals.ku.edu/index.php/jbi/article/view/25)

[W3C Interest Group note: Mapping and linking life science data using RDF](https://docs.google.com/a/nescent.org/document/d/1XzdsjCfPylcyOoNtDfAgz15HwRdCD-0e0ixh21_U0y0/edit?hl=en_US) (Thanks to Hilmar Lapp for providing the link.)

[Early draft of expressing Darwin Core taxonomies in SKOS](http://www.w3.org/egov/wiki/Linked_Environment_Data) (Thomas Bandholtz)

[Open Annotation Core Data Model](http://www.openannotation.org/spec/core/) (for creating associations between distant pieces of information)

[Proposal for linking metadata to the web pages they describe](http://www.w3.org/QA/2010/07/new_opportunities_for_linked_d.html)

Information about the draft Shape Expressions language for validating RDF [Shape Expressions primer](http://www.w3.org/2013/ShEx/Primer) [Shape Expressions definition](http://www.w3.org/2013/ShEx/Definition)

### 0.3.3. Related to the Dublin Core Metadata Initiative (DCMI) Abstract Model ###
[DCMI Abstract Model (DCAM) specification](http://dublincore.org/documents/abstract-model/)   ([Relationship between DCAM and RDFS](http://dublincore.org/documents/abstract-model/#sect-5))

[Representing DCAM constructs using the RDF Model](http://dublincore.org/documents/dc-rdf/#sect-4)

[Notes on DCMI specifications for Dublin Core metadata in RDF](http://dublincore.org/documents/2008/01/14/dc-rdf-notes/)

[Domains and Ranges for DCMI Properties](http://dublincore.org/documents/domain-range/)

[Darwin Core abstract model (vs. DCAM)](http://rs.tdwg.org/dwc/terms/guides/xml/index.htm#abstractmodel)

### 0.3.4. Related to Web Ontology Language (OWL) ###
[OWL 2 Web Ontology Language Primer (for beginners)](http://www.w3.org/TR/owl-primer/)

[OWL 2 Web Ontology Language Document Overview](http://www.w3.org/TR/owl2-overview/)

[OWL 2 Web Ontology Language RDF-Based Semantics](http://www.w3.org/TR/owl2-rdf-based-semantics/)

[A Practical Guide To Building OWL Ontologies Using Protégé 4 and CO-ODE Tools](http://owl.cs.manchester.ac.uk/tutorials/protegeowltutorial/)

[Allemang and Hendler Semantic Web for the Working Ontologist, Second Edition: Effective Modeling in RDFS and OWL (not available online)](http://www.amazon.com/Semantic-Web-Working-Ontologist-Second/dp/0123859654/)

[Hogan et al. 2011 Scalable OWL 2 Reasoning for Linked Data](http://sw.deri.org/~aidanh/docs/rw_2011.pdf)

[Link to Aidan Hogan's Ph.D. thesis "Exploiting RDFS and OWL for Integrating Heterogeneous, Large-Scale, Linked Data Corpora" and other OWL and RDF related links](http://sw.deri.org/~aidanh/)

[Ontobee web server for Ontologies](http://www.ontobee.org/)  Can be set up with PURL redirection to dereference ontology terms.  See [this email](http://lists.tdwg.org/pipermail/tdwg-content/2012-May/002889.html) for further information.

**Some rule-based extensions to OWL/SPARQL/RDF**

[SWRL submission to W3C (stalled?)](http://www.w3.org/Submission/SWRL/)

[SPIN submission to W3C (SPARQL-based)](http://www.w3.org/Submission/spin-overview/)

[W3C Rule Interchange Format (RIF) FAQ page](http://www.w3.org/2005/rules/wiki/RIF_FAQ)

### 0.3.5. Software tools ###
[rdfEditor (syntax highlighting, validates and converts)](http://www.dotnetrdf.org/content.asp?pageID=rdfEditor)

[jEdit (plugin for XML will validate, no RDF plugin)](http://www.jedit.org/)

[Protégé ontology editor](http://protege.stanford.edu/) ([guide](http://owl.cs.manchester.ac.uk/tutorials/protegeowltutorial/))

[SWOOP tool for creating, editing, and debugging OWL ontologies](http://code.google.com/p/swoop/)

[Pellet OWL Reasoner](http://clarkparsia.com/pellet) ([Pellet tutorial](http://clarkparsia.com/pellet/tutorial))

[ELK reasoner](https://code.google.com/p/elk-reasoner/) (supports the  [OWL 2 EL](http://www.w3.org/TR/owl2-profiles/#OWL_2_EL) profile)

See also http://www.w3.org/RDF/ for a listing of tools relevant to RDF

[mx](http://mx.phenomix.org/index.php/Main_Page) - a Ruby-based platform that consists of a Ruby on Rails application and various supporting gems/libraries developed as a collaborative web-based content management system for biodiversity informatics.

### 0.3.6. Web interfaces ###
[Vapour Linked Data Validator for examining the dereferencing process for a URI](http://validator.linkeddata.org/vapour)

[URI Debugger to dereference URIs and visualize the HTTP response of the server](http://linkeddata.informatik.hu-berlin.de/uridbg/)

[Rod Page's LSID tester](http://darwin.zoology.gla.ac.uk/~rpage/lsid/tester/)

[TDWG LSID resolver](http://lsid.tdwg.org/)

[Rod Page's LSID resolver](http://bioguid.info/lsid.php)

[Rod Page's OpenURL Resolver which can be used to proxy some identifiers as HTTP URIs which return RDF](http://bioguid.info/openurl/)  Paper: ["bioGUID: resolving, discovering, and minting identifiers for biodiversity informatics" doi:10.1186/1471-2105-10-S14-S5](http://www.biomedcentral.com/1471-2105/10/S14/S5)

[W3C RDF Validation Service (includes graphical display)](http://www.w3.org/RDF/Validator/)

[rdfabout.com RDF Validator and Converter (converts from XML to N3 and vice versa)](http://www.rdfabout.com/demo/validator/)

[RSS validator (also XML validation)](http://www.validome.org/rss-atom/)

[Manchester OWL Validator](http://owl.cs.manchester.ac.uk/validator/)

[WonderWeb OWL Ontology Validator](http://www.mygrid.org.uk/OWL/Validator)

[Mindswap OWL Consistency Checker](http://www.mindswap.org/2003/pellet/demo.shtml)

[Live OWL Documentation Environment](http://www.essepuntato.it/lode) generates human-readable versions of OWL ontologies (see [this documentation](http://speroni.web.cs.unibo.it/publications/peroni-2012-live-documentation-environment.pdf)

[Rod Page's "Status of Biodiversity Services" checker (takes a long time to run so be patient)](http://bioguid.info/status/)

[Marbles Linked Data browser](http://www5.wiwiss.fu-berlin.de/marbles)

[OpenLink Data Explorer Linked Data Browser](http://linkeddata.uriburner.com/ode/)

[Zitgist Linked Data viewer](http://dataviewer.zitgist.com/)

[Disco Hyperdata Browser](http://www4.wiwiss.fu-berlin.de/rdf_browser/)

[Semantic Information Mashup (sig.ma) using Sindice's semantic web index](http://sig.ma/search)

[URIBurner test basic SPARQL endpoint](http://uriburner.com/sparql)

[URIBurner enhanced SPARQL endpoint](http://uriburner.com/isparql)

### 0.3.7. Biodiversity-related and General vocabularies and ontologies ###
[Audubon Core (AC) draft TDWG standard](http://terms.gbif.org/wiki/Audubon_Core) ([draft term list](http://terms.gbif.org/wiki/Audubon_Core_Term_List_%281.0_normative%29))

Australian Plant Name Index (APNI) vocabulary ([in RDF](http://www.biodiversity.org.au/voc/apni/APNI.rdf))

[Bibliographic Ontology Specification (BIBO)](http://bibotools.googlecode.com/svn/bibo-ontology/trunk/doc/index.html) ([in RDF/N3](http://code.google.com/p/bibotools/source/browse/bibo-ontology/tags/1.0/bibo.n3))

[Content-in-RDF10 (Representing Content in RDF 1.0 vocabulary)](http://www.w3.org/TR/Content-in-RDF10/)

[Creative Commons Rights Expression Language (CC REL)](http://creativecommons.org/ns#) ([in RDF](http://creativecommons.org/schema.rdf))

[Darwin Core (DwC) TDWG Standard](http://www.tdwg.org/standards/450/) ([homepage](http://rs.tdwg.org/dwc/)) ([term quick reference guide](http://rs.tdwg.org/dwc/terms/index.htm)) ([term definitions in RDF](http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwcterms.rdf)) ([type vocabulary](http://rs.tdwg.org/dwc/terms/type-vocabulary/index.htm)) ([type definitions in RDF](http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwctype.rdf))

[darwin-sw (DSW) ontology](http://code.google.com/p/darwin-sw/) ([in RDF](http://code.google.com/p/darwin-sw/source/browse/trunk/dsw.owl))

[Dublin Core (DC) terms](http://dublincore.org/documents/dcmi-terms/) ([in RDF](http://dublincore.org/2010/10/11/dcterms.rdf)) ([type vocabulary](http://dublincore.org/documents/dcmi-type-vocabulary/#H7))  ([in RDF](http://dublincore.org/2010/10/11/dctype.rdf))

[FOAF Vocabulary Specification 0.98](http://xmlns.com/foaf/spec/) ([in RDF](http://xmlns.com/foaf/spec/index.rdf))

[Basic Geo WGS84 lat/long (GEO) Vocabulary](http://www.w3.org/2003/01/geo/) ([in RDF](http://www.w3.org/2003/01/geo/wgs84_pos))

[GeoSciML Geologic Timescale model Ontology](https://www.seegrid.csiro.au/wiki/CGIModel/GeologicTime) ([in RDF](http://resource.geosciml.org/ontology/timescale/gts-30.rdf))

[Library of Congress Authorities and Vocabularies: ISO639 languages, MARC countries and geographic areas](http://id.loc.gov/) (Use view page source: [ISO639](http://id.loc.gov/vocabulary/iso639-1.rdf), [MARC geographic areas](http://id.loc.gov/vocabulary/geographicAreas.rdf), etc. in RDF)

[Linked Open Data of Ecology (LODE) vocabulary](http://test.ckan.org/lv/dataset/linked-open-data-of-ecology) ([Ecoinformatics Working Group of the TFRI](http://ecoinformatics.tfri.gov.tw/ternwork/member))

[MARC (Library of Congress) Relators list (terms are subPropertyOf dc:contributor and possibly other dc:terms)](http://id.loc.gov/vocabulary/relators.html)  see also [MARC Relator terms and Dublin Core](http://dublincore.org/usage/documents/relators/)

[Natural Collections Descriptions (NCD) draft TDWG Standard](http://www.tdwg.org/standards/312/) ([PDF non-normative document viewable in browser](http://bioimages.vanderbilt.edu/pages/NCD-v090_TDWG-NonNormative.pdf)) ([PDF normative document viewable in browser](http://bioimages.vanderbilt.edu/pages/NCD-v090_TDWG-Normative.pdf)) ([Collection in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/Collection.rdf))  ([Institution in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/Institution.rdf)) ([InstitutionType in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/InstitutionType.rdf)) ([ContactDetails in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/ContactDetails.rdf))

[Open Annotation Core Data Model](http://www.openannotation.org/spec/core/)

OBO foundry (http://www.obofoundry.org/ ) ontologies:

  * Basic Formal Ontology (BFO) http://www.ifomis.org/bfo .  Includes definition of "process" and "material entity".

  * Biological Collections Ontology (BCO) ([browse draft here](http://bioportal.bioontology.org/ontologies/49826?p=terms)) ([view draft OWL as RDF](http://biocode-commons.googlecode.com/svn/trunk/ontologies/biocollections/biocode.owl)).  Includes definition of "material sample", "sampling process", and "observing process".

  * Common Anatomy Reference Ontology (CARO) ([browse here](http://bioportal.bioontology.org/ontologies/46615?p=terms) or [here](http://www.ontobee.org/browser/rdf.php?o=CARO&iri=http://purl.obolibrary.org/obo/CARO_0000012))  ([OWL as RDF](http://www.berkeleybop.org/ontologies/owl/CARO)).  Includes definition of "multicellular organism" and "organism".

  * Environment Ontology (EnvO) http://www.environmentontology.org/ .  Includes definition of "biome" and "environmental feature".

  * Gene Ontology (GO) http://www.geneontology.org/ . ([browse](http://amigo.geneontology.org/cgi-bin/amigo/browse.cgi)).  Includes definition of "biological process".

  * Information Artifact Ontology (IAO) http://code.google.com/p/information-artifact-ontology/ . Includes definition of "information content entity" and "data item".

  * Ontology for Biomedical Investigations (OBI) http://obi-ontology.org/ ([OWL as RDF](http://obi.svn.sourceforge.net/svnroot/obi/releases/2012-07-01/merged/merged-obi-comments.owl)).  Includes definition of "planned process".

  * Plant Ontology (PO) http://www.plantontology.org/  ([OWL as RDF](http://owlfiles.plantontology.org/))

  * Population and Community Ontology (PCO) http://code.google.com/p/popcomm-ontology/ (http://code.google.com/p/popcomm-ontology/source/browse/trunk/pco.owl view OWL as RDF]).  Includes definition of "species", "population", "species", and "community".

[PROV (Provenance) Model primer](http://www.w3.org/TR/2013/WD-prov-primer-20130312/)

[PAV (Provenance, Authoring and Versioning) Ontology (a lightweight ontology that is a refinement of PROV)](http://pav-ontology.googlecode.com/svn/tags/2.1.1/pav.owl)

[Publishing Requirements for Industry Standard Metadata (PRISM)](http://www.idealliance.org/specifications/prism/) (RDF???)

[SKOS Simple Knowledge Organization System Namespace Document](http://www.w3.org/2009/08/skos-reference/skos.html) ([in RDF](http://www.w3.org/2009/08/skos-reference/skos.rdf))

[Taxon Meta-Ontology TaxMeOn](http://www.ldf.fi/schema/taxmeon/index.html) Associated paper: Making species checklists understandable to machines - a shift from relational databases to ontologies http://dx.doi.org/10.1186/2041-1480-5-40

[Taxonomic Concept Transfer Schema (TCS) (TDWG Standard)](http://www.tdwg.org/standards/117/) [(Users Guide PDF viewable in browser)](http://bioimages.vanderbilt.edu/pages/TCS-Schema-UserGuide-v1.3.pdf) [(XML schema details PDF viewable in browser)](http://bioimages.vanderbilt.edu/pages/xmlspy_documentation_01.pdf) ([TaxonConcept in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.rdf))  ([TaxonName in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonName.rdf))  ([Common in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/Common.rdf))  [Journal of Biomedical Semantics 2:7 article on application of LSIDs and TCS at Catalogue of Life](http://www.jbiomedsem.com/content/2/1/7)

[TaxonConcept Ontologies](http://www.taxonconcept.org/ontologies/) ([in RDF](http://lod.taxonconcept.org/ontology/txn.owl))

[TDWG Ontology (human readable)](http://wiki.tdwg.org/twiki/bin/view/TAG/TDWGOntology)  ([in RDF](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/))

[vCard](http://www.w3.org/Submission/vcard-rdf/) ([in RDF](http://www.w3.org/2006/vcard/ns))

[VoID vocabulary](http://www.w3.org/TR/void/) ([see also](http://vocab.deri.ie/void))


### 0.3.8. Biodiversity-related RDF in the wild ###
[Atlas of Living Australia (ALA) National Species List (NSL) Linked Data Services; uses DC, TCS, APNI](http://www.biodiversity.org.au/confluence/display/bdv/NSL%2bServices) ([example resource](http://biodiversity.org.au/apni.taxon/118883.rdf))

[Biodiversity Collections Index; uses DC, vCard, and NCD](http://www.biodiversitycollectionsindex.org/static/index.html) ([example resource](http://www.biodiversitycollectionsindex.org/collection/rdf/id/12599))

[Bioimages; uses DC, DwC, TCS, FOAF, AC, DSW, and others](http://bioimages.vanderbilt.edu/) ([example resource](http://bioimages.vanderbilt.edu/baskauf/10531.rdf)) ([example resource](http://bioimages.vanderbilt.edu/vanderbilt/7-16.rdf))

[DOIs dereferenced as RDF; uses DC, BIBO, PRISM](http://www.crossref.org/CrossTech/2011/04/content_negotiation_for_crossr.html) ([example resource](http://www5.wiwiss.fu-berlin.de/marbles?uri=http%3A%2F%2Fdx.doi.org%2F10.1525%2Fauk.2009.09022) URI is `http://dx.doi.org/10.1525/auk.2009.09022` but RDF can't be viewed in a browser directly)

[International Chronostratigraphic Chart (2012)](http://def.seegrid.csiro.au/sissvoc/isc2012/resource?uri=http://resource.geosciml.org/classifierscheme/ics/2012/ischart) ([Example resource as RDF: Middle Jurassic; URI=http://resource.geosciml.org/classifier/ics/ischart/MiddleJurassic](http://def.seegrid.csiro.au/sissvoc/isc2012/resource.rdf?uri=http://resource.geosciml.org/classifier/ics/ischart/MiddleJurassic))

[Linked Open Data of Ecology; uses DwC, FOAF, GEO, LODE](http://ecowlim.tfri.gov.tw/lode/) ([example resource](http://test.ckan.org/lv/dataset/linked-open-data-of-ecology/resource/b27bdda0-5f10-4419-9da2-69e513152582))

[TaxonConcept; uses DC, FOAF, BIBO, TaxonConcept, SKOS, and others](http://www.taxonconcept.org/) ([example resource](http://lod.taxonconcept.org/ses/dwAmr.rdf))

[uBio; uses DC and locally defined predicates](http://www.ubio.org/) ([example resource](http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:463007))

[Virtual International Authority File (VIAF); URIs for persons](http://viaf.org/) ([http://viaf.org/viaf/27063124 example resource](http://viaf.org/viaf/27063124.rdf))


---

Questions? Comments? Contact [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide)