# Summary and links to a thread about the Open Annotation data model, the Darwin Core ResourceRelationship terms, and the TDWG TaxonConcept ontology #


# Background #
On 2013-02-25 a thread began on the TDWG RDF Task group email list regarding the Open Annotation data model (http://www.openannotation.org/spec/core/) and the similarities between it and parts of TDWG vocabularies.  In particular, the text-based dwc:ResourceRelationship terms (http://rs.tdwg.org/dwc/terms/#relindex) and tc:hasRelationship term and its possible values from the TDWG TaxonConcept ontology (http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.rdf) use a similar approach to modeling the relationships between resources.  The diagrams and table at http://code.google.com/p/tdwg-rdf/wiki/OpenAnnotationAndTDWG compare the three sets of terms.

# Some posts from the TDWG RDF email list related to this issue #

Steve Baskauf's initial post noting the similarities among the three vocabularies https://groups.google.com/d/msg/tdwg-rdf/eTATmyyE8a0/Jta39nkXyYgJ

Specific example laying out the difference between expressing a relationship between two taxa using a single triple vs. an expressing a relationship by creating a tc:hasRelationship instance linked to the two taxa.  https://groups.google.com/d/msg/tdwg-rdf/eTATmyyE8a0/NtT8vp27M6IJ

John Deck notes that BiSciCol is interested in expressing relationships using the OA core.  https://groups.google.com/d/msg/tdwg-rdf/eTATmyyE8a0/HTvfBlGSYuoJ

Steve Baskauf provides an example of how the OA terms could be used to represent a dwc:ResourcRelationship instance and asks whether it would be a valid use of the OA model. https://groups.google.com/d/msg/tdwg-rdf/eTATmyyE8a0/4yZwR6UGlngJ

Bob Morris says he thinks it is not an abuse of OA and suggests a possible way to use SKOS terms to describe that the relationship is narrower than the oa:Motivation oa:linking .  https://groups.google.com/d/msg/tdwg-rdf/eTATmyyE8a0/Et0SSxEc6NYJ

Éamonn Ó Tuama notes that the VoMaG (http://community.gbif.org/pg/groups/21382/vocabulary-management/) term wiki is set up for handling SKOS schemes. https://groups.google.com/d/msg/tdwg-rdf/eTATmyyE8a0/ubWXVqgr59UJ

Steve Baskauf forwards a reply from Rob Sanderson, one of the OA editors, who says that although the OA is framed in terms of annotations of information resources, it is broad enough to include the sorts of non-information resources (specimens, taxa) that would be related by the dwc:ResourceRelationship class terms.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/sfOu-v_Y4GkJ

Paul Morris provides an alternative way to annotate a simple triple. https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/ewJG0pu9V-UJ

Hilmar Lapp says that common sense says not to use oa:Annotation to say something that could just as well be said in a triple directly. https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/sazAKg8t8JQJ

Steve Baskauf notes that the TDWG TaxonConcept ontology uses an annotation-like structure to document the relationship between tc:TaxonConcept instances and asks why. https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/g_h7R4GrynoJ

Nico Franz comments that the TaxonConcept ontology needed to document person-specific assessments of relationships between concepts.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/-r-HMLMudMAJ

Bob Morris notes that OA provides a mechanism for documenting provenance. https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/I6hPLPtn1qkJ

Steve Baskauf comments that the extent to which people are going to care about the provenance is going to depend somewhat on how taxon concepts are going to be managed (centralized vs. aggregation from many smaller sources).  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/cOdstpLHoYUJ

Éamonn Ó Tuama asks why reification is not adopted over special schemes for annotation/provenance.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/cWr7InFkzOEJ

Hilmar Lapp agrees that reification has fallen out of favour due to problems it causes with SPARQL queries.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/6HiBBv--ObwJ

Rod Page thinks that documenting provenance is probably the reason for structuring the taxon relationships the way they are modeled in the TDWG TaxonConcept ontology.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/wPjVnNyxGiMJ

Jessie Kennedy confirms that documenting provenance was a central reason for the structure of TCS and its RDF successor (the TDWG TaxonConcept ontology).  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/CTOhXDt3yRkJ

Jessie Kennedy notes that simply using subclassing or assuming that genus placement is correct is an oversimplification and does not adequately record provenance https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/6MPuLSGd_kYJ

Rod Page feels that the TaxonConcept vocabularies are over-engineered.  He feels that useful TaxonConcepts are connected to other resources that "we can compute over" e.g. GBIF and NCBI. https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/6Lo0pSlkyVUJ

Greg Whitbread disagrees. He says that GBIF and NCBI provide an ephemeral guess.Science requires vocabularies which can support research and links to original work.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/yH-O-cWuQZ8J

Rod Page replies that he sees classifications simply as tools for navigation and organising data. https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/dvmXZV-iC-IJ

Steve Baskauf summarizes: 1. the structure of the TDWG TaxonConcept ontology allows for the tracking of provenance and linking of the assertion to other resources.  2. The TaxonConcept ontology needs to be kept because it provides a means for documenting relationships between taxa and because it's being used.  The "market" will decide if it or some other system is the best way to document the relationships.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/I6_HOxaSzI8J

Hilmar Lapp posits that a taxon concept is anything that a person or group asserts to represent a taxon compliant with a code.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/-abF_Poo9Q0J

Hilmar Lapp says VoMaG must care about provenance and suggests the PROV model.  He also notes that it would be counterproductive to turn every triple into an object.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/jWsJ6CKn0zcJ

Steve Baskauf refers to a previous thread and says that without a careful definition there will be a lot of disagreement about what the nature of a "taxon concept" or "taxon".  The TaxonConcept ontology provides a well-defined tc:TaxonConcept class.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/iJg169xY8j0J

Greg Whitbread reviews how APNI uses the TaxonConcept ontology.  Their main purpose is not to model taxa but to deliver persistent, linkable nomenclatural and taxonomic objects.  He describes some deficiencies of tc:hasRelationship.  There is a failure to distinguish accurately among different kinds of nomenclatural/taxonomic resources.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/3_XZBTSoZ5YJ

Steve Baskauf notes that there may be some valuable parts of the TaxonConcept even if other parts are flawed.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/Pq08ogynqa8J

Mark Schildhauer is a bit frustrated that this discussion wanders through a broad Knowledge Representation (KR) space.  He asks if there is a set of documented use cases which would clarify and prioritize the goals of vocabulary development.  He suggests ways to focus the discussion: 1 record use cases.  2 concretize needed specific semantic capabilities. 3 decide how to achieve this with RDF vocabularies or something more expressive. 4 build vocabularies using patterns captured on a wiki.  LOD exposure might be a starting point, while more advanced challenges (e.g. expressing and querying taxon concepts) ma require more advanced inferencing.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/P9388MarNVkJ

Steve Baskauf refers to the task groups use case page (http://code.google.com/p/tdwg-rdf/wiki/UseCases) and notes the need for work such as Mark suggests to be done by the experts in the group.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/oB9-W5CTBCUJ

Nico Franz adds an item to the use case list regarding semantically enhancing taxonomic and phylogenetic revisions.  https://groups.google.com/d/msg/tdwg-rdf/Z6p1Q02v-cQ/cfGP4xgeIMMJ