## Background ##
The RDF/OWL Best Practices Task Group is part of Biodiversity Information Standards (TDWG; http://www.tdwg.org/).  Its purpose is to adapt TDWG vocabularies for use as RDF classes and properties and to integrate those resources with other well-known vocabularies and ontologies outside TDWG for use in describing biodiversity resources.

Group discussions are conducted via an email list hosted and archived at http://groups.google.com/group/tdwg-rdf .  Please visit that site to request an invitation to be added to the list.

The issues tracker is set up to handle specific best-practices recommendations, missing terms, etc.

Our [charter](http://code.google.com/p/tdwg-rdf/wiki/CharterOfTG) was approved by the TDWG executive at the 2011 meeting in New Orleans. At the [meeting](http://code.google.com/p/tdwg-rdf/wiki/TDWG2012MtgNotes) there was a discussion of the purpose of the group.  There was also a [survey](http://code.google.com/p/tdwg-rdf/wiki/Survey) to discuss the goals of the group.

We have also been tasked by the TDWG Executive Committee with examining the implications of adding new classes to the Darwin Core Type Vocabulary (http://rs.tdwg.org/dwc/dwctype/) in the broader context of clarification of the relationships among classes in the biodiversity realm (see [DwC issue 115](http://code.google.com/p/darwincore/issues/detail?id=115), [DwC issue 116](http://code.google.com/p/darwincore/issues/detail?id=116), and [DwC issue 117](http://code.google.com/p/darwincore/issues/detail?id=117)).

## RDF Sandboxes/Development platforms ##
The sandboxes are places to experiment with RDF. Everyone is invited to load data, load ontologies, and issues sparql queries into any (or all) of the sandboxes linked to below. If you'd like to offer a sandbox for use, add the link here. (Note: by providing a sandbox, you implicitly agree to support it.)

  * http://tdwg-rdf.phylodiversity.net/  Two triple stores available here, one based on 4store, one based on `AllegroGraph`. Hosted by Cam Webb.
  * http://82.96.149.133:8890/sparql An `OpenLink` Virtuosuo sparql endpoint. (You provide the graph.) Hosted by Natural Solutions.

## Beginner's Guide to RDF ##

The Beginner's Guide is intended to serve as an introduction for persons who are not already familiar with RDF and OWL, and as a reference for those who would like organized access to reference material on those topics. The information is presented with minimal formal language and includes functional examples from the biodiversity informatics community.

[Click here to go to the Introduction of the Guide](Beginners.md)

An [RDF Primer video](http://youtu.be/XAGifYBiXMY) was produced for the 2013 Semantics of Biodiversity symposium and may be a helpful first introduction to RDF.

## Semantics of Biodiversity Symposium at TDWG 2013 ##

Several members of the task group were actively involved in organizing a Semantics of Biodiversity Symposium at the 2013 TDWG Annual Meeting in Florence, Italy.  The slide sets from the talks given during the symposium are listed [here](Tdwg2013Semantics.md).

## Darwin Core RDF Guide approved ##

The Darwin Core RDF Guide was approved as an addition to the Darwin Core standard by the TDWG Executive on 2015-03-27.  Until the Guide is live on the Darwin Core website, see the [submission cover page](DwcRdf.md) for details.

## The Vocabulary Management Task Group (VoMaG) has released its report ##
The VoMaG was a Task Group under the Technical Architecture Group (TAG) of the Biodiversity Information Standards (TDWG). Its purpose was to address the best practices for the collaborative development and maintenance of vocabularies for the description of biodiversity resources.  Members of the RDF/OWL task group were contributors to the report.  The final report can be downloaded at http://www.gbif.org/resources/2246 .  The group website is at http://community.gbif.org/pg/groups/21382/vocabulary-management/ .  The proposed Knowledge Organization System (KOS) for biodiversity information resources is at http://kos.gbif.org/ .

## Mapping and linking life science data using RDF ##
  * Members of the W3C Health Care and Life Sciences Interest Group (HCLSIG) recently published the following article: Marshall, M. S. et al (2012) [Emerging practices for mapping and linking life sciences data using RDF - A case series](http://dx.doi.org/10.1016/j.websem.2012.02.003). Web Semantics: Science, Services and Agents on the World Wide Web 1-12. doi:10.1016/j.websem.2012.02.003.
  * This article is based on the draft W3C Interest Group note [Mapping and linking life science data using RDF](https://docs.google.com/a/nescent.org/document/d/1XzdsjCfPylcyOoNtDfAgz15HwRdCD-0e0ixh21_U0y0/edit?hl=en_US), which "summarizes emerging practices for creating and publishing healthcare and life sciences data as Linked Data in such a way that they are discoverable and useable by users, Semantic Web agents, and applications."

_The image on the page banner has the HTTP URI http://bioimages.vanderbilt.edu/baskauf/s3018 which can be dereferenced in a browser for human-readable metadata or by a semantic client for machine-readable metadata in the form of RDF_