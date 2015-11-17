# Under what circumstances is it more beneficial to use many classes vs. few in a model? #

The eventual purpose of this page is to provide guidance for deciding whether it is more beneficial to create a model with many classes or few classes having many instances.  At this point I'm going to paste in some information from posts to the email list.  Hopefully somebody will take up the task of creating a more useful and user-friendly resource.

Note on 2013-11-09: this topic reared its head again last month on tdwg-content http://lists.tdwg.org/pipermail/tdwg-content/2013-October/003166.html which caused me to look up the old "[Subclass or not?](http://wiki.tdwg.org/twiki/bin/view/TAG/SubclassOrNot)" post: which either Bob Morris or Roger Hyam (or both) wrote.  I can't remember...

## Situations where fewer classes and more instances would be beneficial ##
From Steve Baskauf's post of 2012-03-11:

I have had an opportunity to twice read through the draft paper that Hilmar mentioned: "Mapping and linking life science data using RDF" which is at
https://docs.google.com/a/nescent.org/document/d/1XzdsjCfPylcyOoNtDfAgz15HwRdCD-0e0ixh21_U0y0/edit?hl=en_US and which I believes originates from http://lists.w3.org/Archives/Public/public-semweb-lifesci/2011Dec/0022.html .

There were a few areas of this paper which I understood to be relevant to issues that have come up previously on the tdwg-content email list.  The issue that I'm talking about is whether it is "better" to model domain components as classes or instances.  In the thread which begins at http://lists.tdwg.org/pipermail/tdwg-content/2011-May/002388.html I try to make the case that it makes more sense to model the biodiversity realm as 7 classes rather than as 13.6 million classes.  There were a couple places in the paper which I took to be relevant to this issue.  One was in question Q14:

"In order to support automated reasoning, it is important that linked data creators consider carefully which entities they model as classes and instances. The discussion of what is best modeled as a class vs an instance is outside the scope of this W3C Note but is covered in resources such as (Allemang & Hendler 2008). Typical practice by linked data developers has tended to describe most data as an instance of some ontological class and to use classes as a values in the metadata for a graph; for example to indicate that a particular class of data is being provided in the data set."

The reference to Allemang and Hendler isn't very specific, but I'm guessing they are talking about the section in chapter 14 under "Common Modeling Errors" entitled "Rampant Classism" which is related to problems caused when entities are unnecessarily modeled as classes rather than as instances (= individuals sensu OWL).  The quote I pasted above does not go into detail, but "typical practice by linked data developers has tended to describe most data as an instance of some ontological class" and the Allemang and Hendler reference leads me to believe that the writers of the paper are suggesting that fewer classes and more instances is the most common model, at least for the type of wholesale relational database conversion that is discussed a lot in this paper.

In question Q2, the statement is made: "Tools that map RDB into RDF, like D2R or Virtuoso, provide an automated process to generate a mapping file (Sahoo et al. 2009), which converts every table into a class.  For tables with a large number of columns this strategy can translate into a significant reduction of the initial time investment required for converting the contents of an RDB."  I consider this approach to be consistent with the statement made in Q14 which I interpret as the following.  A typical practice would be to have relatively few classes, with database tables representing classes.  The columns represent the properties and the instances of the class would be represented by the rows.  I am guessing that this kind of model would be appropriate for most of what typically constitutes databases in the traditional TDWG realm, i.e. tables for taxa and occurrences with their properties described by Darwin Core terms.  More normalized (less flat) databases may also include more tables for additional Darwin Core classes such as Identifications, Locations, and Events.

## Situations in which it is beneficial to have many classes ##
From Steve Baskauf's post of 2012-03-11:

In Bob Morris' response to my "7 classes rather than as 13.6 million classes" emails http://lists.tdwg.org/pipermail/tdwg-content/2011-May/002398.html , he cited three papers where people were actually doing reasoning on real data.  The last paper (Calder et al. 2009, which mentions the "excess of classes" problem) uses a relatively small ontology.  But the first two (Mungall et al. 2010 and Blondé et al. 2011) involve analysis of OBO ontologies ( http://obofoundry.org/ ).  OBO Ontologies can have hundreds of classes because they are used to express relationships such as partOf,  isLocatedIn, isA, participatesIn, derivedFrom, etc. among a complex collection of classes like "apoptosis", "cell death", "shoot axis", "shoot apex", "abnormal tooth development", "abnormal tooth morphology", etc. etc.  In contrast to the situation of Darwin Core where there are relatively few classes and relatively more properties per class, an OBO ontology like Plant Ontology ( http://www.plantontology.org ) has hundreds (thousands?) of classes with only 7 basic relationship types (i.e. properties that relate the classes).  I believe that these ontologies are designed primarily to facilitate reasoning as opposed to be used for marking up metadata.

Within the biodiversity realm, this kind of ontology could be useful to describe the more complex relationships among classes of things that we are having trouble fitting into our 6 or 7 Darwin Core "boxes", e.g. living specimens, preserved specimens, tissue samples, observations, individuals, populations, DNA sequences, etc.  which would have the kind of "object property" relationships I mentioned above like "isA", "derivedFrom", "partOf", etc. rather than the more mundane database column headings like "lifeStage", "recordedBy", "verbatumElevation", etc.  This kind of complex ontology also might be useful in the taxon/taxonConcept realm.

## An approach the plays it both ways ##
From Paul Murray's post of 2012-03-13:

Once again, if you are interested in playing with more-or-less real data:

At biodiversity.org.au, we produce TDWG Taxon Concept objects for our taxa. We **also** generate a class for each accepted taxon. Thus for taxon concept
> http://biodiversity.org.au/apni.taxon/298605

there also exists a uri
> http://biodiversity.org.au/apni.taxon/298605#Instance

which can be use to declare that something is-a Dodonaea viscosa. There are no type restrictions, so how you use it is up to you.

I also declare that something belonging to this class is the same as it having an "ibis:instanceOf" the taxon concept.

Thus:
> :my-specimen ibis:instanceOf <http://biodiversity.org.au/apni.taxon/298605>
implies
> :my-specimen a <http://biodiversity.org.au/apni.taxon/298605#Instance>

and the reverse. The use of a predicate external to other vocabularies is deliberate - it bypasses a variety of philosophical arguments over the meaning of basic terms in other vocabularies. When working with your data you can inform your reasoner that ibis:instanceOf is a subproperty of "is-a" in some other vocabulary, or not.

What I **don't** include are subclassing rules that would imply a taxonomic tree -

> <http://biodiversity.org.au/apni.taxon/298605#Instance> is subclass of <http://biodiversity.org.au/apni.taxon/50016#Instance>

I decided to not do this on the grounds that … well, I was concerned that including it might make things explode even if you are not trying to do things such as "what individuals are of type <Animalia#instance> ?".  However, the absence of these subclassing rules means that these classes don't really "do" anything much apart from being there. Sparql helps here - you can break the data up into silos by putting them in named graphs, and include the information that you want to use, as opposed to linked data which is all or nothing.

As for the choice of "#Instance" for the URI:
  * I didn't want to create a whole new namespace for these classes,
  * I wanted the taxon concept object and the taxon class to be paired, somehow
  * I needed somewhere where I could put thousands of these things
  * I did not want to "pun" the taxon URI itself

It might be worthwhile putting the reflexive properties in, too, allowing reasoning over conditional property chains.

Another consideration is distinguishing, somehow, between something being an instance of a taxon becuase it was identified as such, and something being an instance of a taxon because it was identified as being an instance of a  subtaxon. Let's call it "classified-as" rather than "instance-of" - which makes it clear that what is happening is the result of some classification.

Thus:

http://biodiversity.org.au/apni.taxon/298605#Instance is a subclass of http://biodiversity.org.au/apni.taxon/298605#ClassifiedTo
http://biodiversity.org.au/apni.taxon/298605#ClassifiedTo  is a subclass of http://biodiversity.org.au/apni.taxon/50016#ClassifiedTo

I don't need to explain that the classification in question is APC, because that taxon is an APC taxon.

The separation of "instanceOf" and "classifiedTo" also means that "instanceOf" can be declared to be a functional property. When you need to get the taxon name for a specimen (or whatever), there is a property that will get you just one of them.

Finally, in addition to adding the subclassing rules to the taxonomic tree, another thing that suggests itself is adding "disjoint classes" declarations. This becomes problematic in the case of hybrids, so some care will be needed. The declaration of "equivalent classes" between taxonomies that are in fact incompatible will result in a reasoner declaring that the ontology is inconsistent. Perhaps, ultimately, that's the pay-off: that's the bit that we would want an automated reasoner **for**.