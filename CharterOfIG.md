# Resource Description Framework (RDF) Interest Group Charter (Draft) #

NOTE: this is an obsolete draft.  To view the approved charter, see the [Charter of Task Group](CharterOfTG.md).

(see http://www.tdwg.org/activities/documentation/templates/ or the Downloads area for the charter template upon which this is based)

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
  * ... Please join us!

> (TDWG IG guidelines: “Please provide an indication of their role within the group where possible. Core members are not people who may have contributed in the past. This is not a credits list. Members of the group will be identified through the membership. Core members could explain to an outsider the purpose, justification and current activities of the group. Any core member could substitute for the Convener when required. It is acceptable to have a link to a web page here as this list may be volatile.”)

## Motivation ##

  * TDWG has embraced a semantic web approach to data discovery and integration for the last several years. Semantic web usage patterns have evolved over this period, and continue to evolve. Biodiversity data providers, aggregators, and consumers need examples of usage patterns that work in our domain, and that represent current best practice. The group will determine these usage patterns through experimentation, and will provide well documented examples of using RDF to represent biodiversity data, and SPARQL to query that data.

### Why is this group needed?  What is its niche? ###

  * Because metadata description and integration spans the range of interests within TDWG, there is no single existing Interest Group within which this effort can fall.
  * An RDF Interest Group can act as a bridge between the traditional interest groups within TDWG and groups outside TDWG which are focused on development of Linked Open Data (LOD) and the Semantic Web in a broader context.

> (TDWG IG guidelines: “Motivation should differentiate the group's activities from other TDWG groups and from groups in other standards organizations. Any historical reasoning should be placed in the 'History' field.”)

## Becoming Involved ##

  * The TDWG community includes users from across the spectrum of biodiversity informatics who can share knowledge and practical experience in the application of RDF.  Anyone with an interest in applying RDF in a biodiversity context is welcome to be involved in the group.
  * Persons having practical experience creating RDF, using RDF for metadata integration, and performing reasoning tasks would be valued participants in the group.
  * Because the focus of this group is on practical applications, metadata providers, consumers, and aggregators can make important contributions to the group, particularly through contribution of use cases and testing of models.
  * Please contact one of the convenors to register your interest.

> (“This section is required. How could an individual reading this help the group? What skills are currently in need? Who should be contacted?”)

## History/Context ##

In its 2006 ‘roadmap’ (http://www.tdwg.org/uploads/media/TAG_Roadmap_01.doc) the TDWG Technical Architecture Group (TAG) described a three-pronged approach to the development of an infrastructure that would facilitate interoperability among TDWG standards and other standards outside the TDWG domain.  This approach consisted of: a Semantic Hub (a type catalogue or ontology), a system of Globally Unique Identifiers (GUIDs), and well defined data exchange protocols.  Key to the functioning of this infrastructure is a common understanding of the types and properties used to describe resources.  This imperative was expressed in subsequent Roadmaps:

  * “Biodiversity research is typically carried out by combining data of different kinds from multiple sources. The providers of data do not know who will use their data or how it will be combined with data from other sources. The consumer needs some level of commonality across all the data received so that it can be combined for analysis without the need to write computer software for every new combination.” (2007 TAG Roadmap; http://www.tdwg.org/fileadmin/subgroups/tag/TAG_Roadmap_2007_final.pdf)
  * “If GUIDs are used to uniquely identify 'pieces' of data we need to have a shared understanding of what we mean by a 'piece of data' i.e. what kind of thing is it that a particular id applies to, a specimen, a person, an observation, a complete data set. We also need to have a shared understanding of at least some of the properties we use to describe these things.” (2008 TAG Roadmap; http://www.tdwg.org/fileadmin/subgroups/tag/TAG_Roadmap_2008.pdf)

The 2006 roadmap stressed that the Semantic Hub would work across multiple technologies.  One such technology is Resource Description Framework (RDF).  Since 2006, RDF has become an integral part of the development of Linked Open Data (LOD) and the Semantic Web.  LOD and the Semantic Web now span a broad section of the informatics universe and the biodiversity community has an opportunity to participate in this broader effort by adapting its standards to a form (RDF) that is compatible with this broader effort.

Because of the development of LOD and the Semantic Web, we can identify resources globally using HTTP URIs, describe the resources using RDF, and transfer information across the Internet using the HTTP protocol.  Thus a technology now exists to satisfy the three-pronged approach described in 2006.  The primary challenge remaining for implementation is arriving at a common understanding of how RDF should be used to describe biodiversity resources.

## Summary ##

The RDF Interest Group has the following goals:

  1. Develop **use-cases and competency questions** that include tests of data discovery, exchange and semantic reasoning.
  1. Experiment with a variety of approaches to addressing the use cases.
  1. Develop documentation (guides and working examples) to make it easier for others to participate and contribute.
  1. Enable the use of GUIDs (specifically HTTP URI GUIDs?) by developing a consensus on the appropriate **class/rdf:type designations for biodiversity resources** and the basic metadata properties (described using RDF) that should be returned when those GUIDs are resolved.
  1. Develop **recommendations for linkage models** to other domains of biodiversity data (taxonomic complexity, observations, phylogenies, etc), carefully critiquing existing ontologies and indicating where development of new ontologies may be needed.
  1. Meet the needs for standardized data exchange by adopting terms from **existing vocabularies and ontologies** that are suitable for use as data properties of biodiversity resources.  Whenever possible, terms should be taken from existing TDWG standards, or vocabularies that are well-known within the Linked Data and Semantic Web communities.
  1. Focus on the practical with a goal of deployment in the **near term**.  Accomplish this by leveraging existing vocabularies and ontologies whenever possible.


## Resources ##

  * Google Code site: http://code.google.com/p/tdwg-rdf/
  * Development platform ("sandbox"): http://tdwg-rdf.net/

> (“Links to the online resources used and promoted by the group - Wiki, mailing list, presentations, tutorials, repository.”)