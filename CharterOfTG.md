# RDF/OWL Task Group Charter #
The RDF/OWL group is a task group of the [TAG](http://www.tdwg.org/activities/tag/) (the TDWG Technical Architecture Group).

## Co-convenors ##

  * Joel Sachs
  * Steve Baskauf

## Core Members ##

  * Kevin Richards
  * Cam Webb
  * Nico Franz
  * Mark Schildhauer
  * Hilmar Lapp
  * John Deck
  * Paul Murray
  * Dag Endresen
  * Paul Morris
  * Greg Whitbread
  * Ben Richardson
  * ... Please join us!

## Motivation ##

[Semantic web](http://www.w3.org/standards/semanticweb/) approaches to data discovery and integration have gained increasing traction across many data-driven domains and sciences. Biodiversity information is no exception to that. The [Biodiversity Information Standards (TDWG)](http://www.tdwg.org/about-tdwg/) organization has embraced semantic web approaches in recent years, but the practices, patterns, and conventions that would further our data and knowledge discovery objectives are still being openly debated, often contentiously.  At the same time, semantic web usage patterns continue to evolve as the technology becomes more widely adopted and faces new requirements both from data publishers as well as consumers.

These issues are far from unique to the field of biodiversity data and information, and are actively being addressed by a large and engaged  community of expert practitioners and researchers, a large part of which organizes itself in W3C standards initiatives, domain-agnostic semantic web events, etc.  By necessity, the pattern and best practice recommendations resulting from these efforts are typically documented using general-purpose use-cases, data, and query applications, which often fail to relate in obvious ways to biodiversity science-driven use-cases of data publication and consumption.  As a result, there is considerable confusion and uncertainty about how to apply general semantic web publishing patterns in biodiversity science applications, and how to stay on top of the rapidly evolving landscape of applicable technologies and conventions.

This Task Group will serve as a bridge from and to semantic web research, development, and standardization initiatives. The group aims to leverage advances made in those initiatives to lower the barriers to wider adoption and application of semantic web approaches within biodiversity science, and to feed back to the larger semantic web community the technological and standards needs arising from biodiversity data.  The group will demonstrate and validate its findings through practical experimentation with [RDF](http://www.w3.org/TR/rdf-primer/) and [OWL](http://www.w3.org/TR/owl-guide/) to represent, integrate, and query biodiversity data in ways that meet actual needs of biodiversity data providers, aggregators, and consumers.

## Goals ##

The goals of the RDF/OWL Task Group will continuously evolve in response to technology and standards advances, but will initially include the following:

  1. Develop **[use-cases](http://en.wikipedia.org/wiki/Use_case) and [competency questions](http://marinemetadata.org/references/competencyquestionsoverview)** that include tests of biodiversity data discovery, exchange and semantic reasoning.
  1. Experiment with a variety of technical and RDF/OWL modeling approaches to addressing the use cases.
  1. Develop documentation (guides and working examples) to make it easier for others to participate and contribute.
  1. Enable the use of [GUIDs](http://www.tdwg.org/standards/150/) (specifically [HTTP URIs](http://www.w3.org/TR/cooluris/)) by developing a consensus on the appropriate **[class/rdf:type](http://www.w3.org/TR/rdf-primer/#schemaclasses) designations for biodiversity resources** and the basic metadata properties (described using RDF or OWL) that are needed to describe the resources identified by those GUIDs
  1. Identify specific ontologies and vocabularies for use in the domain.
  1. Develop **recommendations for linkage models** to other domains of biodiversity data (taxonomic complexity, observations, phylogenies, etc), including the review of existing ontologies and vocabularies, and the identification of new ontology development needs.

In pursuing these, the group will focus on the practical with a goal of deployment in the **near term**. As a consequence, priority will be placed on leveraging existing vocabularies, ontologies, conventions, and other resources whenever possible.

## Deliverables ##

Our primary deliverables consist of on-line documents comprising i) use cases and competency questions covering a range of biodiversity informatics; and ii) well documented and validated examples of using RDF/OWL and [SPARQL](http://www.w3.org/TR/rdf-sparql-query/#introduction) to address those use cases. We will deliver these to the TAG and to the broader community within a one year time frame.  All documents will be published so that they facilitate continued community maintenance.

## Becoming Involved ##

  * The TDWG community includes users from across the spectrum of biodiversity informatics who can share knowledge and practical experience in the application of RDF.  Anyone with an interest in applying RDF in a biodiversity context is welcome to be involved in the group.
  * Persons having practical experience creating RDF, using RDF for metadata integration, and performing reasoning tasks would be valued participants in the group.
  * Because the focus of this group is on practical applications, metadata providers, consumers, and aggregators can make important contributions to the group, particularly through contribution of use cases and testing of models.

Please contact one of the convenors to register your interest.

## History/Context ##

In its [2006 Roadmap](http://www.tdwg.org/uploads/media/TAG_Roadmap_01.doc) the [TDWG Technical Architecture Group (TAG)](http://www.tdwg.org/activities/tag/) described a three-pronged approach to the development of an infrastructure that would facilitate interoperability among TDWG standards and other standards outside the TDWG domain.  This approach consisted of: a Semantic Hub (a type catalog or ontology), a system of Globally Unique Identifiers (GUIDs), and well defined data exchange protocols.

There is broad sentiment within TDWG that we should pursue this approach via the Semantic Web/[Linked Open Data](http://linkeddata.org/). We can identify resources globally using HTTP URIs, describe the resources using RDF, and transfer information across the Internet using the [HTTP protocol](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol). The primary challenge  for implementation is arriving at a common understanding of how RDF should be used to describe biodiversity resources. Thus, we see the group as paving the way for implementation of the [latest version (2008) of the Roadmap](http://wiki.tdwg.org/twiki/pub/TAG/RoadMap2008/TDWG_TAG_Roadmap_2008.pdf).

## Summary ##
The main output of this task group will be well documented and validated examples of using and querying RDF / OWL to address a wide range of biodiversity informatics use cases. We will collect use cases and competency questions, and make them easily available for reference and update on a wiki. Our approach will focus on experimenting with a variety of semantic web tools and patterns for addressing the use cases, while documenting the lessons learned. Since semantic web usage is still rapidly evolving, our deliverables will be living documents that can be maintained in a collaborative and distributed manner.

## Resources ##

Online resources used and promoted by the group, including Wiki, mailing list, presentations, tutorials, repository.
  * [Code and Interest Group on Google Code](http://code.google.com/p/tdwg-rdf/)
  * [Wiki](http://code.google.com/p/tdwg-rdf/w/list)
  * Development platform ("sandbox"): http://tdwg-rdf.phylodiversity.net/