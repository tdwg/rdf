# Beginner's guide to RDF: 6. Querying with SPARQL #

[go to part 5: Discovery, Transmission, and Storage of RDF data](Beginners5RDFdata.md)

[go to part 7: Ontologies and OWL](Beginners7OWL.md)

[Introduction to the Guide](Beginners.md)

**Contents**



## 6.1. What is SPARQL? ##

SPARQL is a query language designed specifically to query RDF databases. [(1)](#1_SPARQL_1.1_Query_Language.md)  SPARQL queries are sent from a client to a service known as a SPARQL end point [(2)](#2__Definition_of_SPARQL_endpoint.md) using the HTTP protocol.  The interaction between the client and the endpoint is defined in a machine-friendly protocol [(3)](#3_Communication_protocol_for_SPARQL.md) that is not intended to be interpreted by humans, so use of SPARQL requires an interface that allows the user to enter the queries and to display the results in a meaningful way.  As with traditional database languages such as SQL, those interfaces are commonly constructed so that the queries are constructed and launched  through forms that do not require the human user to have any knowledge of RDF and SPARQL.  Programming such interfaces is beyond the scope of this guide.

In this guide, some examples will be provided to show you some of the capabilities of SPARQL.  Then a few basic search terms will be described and illustrated.  SPARQL is capable of doing queries that are far more sophisticated than those shown here.  However, such queries are beyond the scope of a guide for beginners so the reader is referred to additional resources in [section 6.6](#6.6._For_further_information.md).

## 6.2. Public SPARQL interfaces ##

### 6.2.1. DBpedia ###
#### 6.2.1.1. Creating RDF metadata and URIs via DBpedia ####

DBpedia transforms into RDF triples data that are entered in Wikipedia.  So creating a page in Wikipedia creates RDF in DBpedia.  Creating a page for a taxonomist creates a URI and other metadata about the person. [(4)](#4_Strategy_for_creating_URIs_for_famous_dead_people.md)  For example, the page

http://en.wikipedia.org/wiki/Johan_Christian_Fabricius

describes Fabricus.  DBpedia creates a URI of the format
```
http://dbpedia.org/resource/wikipedia_page_name
```
where wikipedia\_page\_name is the name of the regular Wikipedia html page.  Note that underscore characters replace spaces, the strategy used for creating the regular page URLs.  In the case of Fabricus, his URI is:
```
http://dbpedia.org/resource/Johan_Christian_Fabricius
```

#### 6.2.1.2. Querying DBpedia ####

DBpedia can be queried via a Web interface at http://dbpedia.org/sparql .  The interface uses the [Virtuoso](http://virtuoso.openlinksw.com/) SPARQL Query Editor to query the DBpedia endpoint.  Enter the query
```
PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
PREFIX dbpprop: <http://dbpedia.org/property/>
PREFIX dbres: <http://dbpedia.org/resource/>

SELECT ?y WHERE {
 ?y dbpedia-owl:binomialAuthority dbres:Johan_Christian_Fabricius.
 }

limit 10
```
into the Query Text box.  Drop down the Results Format selection to HTML then click Run Query.  The resulting display should provide a table of 10 species for which the binomial authority was Fabricus.  Note that because the resources are described by the Wikipedia page names, there is no consistency in the URIs - some are given as scientific names and some are given as common names.  Output formats other than HTML are possible with this query editor but most aren't human-friendly.

DBpedia has an ontology for categorizing information systematically.  It includes properties such as dbpedia-owl:family and other taxonomic levels.  Enter the following query:
```
PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
PREFIX dbpprop: <http://dbpedia.org/property/>
PREFIX dbres: <http://dbpedia.org/resource/>

DESCRIBE ?x WHERE {
 ?x dbpedia-owl:family dbres:Crambidae.
 ?x dbpedia-owl:binomialAuthority dbres:Johan_Christian_Fabricius.
 }

limit 10
```
and select Results Format RDF/XML or some other format.  Depending on your browser you may be able to view the output directly or you may have to save the file and open it using a text editor.  (Some dedicated RDF and XML editors are listed in [section 0.3.5.](Beginners#0.3.5._Software_tools.md) of this guide.)  The results show all of the triples that describe the 5 or so Crambidae species described by Fabricus which have articles in Wikipedia.  You should note that DBpedia routinely provides the language attribute for literals.  So a query containing a literal must have an "@" language tag.  For example:
```
PREFIX dbpprop: <http://dbpedia.org/property/>

DESCRIBE ?x WHERE {
 ?x dbpprop:binomial "Diatraea saccharalis"@en.
 }
```
will produce results even though the binomial is in Latin because Wikipedia apparently assumes that text entered in English wiki pages is in English.

### 6.2.2. URIBurner ###
#### 6.2.2.1. Pushing metadata into URIBurner cloud ####
URIBurner (a  Virtuoso-based product of OpenLink software) provides a web-based mechanism to "sponge" data from an RDF file which is on the Web.  As of 12 Feb 2012, the URIBurner home page http://uriburner.com provides a text box into which the URL of a file containing RDF (in RDF/XML, N3, or RDFa) can be entered.  After clicking on the Sponge! button, the triples in the file get added to the uriburner.com SPARQL host where they can be accessed through a public endpoint.  The metadata aren't really in the Linked Open Data (LOD) "cloud" any more than they were before, but forcing URIBurner to sponge the file makes the metadata available to anyone who conducts a search using a URIBurner interface.

#### 6.2.2.2. Querying the URIBurner triplestore ####
URIBurner provides a basic Virtuoso-based SPARQL endpoint similar to the DBpedia interface at http://uriburner.com/sparql [(5)](#5_Demonstration_of_capabilities_of_URIBurner.md).  The results are as un-human friendly as those of DBpedia.  However, URIBurner has an enhanced service at http://uriburner.com/isparql/ which provides output in a number of forms that is more readable to humans.  As of 12 Feb 2012, TDWG BioBlitz metadata were present on URIBurner.  Using the enhanced interface with the Advanced tab selected, enter the following query in the SPARQL Query text box
```
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX txn: <http://lod.taxonconcept.org/ontology/txn.owl#>
PREFIX tdwg: <http://rs.tdwg.org/dwc/terms/#>

DESCRIBE ?x WHERE {
 ?x a txn:Occurrence.
 ?x dcterms:date "2010-09-29".
 ?x tdwg:recordedBy "Peter Desmet".
}
limit 10
```
and click the Run Query button which has an icon like a "play" button.  This should display the results of the query under the Results tab.  The default view is Navigator, which behaves like the OpenLink Navigator linked data browser (see [section 0.3.6.](Beginners#0.3.6._Web_interfaces.md) of this guide).  Dropping down the view to Raw Triples lists property-value pairs under the heading of each subject URI.  If the value is an image URL, the image is displayed on the screen.  If a described resource contains `geo:lat` and `geo:long` triples, dropping down the Google Maps v3 view will display markers on a Google Map display.  Clicking on a marker displays the triples for the resource whose properties include the `geo:lat` and `geo:long` values.

### 6.2.3. TaxonConcept ###
The TaxonConcept database [(6)](#6_TaxonConcept_project.md) is a very large public triplestore which contains metadata on many species and which has loaded other datasets of interest.  It contains over 37 million triples (as of 1 March 2012).

Go to the human-friendly interface at http://lsd.taxonconcept.org/isparql .  Replace the default query with
```
DESCRIBE ?y WHERE {
 ?y skos:closeMatch ?z.
 ?z txn:scientificName "Apis mellifera".
}
```
Click the Run Query button ("play").  On the Results tab, click on the "55 more..." link.  The results show the many concepts which have been used to represent entities that are nearly the same as `http://lod.taxonconcept.org/ses/z9oqP#Species` which represents a species concept for _Apis mellifera_ (the European honey bee).

## 6.3. Loading metadata into a private triple store for querying ##

The TDWG TDF/OWL Task Group has several sandboxes for experimenting with SPARQL queries at http://tdwg-rdf.phylodiversity.net/ .  To obtain access, contact Cam Webb via the link on the page.  The query interfaces are similar to those described in the previous sections.  However, loaded datasets are restricted to those loaded by participants in the Task Group, so the results may be somewhat more predictable than results from public triplestores.  Also, the stability of the triples might be somewhat better than the unknown stability of the public stores (assuming the members of the TDWG-RDF group do not unload datasets that are currently present there).

## 6.4. Basic SPARQL queries ##

These examples use metadata currently loaded as of 13 February 2012, so in theory they should produce results until the datasets are unloaded at some future time.  Additional information about constructing queries is at http://www.w3.org/TR/sparql11-query/#basicpatterns

### 6.4.1. Representing literals, URIs, and variables ###

Literals are placed in quotation marks, e.g. "Hawaii".  [(7)](#7_Literals_that_are_typed_or_which_have_language_tags.md)  URIs [(8)](#8_Internationalized_Resource_Identifiers_(IRIs).md) are placed inside angled brackets, e.g. `<http://xmalesia.info/sw/event/3e2c5f3711>` .  This is similar to the format used in the N3 RDF serialization (see [section 3.3.4.](Beginners3RDFbasics#3.3.4._Notation_3_(N3)_representation.md) of this guide).

#### 6.4.1.1. PREFIX declarations ####
SPARQL queries allow the user to abbreviate URIs by declaring prefix abbreviations.  For example, the declaration
```
PREFIX dcterms: <http://purl.org/dc/terms/>
```
allows the URI `http://purl.org/dc/terms/Location` to be abbreviated as `dcterms:Location`.  Note: this behavior is similar to the use of namespace abbreviations for URIs in N3 RDF serializations (see[section 3.3.4.](Beginners3RDFbasics#3.3.4._Notation_3_(N3)_representation.md) of this guide).

#### 6.4.1.2. Variables ####
If a string is preceded by a question mark, it is treated as a variable which can represent a URI or a literal, e.g. `?x`  or `?person`.

### 6.4.2. Triple patterns ###
SPARQL is based on matching parts of an RDF graph [(9)](#9_RDF_graph.md) with triple patterns that may contain variables.  For example, the triple pattern
```
?Location  dwc:stateProvince "Hawaii"
```
would match the triple
```
<http://bioimages.vanderbilt.edu/baskauf/04005#loc>  dwc:stateProvince  "Hawaii"
```
The solution sequence is the set of triples which match the triple pattern.  There can be zero, one, or many solutions in the sequence.  A triple pattern can also contain zero, one, two, or three variables.

As in N3 serialization, the URI
```
http://www.w3.org/1999/02/22-rdf-syntax-ns#type
```
> or
```
rdf:type
```
can be abbreviated as
```
a
```
So the pattern
```
?loc a dcterms:Location
```
is the same as
```
?loc rdf:type dcterms:Location
```

### 6.4.3. SELECT query form ###
The SELECT query form is used to create a list of URIs which satisfy the pattern-matching requirements specified in the query.

To investigate the use of SELECT, go to http://lsd.taxonconcept.org/isparql/ and click on the Advanced tab if necessary. Clear the Result size limit box, then in the query box, enter the following prefix declarations which will be used in the examples to follow:
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX dcmitype: <http://purl.org/dc/dcmitype/>
PREFIX dwc: <http://rs.tdwg.org/dwc/terms/>
PREFIX tdwg: <http://rs.tdwg.org/dwc/terms/#>
PREFIX mrtg: <http://xxx.org/XXX/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX txn:   <http://lod.taxonconcept.org/ontology/txn.owl#>
PREFIX dsw: <http://purl.org/dsw/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
PREFIX mbank: <http://www.morphbank.net/schema/morphbank#>
```
Skip a line then enter the query below which contains the triple pattern given in the previous example.
```
SELECT ?Location WHERE {
 ?Location  dwc:stateProvince "Hawaii".
 }
```

Click on the Run Query (play button) icon.  Mouse over the results link to see the URIs (e.g. http://bioimages.vanderbilt.edu/baskauf/04005#loc) which can substitute for the variable `?Location` in the triple pattern.  Click on the Advanced tab and try replacing "`Hawaii`" with "`Tennessee`" and "`Indiana`".  <a href='Hidden comment: doesn"t work on that endpoint
(If you click on one of the links in the Results view, it will take you to a Linked Data browser.  To return back to the query results, click on the blue left-facing arrow before clicking on the Advanced tab again.)'></a>


To see what the query results look like in machine-friendly form, repeat them at the URL http://lsd.taxonconcept.org/sparql/ and select a non-HTML Results Format.

#### 6.4.3.1. Eliminating duplicate results using DISTINCT ####
Return to the human-friendly interface ( http://lsd.taxonconcept.org/isparql/ ). Using the same prefix list as above, enter the following query:
```
SELECT ?Organism WHERE {
 ?Organism dsw:hasOccurrence ?Occurrence.
 ?Image dsw:evidenceFor ?Occurrence.
 ?Image dcterms:type dcmitype:StillImage.
}
LIMIT 50
```
This query selects individual organisms (trees) which have occurrences that are documented by images.  Because there are many possible results, `limit 50` is specified to try out the query without getting an inordinate number of results.  If you run the query, you will find that there are numerous duplicate results because there are numerous images for each tree.  Replace the first line with
```
SELECT DISTINCT ?Organism WHERE {
```
to remove duplicate results.


### 6.4.4. DESCRIBE query form ###

The DESCRIBE query form returns all triples which contain all URIs which satisfy the pattern-matching requirements specified in the query.  The URIs may be present as either the subject or object of the triples.

#### 6.4.4.1. Describing a single resource identified by URI ####
Using the same prefixes as before, enter the following query:
```
DESCRIBE <http://bioimages.vanderbilt.edu/baskauf/04005#loc>
```
which contains a URI solution for the variable `?Location` in the query of [6.4.3](#6.4.3._SELECT_query_form.md).  Try changing the View from Navigator to Raw Triples as described in [section 6.2.2.2.](#6.2.2.2._Querying_the_URIBurner_triplestore.md) .  The description of the resource identified by the URI contains triples in which the URI is the subject (grouped together) and a triple where the URI was the object.  Change the View to Google Maps v3.  Zoom out and change the view to Satellite if desired.

#### 6.4.4.2. Describing a set of resources that match a variable in a triple pattern ####

Click on the Advanced tab to return to the query interface and replace the previous query with
```
DESCRIBE ?Location WHERE {
 ?Location  dwc:stateProvince "Tennessee".
 }
```
If you are not patient, you can use LIMIT 50.  The results include triples for all of the location URIs which can substitute for `?Location` in the triple pattern used in the query.  The Grid View shows the triples that were returned.  The Raw Triples view groups predicate/object (i.e. property/value) pairs under the subject resource.  Google Maps v3 uses the `geo:lat` and `geo:long` values present in the resulting set of triples to map the locations of the described resources.

#### 6.4.4.3. Describing a set of resources that match a variable in several triple patterns ####
Go to the http://uriburner.com/isparql/ endpoint and paste in the list of prefixes from [6.4.3.](#6.4.3._SELECT_query_form.md).  Replace the existing query with the query similar to that given in [section 6.2.2.2.](#6.2.2.2._Querying_the_URIBurner_triplestore.md):
```
DESCRIBE ?x WHERE {
 ?x a txn:Occurrence.
 ?x dcterms:date "2010-09-29".
}
LIMIT 10
```
There are many records in the TDWG Bioblitz.  We want to limit the description set by requiring the record URIs to match several criteria.  We want to examine records that are only `txn:Occurrences` [(10)](#10_TaxonConcept_ontology.md) that were recorded on September 29, 2010.  Experiment with various views.

The query can be further limited by adding the triple pattern
```
?x tdwg:recordedBy "Peter Desmet".
```
to the list and removing the `LIMIT 10` restriction.  Other possible literals that could be used are "Donald Hobern", "Cyndy Sims Parr", "test", and "Dmitry Mozzherin"

#### 6.4.4.4. Describing a set of resources that match several triple patterns containing multiple variables ####
Because the structure of the TDWG Bioblitz metadata was very flat with all properties ascribed to the occurrence, the single variable `?x` could represent the URIs of the desired occurrence resources.  The Bioimages RDF graph uses the Darwin-SW ontology [(11)](#11_Darwin-SW_ontology.md) which is highly normalized (NOT flat) and therefore separates the metadata among instances of many of the Darwin Core classes.

Return to the http://lsd.taxonconcept.org/isparql/ endpoint and use the usual prefix list from [section 6.4.3.](#6.4.3._SELECT_query_form.md). The query
```
DESCRIBE ?SAP WHERE {
 ?SAP mrtg:variant "Lower Quality".
 ?Image mrtg:hasServiceAccessPoint ?SAP.
 ?Image dsw:evidenceFor ?Occurrence.
 ?Occurrence dsw:atEvent ?Event.
 ?Event dsw:locatedAt ?Location.
 ?Location a dcterms:Location.
 ?Location dwc:stateProvince "Hawaii".
}
```
requests a description of the `Lower Quality` `ServiceAccessPoint`s (downloadable versions) of images which serve as `evidenceFor` occurrences documented `atEvents` which are `locatedAt` Locations which are in the `stateProvince` of `Hawaii`.  The variables (`?Location`, `?Event`, etc.) represent intermediate resources (instances of Location, Event, Occurrence, etc.) that link the string "`Hawaii`" with the URI for the `ServiceAccessPoint` (e.g. `http://bioimages.vanderbilt.edu/baskauf/04005#lq`) and the URL which provides access to the actual images (e.g. `http://bioimages.vanderbilt.edu/lq/baskauf/wmetro-br04005.jpg`) that are the solutions to the query.  Select the Raw Triples view to see the actual images.  Replace "DESCRIBE ?SAP" with "DESCRIBE ?Location ", run the query and select the Google Maps v3 View to see the locations where the images were taken.

### 6.4.5. Creating RDF graphs using CONSTRUCT ###
The result of the CONSTRUCT query form is an RDF graph which contains triples in the form of the graph template with substitution for variables of URIs or literals from solutions to the constraining query triple patterns.

In the example given in [section 6.4.4.1.](#6.4.4.1._Describing_a_single_resource_identified_by_URI.md), the result described the resource identified by the URI by presenting all triples in the dataset which referenced that URI, including triples where the URI was the object rather than the subject.  To produce similar descriptive results where the results are constrained solely to triples where the URI is the subject, use the query
```
CONSTRUCT {
  <http://bioimages.vanderbilt.edu/baskauf/04005#loc> ?predicate ?object.
}
WHERE {
  <http://bioimages.vanderbilt.edu/baskauf/04005#loc> ?predicate ?object.
}
```
View the result using the Raw Triples view.  Note that this time only triples which contain the URI as the subject are included.  This is achieved by placing no restrictions on the values of the predicate and object in the WHERE section.  The constructed triples include each predicate and object value in the same position in which they occurred in the match.

The values of the constructed triples can be constrained by several triple patterns.  For example, in the following query
```
CONSTRUCT { ?x txn:scientificName ?name }
WHERE {
 ?x txn:scientificName ?name.
 ?x a txn:SpeciesConcept.
 ?x txn:kingdom "Plantae".
 }

LIMIT 10
```
the species concept must represent a plant.  The constructed triples contain the same name string object as the object of the first triple pattern of the constraints.

There is no requirement that the values have to be in the same position as they were in the patterns used to do the screening and the constructed triples may contain values that are not even present in the source graph.  For example in this query:
```
CONSTRUCT { ?article dwc:articleTaxonName ?name }
WHERE {
 ?x txn:hasWikipediaArticle ?article.
 ?x txn:scientificName ?name.
 ?x a txn:SpeciesConcept.
 ?x txn:kingdom "Plantae".
 }

LIMIT 10
```

The resulting triples contain a subject which was the object of one of the pattern triples and an object from a different pattern triple.  The constructed triple also has a made-up predicate (not actually even present in the dwc:namespace!).  CONSTRUCT will create whatever triple you specify regardless of whether the statements made by the created triples make sense or are actually true.

## 6.5. Examples of more complex queries ##
A more complex version of the query in [section 6.4.3.1.](#6.4.3.1._Eliminating_duplicate_results_using_DISTINCT.md) can be made at the endpoint http://tdwg-rdf.phylodiversity.net/store2/ as follows:
```
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX dcmitype: <http://purl.org/dc/dcmitype/>
PREFIX dsw: <http://purl.org/dsw/>

SELECT DISTINCT ?tree WHERE {
 ?tree dsw:hasOccurrence ?Occurrence.
 ?image dsw:evidenceFor ?Occurrence.
 ?image dcterms:type dcmitype:StillImage.
 ?tree dsw:hasOccurrence ?OtherOccurrence.
 ?specimen dsw:evidenceFor ?OtherOccurrence.
 ?specimen a dsw:PreservedSpecimen.
}
```
As in the example of [section 6.4.3.1.](#6.4.3.1._Eliminating_duplicate_results_using_DISTINCT.md), the first three triple patterns select trees that are have occurrences that are documented by images.  The last three triple patterns similarly select trees that have occurrences that are documented by preserved specimens.  By using the same variable `?tree` to refer to trees document by images and trees documented by specimens, trees described by the resulting set must be documented by both images and specimens.

The query
```
DESCRIBE ?specimen WHERE {
 ?tree dsw:hasOccurrence ?Occurrence.
 ?image dsw:evidenceFor ?Occurrence.
 ?image dcterms:type dcmitype:StillImage.
 ?tree dsw:hasOccurrence ?OtherOccurrence.
 ?specimen dsw:evidenceFor ?OtherOccurrence.
 ?specimen a dsw:PreservedSpecimen.
}
```
performs a similar screen but requests the query to describe the specimen (`?specimen`) rather than list the URI of the tree.

## 6.6. For further information ##
### 6.6.1. W3C SPARQL reference document ###
More complex queries can be constructed using filters, negation, optional patterns, and other features of SPARQL that are beyond the scope of this guide.  See

http://www.w3.org/TR/sparql11-query/

for an exhaustive description of SPARQL queries.

### 6.6.2. SPARQL Web tutorials ###
The following is a list of some Web tutorials for learning SPARQL.  They have not been vetted and their listing here does not imply the endorsement of the TDWG-RDF group.

http://www.cambridgesemantics.com/semantic-university/sparql-by-example

http://www.linkeddatatools.com/querying-semantic-data

http://www.ibm.com/developerworks/xml/library/j-sparql/

http://jena.sourceforge.net/ARQ/Tutorial/

### 6.6.3. Examples ###

Here is an example of a complex SPARQL query:

https://groups.google.com/d/msg/tdwg-rdf/GQ9zoMC9RF0/KggrkVPOGgYJ

Here is a paper that assesses the efficiency of querying using SPARQL:

[FishMark: A Linked Data Application Benchmark](http://www.academia.edu/2721762/FishMark_A_Linked_Data_Application_Benchmark)

# References #
### 1 SPARQL 1.1 Query Language ###
http://www.w3.org/TR/sparql11-query/

### 2  Definition of SPARQL endpoint ###
http://semanticweb.org/wiki/SPARQL_endpoint

### 3 Communication protocol for SPARQL ###
http://www.w3.org/TR/sparql11-protocol/

### 4 Strategy for creating URIs for famous dead people ###
This was suggested by Pete DeVries.

### 5 Demonstration of capabilities of URIBurner ###

http://www.taxonconcept.org/example-sparql-queries/

thanks to Pete DeVries.  This page also contains URLs which provide examples of embedding the SPARQL queries within the URL so that the results are displayed when the URL is clicked.

### 6 TaxonConcept project ###
Homepage:

http://www.taxonconcept.org/

SPARQL endpoint:

http://lsd.taxonconcept.org/sparql

Human-friendly endpoint:

http://lsd.taxonconcept.org/isparql

### 7 Literals that are typed or which have language tags ###
If literal strings are typed or have language tags, they are not considered equivalent to the same simple literal string.  For example, "cat" is not equivalent to "cat"@en ("cat" tagged as English).  See http://www.w3.org/TR/sparql11-query/#matchingRDFLiterals for more information.

### 8 Internationalized Resource Identifiers (IRIs) ###
Technically, SPARQL uses IRIs which are a generalization of URIs that allow non-ASCII characters.  See

http://tools.ietf.org/html/rfc3987

However, as a matter of convenience, IRIs will be referred to as URIs in this guide.

### 9 RDF graph ###
"Graph" is the term for a set of RDF triples which may be interconnected by having nodes (URIs or literals) in common.  Graphically, this is shown as nodes connected by arrows which represent predicates.  However, the term "graph" represents the set of triples regardless of serialization and not specifically a graphical representation.  For more information, see

http://www.w3.org/TR/rdf-primer/#intro

A _named graph_ provides a means for identifying a subgraph of triples within a triple store.

### 10 TaxonConcept ontology ###
The TDWG BioBlitz used some terms from the TaxonConcept ontology which defines "light-weight tags" (many classes) that can be used to create very flat database records.  For more details, see

http://www.taxonconcept.org/ontologies/

### 11 Darwin-SW ontology ###
The Darwin-SW (DSW) ontology is a fully normalized model which has relatively few classes (based primarily on the Darwin Core classes) but which results in very deeply nested records.  See the diagram at

http://code.google.com/p/darwin-sw/

which diagrams the relationships among the classes and

http://code.google.com/p/darwin-sw/wiki/DesignPrinciples

for a description of the design principles on which it is based.

---

Thanks to Bob Morris for helpful comments and suggestions on this page.

Questions? Comments? Contact [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide)

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.