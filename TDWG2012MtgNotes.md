# Meeting at TDWG 2011 of parties interested in the TDWG-RDF Task Group on 2011-10-18 #

Some of the people in attendance (reconstructed by Steve B.) were: Joel Sachs, Cam Webb, Dick Moe, Chuck Miller, Greg Riccardi, Paul Morris, Donald Hobern, Bob Morris, Greg Whitbread, Hilmar Lapp, Stan Blum, Olivier Rovellotti, Katja Seltmann, Kevin Richards, Jim Croft, Rod Page (via Skype), Steve Baskauf (via Skype, missed part of the discussion), and more people whom I didn't catch on the audio or notes.

## Notes: ##
Jim - tweeter
Bob Morris - Rapporteur

Joel: History - TDWG Content list activity around representing DwC in RDF (deVries, Baskauf). iEvoBio proposals by Morrison, Schindel and Deck/Sachs
> Rod Page proposes a challenge to TDWG - what is RDF good for (http://iphylo.blogspot.com/2011/10/tdwg-challenge-what-is-rdf-good-for.html)
> Presents goals of the group: code.google.com/p/tdwg-rdf/wiki. Desire to have sandbox(es) of triplestores. Immediate term: get engagement from a good portion of the participants, and rough agreement on strategy/scope


## Introductions ##
Chuck: Wants TDWG to tap into existing ontologies in other domains; a (draft) model from this group
Rod Page prize: Your project sucks!
Bob Morris warns not to prematurely close ontology to the world
Kevin Richards: for TAG - looking for TDWG to be more consistent with its approach to RDF

[random comments from the introductions noted by Steve](additional.md)
-How can RDF help TDWG integrate with different communities?
-Reproducibility and interoperability desired.
-Semantic interoperability.
-Merge TDWG approaches with other semantic technologies.
-Ability to express ontologies in OWL, best practices, maintain ontologies, visualization, harmonize with other technologies.
-Combine occurrences with other fields such as genomics, RDF redefinition of all of the activities of Interest Groups.
-Best practices.
-It's a misconception that ontologies must come first.
[of Steve's inserted notes](end.md)


Joel S: what categories of data do we have for representing in RDF: occurrences, descriptive data (SDD), phenotypes, genomics

Donald H: better approach than fixed list is to look to unify the various TDWG standards using RDF

Greg W: step back and look for smaller components, rather than work backwards with RDF

Hilmar L: we should manage expectations of the group. What will and will not come out of the group. Not expecting the group to create an ontology, rather best practices

Bob M: creating ontologies is like TDWG supporting database schemas

Hilmar L: as a group of informaticians we're coming with a top-down view, not bottom up starting with data

Joel S: agrees we don't want to be creating ontologies

Donald: reiterates history of TDWG came with top-down approach with schemas like ABCD. DarwinCore was successful because it avoided pitfalls of XML schema, yet lost semantics. Suggests
we can continue the pick and match of Classes and Properties, more semantic rigor

Stan: earlier presented a challenge of presenting data to two different groups without losing information. Tease apart the essential similarities and differences of ontologies in groups represented in TDWG and elsewhere

Hilmar: Ontology is the byproduct of substantiating the case we want to make, not the final product

Katja: very abstract class / relationship vocabulary

Olivier: lets take up Rod's challenge and create an application which uses existing RDF data

Joel: agrees. Who is willing (or not) to contribute data to the challenge through the tdwg-rdf group?

Donald: was Rod asking for inferences, or simply uses of RDF data?

Bob: if A knows something B doesn't and vice versa, is it possible, when combining all data, to understand the union of A and B's knowledge in a meaningful way?

Break; when reconvening to talk about building the sandbox, defining scope

---


Steve B: TDWG is a standards body, so it should endorse standards. There are several categories of standards, including best practices, applicability. In the case of RDF: formatting, indexing, how to upload to triplestore. Approaching these other types of ‘standards’ may help us avoid the ‘minefield’.

Bob: Goal #2 [from tdwg-rdf charter ](.md) has no measurable outcome

Joel: Goal for first year should be to document the approaches.... Would be happy of we produce nothing more than a ‘standard’ which is a best practices document

Kevin: we should list what the group members hope to get out of the group

Hilmar: would would motivate member from moving from being inclined to participate to actually participating in the group
Joel: test the sandbox to see what data is added, and if they actually match

Bob: wants to take it mush slower. Understand the implications of different modeling strategies before making recommendations. An audit is next years task

Donald: perhaps a good test is to take Catalogue of Life, FishBase (perhaps through EOL), and GBIF occurrence information and see what we might make of that aggregate

Bob: the bleeding edge can keep bleeding for another year

Hilmar: the differences between RDF/RDFs/OWL is very technical and irrelevant to scientific research

Cam: agrees the technical stuff is irrelevant. Where are the tools and how do I use them?

Bob/Hilmar: the tools which produce RDF like datasets and the common RDF datasets themselves are within scope of the best practices

Greg: we have to start to put the larger datasets together (CoL, BHL)

Joel: one of his best practices: do not use domain and range constraints due to their affect on inferences. We should define patterns for creating Classes and Properties. Does anyone have a SPARQL endpoint where we can load data and run queries and do reasoning? (3 yeses - Olivier, Cam [small scale](http://tdwg-rdf.net/store1,) and Julien). Anyone else with triplestore should link to it from Google group. Group will also have a questionnaire

Cam: if people that provide datasets, provide bubble diagrams of Classes and Properties within

Joel: does anyone have a really good dataset to share

Hilmar: you’re asking for too much, no one has a ‘perfect’ dataset, but perhaps parts are good. What can we learn from the failures? Datasets are very idiosyncratic, and work for the providers and not many others

Joel: we all generally agree on the 3 medium term goals (use cases, experiment with modelling, documentation). Looking for volunteers to go through the questionnaire responses to look for use cases

Donald: the data provided will massively constrain the use cases we might tackle

Rod Page (via Jim C): do we actually have users that want RDF?

Cam, James, Hilmar, Greg: I’m a user

Stan: the group is so diverse, and the matrix of data is so sparse, which creates problems

Matt: my use case is to make available phenotypes and atomized descriptive data. We don’t need complex data - lets make what we have available because simply knowing what is red or blue can be useful to the right user

Donald: an immediate use case for ALA (show me the Acacia species within 10km and get their character/state data and create a key) doesn’t need reasoning or OWL. Simply need to aggregate and relate datasets

---

## Joint discussion: ##

BiSciCol (Deck, Pyle): Lets throw the data into the sandbox, see whats out there, and see what problems come up rather than predicting the problems