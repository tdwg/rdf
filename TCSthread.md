# Summary and links to a thread related to TCS and Taxon Concepts #

# Background #

On 2012-11-01 a thread began on the TDWG TAG email list regarding the Taxon Concept Transfer Schema (TCS).  The TCS is a TDWG Current (2005) Standard (http://www.tdwg.org/standards/117/ viewable as a pdf at http://bioimages.vanderbilt.edu/pages/TCS-Schema-UserGuide-v1.3.pdf ).  The TCS specifies the structure for XML documents to be used for the transfer of defined concepts.  It does not provide any guidance about how to represent taxon concepts in RDF.  However, the Taxon Concept Ontology component of the TDWG Ontology (http://rs.tdwg.org/ontology/voc/TaxonConcept viewable in a browser at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.rdf ) is based on TCS and provides a means to express TCS as RDF.

# TDWG TAG mailing list and TDWG RDF Task Group mailing list thread posts relevant to TCS as RDF and broad issues that would impact RDF #

Question posed by Tony Rees asking whether any users have real-world experience using TCS
http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002513.html

Rod Page notes that some providers use vocabularies for taxonomic names, others use vocabularies for taxonomic concepts, and others such as Darwin Core blur the distinction.  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002514.html

Greg Whitbread notes that the Atlas of Living Australia, National Species List (ANA-NSL) uses the TDWG Ontology (specifically the Taxon Concept part) as a basis for LSID, RDF, and JSON services. http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002515.html

Steve Baskauf notes that although the TDWG Ontology has an "unfinished" feel, the Taxon Concept part of it appears to be complete and usable.  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002516.html

Rich Pyle asks for feedback from users of TCS, the TDWG Taxon Concept Ontology, and the Darwin Core dwc:Taxon class terms.  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002517.html

Kevin Richards reports use of the Taxon Concept Ontology in LSID resolvers that resolve names.  (Actually some of these use the Taxon Name Ontology part of the TDWG ontology, which is actually a separate component at http://rs.tdwg.org/ontology/voc/TaxonName viewable in a browser at http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonName.owl )

Nico Franz reports on current NSF projects dealing explicitly with taxon concept representation and integration.  He points out the weakness of TCS in defining relationships between concepts.  (actually a posting to a cross-post on the TDWG RDF email list) https://groups.google.com/d/msg/tdwg-rdf/ILZ4R07mfhw/XT7fy15kQ4wJ

Jessie Kennedy (author of TCS) provides a short history of TCS at http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002524.html

Rich Pyle enumerates things that he things TCS "got right" and describes the approach involving "atomized" taxon name usage (TNU) instances.  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002526.html

Tony Rees discusses the advantages associated with the ability to query multiple taxonomic databases.  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002528.html

Rod Page discusses the pros and cons of depending on the GBIF classification  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002529.html

Nico Franz describes three expected actions of concepts.  He says tools are needed to import existing concept hierarchies. https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/iJgh5zI-bCIJ

Rich Pyle responds to Nico's post (but I don't think it went out on the list - it's included in Nico's subsequent response) by describing a Taxon Name Usage Instance (TNU).  A TNU is a snapshot in time and can include Code-governed Nomenclatural Acts (small subset) as well as things as vague as a newspaper reference or label annotation.  He says it would be nice to have a registry of TNUs that represent Taxon Concepts (TNUs that are defined in referenceable literature?) as well a mechanism for asserting how concepts map to each other.

Nico responds (quoting the above email) describing how he thinks his description of taxon concepts maps to Rich's.  He says describes a situation where a TNU can "rise" to become a taxon concept via a mapping.  Thus it may be premature to define things to soon or too narrowly.  https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/OV7TB8ctTs8J

Rod Page created a graphical representation of the model that underlies Zoobank. https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/kBsh0oRIF9YJ blog post at http://iphylo.blogspot.co.uk/2012/11/zoobank-data-model.html

Nico Franz states that he believes that the set-theory relationships can be worked out through an SQL database and do not require an ontology-like environment.  He notes the desirability of a taxonomy submission tool with a pleasant front-end.  https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/I1ldlSOqjDYJ

Steve Baskauf expresses the opinion that what Rich wants to do with TNUs could and probably should be done using the TDWG Taxon Concept ontology.  https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/41J-e0lRJIQJ and followup https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/4KBXOW1NzwwJ

Rich Pyle responds to Rod's blog post and discusses features of the GNUB data model.  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002541.html

David Remsen makes a number of points about the use of the term "taxon concept".  People don't understand it.  He objects to using sensu for things that don't resolve to anything that defines a taxon.  A taxonomic concept must provide evidence of its circumscription.  Ideally that would include machine-comparable information, but specimens, original descriptions, morphological characters, geographic distributions, and synonymy are means of circumscription.  http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002542.html

Rich Pyle responds to Steve's email.  He notes that a TNU must have documentation.  He notes that it may be possible to infer the concept a person had in mind when assigning a name in a specimen determination, but most of the time the TNU will probably not be matched with a clear concept.  He endorses the idea of using TCS 1.2 as the basis for a more advanced version. http://lists.tdwg.org/pipermail/tdwg-tag/2012-November/002543.html

Steve Baskauf comments about the documentation of the TDWG Taxon Concept ontology and TCS.  He proposes using tc:hasName and tc:accordingTo as properties which define tc:Taxon (or tc:TaxonConcept) instances.  He provides a concrete example using a real name URI from uBio and a real reference URI which is an HTTP-proxied DOI.  He shows how the RDF graph would be represented graphically and marked up in RDF/XML and RDF/turtle.  He discusses how differing views on taxon concepts and TNUs would be handled under this model. He asserts that Darwin Core is not up to handling complex non-"flat" situations like this.  He proposes that the TDWG Taxon Concept and Taxon Name ontology terms be used instead of Darwin Core when represented as RDF.  He requests feedback on this proposal.  https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/OA8OalRFAHkJ

Nico Franz replies that he thinks this is a good path to take and ... "To the extent that communication succeeds relevantly (like for instance we can identify and protect a "natural cluster" of things out there to a satisfactory degree), we can call it "real" or "construct".. - the success remains and our model needs to be able to accommodate successes that inherently involve semantic vagueness. ..."  https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/D53JBKtxQGUJ

Rich Pyle replies to Steve's email.  He distinguishes between name strings which can be entirely represented as UTF-8 string and "name objects" which are more abstract resources which can themselves have properties.  https://groups.google.com/d/msg/tdwg-rdf/CMfwf10Ozpo/GW2GaWW8C78J (first forwarded email)

Rich Pyle provides additional responses to Steve's email.  He notes that when TCS was adopted, there was an understanding that there would eventually be a TCS 2.0 but that never happened.  He notes that it is the documentation (reference) associated with a taxon that gives it "reality" rather than just being an idea in somebody's head.  He notes that he things tc:hasName is ambiguous because it is not clear whether it points to a name string or a "name object", which he says is a TNU.  He questions the need for a URI to represent a name string, since a string can be represented as a literal.  He wonders if the terms in Darwin Core (including the ResourceRelationship terms) are enough to facilitate RDF without the need to invoke the TDWG TaxonConcept ontology.  https://groups.google.com/d/msg/tdwg-rdf/CMfwf10Ozpo/GW2GaWW8C78J (second forwarded email)

Steve responds to Rich's emails.  He questions whether Zoobank actually avoids creating a GUID for things that already have them since it doesn't use DOIs as the GUID in cases where they are provided.  Steve suggests that we should decide on the nature of a class by examining the properties it has (octopus analogy), then asks whether Rich's "name object" is a tn:TaxonName or a tc:TaxonConcept.  He says that based on Rich's description of a "name object", tn:TaxonName rdfs:subClassOf tc:TaxonConcept.  Steve summarizes that he believes that the question is whether the TDWG Taxon Concept and Taxon Name ontologies are adequate to describe resources of interest to the TDWG community.  https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/MqFSQF6V74kJ

Bob Morris notes that W3C has a working draft for an RDF vocabulary (http://www.w3.org/TR/Content-in-RDF10/ ) that can provide URIs for strings.  The overarching class is http://www.w3.org/2011/content#Content or cnt:Content .
https://groups.google.com/d/msg/tdwg-rdf/Td_Rhb9BG4g/SgJj7SE281sJ

Rich replies that ICZN (sponsor of ZooBank) cannot rely on DOIs to be around 100+ years from now and therefore mints a UUID which he believes has greater longevity.  He explains details of how ZooBank cross-references and avoids redundancy.  He explains how a complex TNU implies many other TNUs that would be cross-referenced to it.  He says that a tn:TaxonName is a "name object".  He says that a tn:TaxonName (equivalent to his "name object" which has the technical name: Protonym) is a subclass of TNUs. He says that the timing is good to work out a model since they are in the process of building related services that would greatly benefit from a more robust taxonomic ontology. https://groups.google.com/d/msg/tdwg-rdf/CMfwf10Ozpo/GW2GaWW8C78J (third forwarded email)

Steve responds more.  Possibly the only compelling reason to represent a name string with a URI is that literals can't be the subject of RDF triples.  The importance of this would depend on whether there is anything else to "say" about the name string.  He gives an example where their is no physical documentation of a name use.  He notes that there are problems with using the ResourceRelationship terms in RDF but defers on discussing them in this thread.  He notes that there are technical problems with using the DwC "ID" properties.
https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/QCCYI1icYCkJ

Rich replies that he thinks we are in full or near-full agreement.  He thinks that perhaps GNUB references to name strings should point to a GNI (Global Names Index) instance URI.  He thinks that creating some kind of sub- or superclass relationships between tn:TaxonName and tc:TaxonConcept might be productive.  Both of these classes could be framed as flavors of TNUs.  He notes that GNUB has a "Personal Communication" reference which can be used to create a reference anchor for TNUs that don't have more concrete representations.
https://groups.google.com/d/msg/tdwg-rdf/CMfwf10Ozpo/GW2GaWW8C78J (fourth forwarded email)

Éamonn Ó Tuama notes that this discussion is related to issues the Vocabulary Management Task Group (VoMaG; http://community.gbif.org/pg/groups/21382/)needs to consider.  He notes that the biodiversity domain is like many octopuses with tentacles intertwined.
https://groups.google.com/d/msg/tdwg-rdf/tMcUkoDNgcI/7azjuKOOC6oJ

Steve attempts to summarize the status of the discussion.  He concludes that it may not be necessary to come to a community consensus on a model for taxon concepts, taxon names, name strings, etc. IF there is consensus that a centralized organization (e.g. GNUB) will handle all of the metadata.  In that case, the organization can simply create an RDF model that fits with their database model and inform users what that model is so that they can understand RDF dumps or run SPARQL queries on the metadata held by the organization.  A community-sanctioned model is really only important if many separate organizations are going to create their own taxon concept/taxon name metadata sets which must be reconciled and aggregated (similar to the situation of occurrences documented by many separate museums).  If there is a centralized system, then Darwin Core dwc:Taxon class terms may become more important as a means to mark up metadata that would be transmitted to the centralized organization.
https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/mQrl1zV8I48J

Steve records his thoughts on the relationships among protonyms, tn:TaxonName instances and tc:TaxonConcept instances as described by Rich.  He also discusses the availability of a property term for name strings and what the appropriate object is for tc:hasName.
https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/AUk0YvbYp1oJ

Rich Pyle made a couple of clarifications.  In addition to protonyms, "New Combination" instances qualify as name objects.  He considers tc:hasName a "dangerous property" because Taxon Name is so poorly defined.
https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/dU6HYjxw1UAJ

Steve replies that tc:hasName will probably have to remain poorly defined for the moment, but it or some other property is needed to collect general Taxon Concepts to more basic forms of Taxon Concepts such as protonyms.
https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/PmW5_7YqoaQJ

Rich says that the use Steve described for tc:hasName is effectively "hasProtonym".  He wonders in what other way one would use tc:hasName.  Steve replies that although he doesn't know what else could be the object of tc:hasName other than a protonym instance, one could get examine properties in the TDWG Taxon Name ontology which have tn:TaxonName as their domain and see which ones don't apply to protonyms.  The non-applicable ones could inform us on possible other uses of tc:hasName.
https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/4LHvDqND9C0J

Éamonn Ó Tuama comments that RDF can also be used simply as a format to define and encode vocabularies themselves.
https://groups.google.com/d/msg/tdwg-rdf/E77vdpH4tj0/uoLE8jW7V4EJ

Bob Morris notes that there are actually two similar files (TaxonConcept.rdf and TaxonConcept.owl) in the Google Code repository which describe the TaxonConcept ontology and comments that it is probably a dangerous situation.
https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/B4NJBvxoMkAJ

Steve Baskauf notes several differences between the two files and says that after investigation he believes that TaxonConcept.rdf is the "real" file (at least the one served when terms are dereferenced for rdf+xml).
https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/-muFUxB7tBQJ

# For further (painful) reading #

A long summary of a variety of posts from the tdwg-content email list between 2009-10 and 2011-02 which include some on the topic of Taxon Concepts and RDF representations.  A text search on the page for "Taxon Concept" will jump you to some entry points. http://code.google.com/p/darwin-sw/wiki/TdwgContentEmailSummary

An attempt to summarize Taxon Concept issues in the context of the development of Darwin-SW is at http://code.google.com/p/darwin-sw/wiki/ClassTaxon .  You are on your own to separate the objective background material from the material shamelessly promoting the Darwin-SW Ontology.