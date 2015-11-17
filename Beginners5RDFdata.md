# Beginner's guide to RDF: 5. Discovery, Transmission, and Storage of RDF data #

[go to part 4: Vocabularies, DCAM, and RDFS](Beginners4Vocabularies.md)

[go to part 6. Querying with SPARQL](Beginners6SPARQL.md)

[Introduction to the Guide](Beginners.md)

**Contents**



## 5.1.  Providing a means for discovering information about a URI through dereferencing ##

The URI
```
urn:isbn:0893273651
```
follows the general rules of URI syntax [(1)](#1._RFC_3986._Uniform_Resource_Identifier_(URI):_Generic_Syntax.md) and the specific rules for describing ISBN numbers as URIs [(2)](#2._Using_International_Standard_Book_Numbers_as_Uniform_Resource.md).  However, there is no obvious way to use this identifier as a means to dereference it, i.e. to retrieve information about the thing that it represents.  In contrast, the URI
```
http://www.w3.org/History/19921103-hypertext/hypertext/WWW/TheProject.html
```
not only follows serves as an identifier for one of the world's first web pages, but it also identifies the protocol (HTTP) that can be used to retrieve the document and provides the information required to tell the web server which document to send.  The URI
```
urn:lsid:biocol.org:col:12599
```
is dereferenceable using the LSID protocol [(3)](#3_References_for_LSIDs.md).  However, the LSID can't be dereferenced without installing special software, i.e. it can't be entered in a standard web browser.

There is no requirement that a URI be dereferenceable and RDF statements can use any URI as the subject or object of a triple.  Advocates of Linked Data [(4)](#4_Linked_Data.md) prefer to use HTTP URIs to refer to resources because the HTTP protocol is in widespread use and because HTTP URIs provide not only a unique identifier but also the means to access a representation of the thing being identified.

## 5.2. Using a document served through URI dereferencing to facilitate discovery of metadata associated with the URI ##

Note: details regarding the mechanisms by which content negotiation is used retrieve RDF information by dereferencing a URI is described in detail in the [Best Practice Recipes for Publishing RDF Vocabularies](http://www.w3.org/TR/swbp-vocab-pub/).

### 5.2.1. Getting the descriptive document. ###
The URI `http://lod.taxonconcept.org/ses/z9oqP#Species` represents an abstract resource which is a species concept for _Apis melifera_, the European honeybee.  Because this identifier is an HTTP URI, a client (computer program) can use the HTTP protocol to dereference the identifier in an attempt to obtain information about the resource through the process described below.  The Vapour Linked Data Validator (http://validator.linkeddata.org/vapour) can be used to examine the details of this process.

1. The client contacts the server `http://lod.taxonconcept.org` and requests the resource identified by `http://lod.taxonconcept.org/ses/z9oqP#Species`.  In the request, the client may indicate its preference of form of response.  If the client is a web browser, it will request `content-type: text/html` [(5)](#5_Internet_media_types.md).  If it is a semantic client it will request `content-type: application/rdf+xml`.

2. The server ignores the "#" character and everything after it in the URI.  A URI which ends in a "hash tag" like this is called a hash URI.  (Another name for the part of the URI after the # character is "fragment".) Hash URIs are commonly used to identify non-information resources.  In this case, the server determines that the base URI `http://lod.taxonconcept.org/ses/z9oqP` is not an information resource that can be returned to the client, so based on some kind of information or rule that it knows, it determines an appropriate representation of the resource based on the content-type requested by the client.  In the case where `content-type: application/rdf+xml` is requested, the server responds to the client that it should "See Also" the representation provided by the URI `http://lod.taxonconcept.org/ses/z9oqP.rdf`.  This process is called content negotiation.

3. The client requests the resource `http://lod.taxonconcept.org/ses/z9oqP.rdf` from the server and the server sends it.

4. The client decodes the XML and interprets it as RDF triples.  Those triples will hopefully describe properties that will help the client understand the nature of the resource `http://lod.taxonconcept.org/ses/z9oqP#Species`.

### 5.2.2. Using the retrieved document to understand the identified resource and other resources related to it ###

The RDF in the retrieved document ` http://lod.taxonconcept.org/ses/z9oqP.rdf` contains the following information (including many additional properties are not shown here) about the the identified resource (click on http://lod.taxonconcept.org/ses/z9oqP.rdf to view the actual document):
```
in XML:
<owl:Class rdf:about="http://lod.taxonconcept.org/ses/z9oqP#Species">
     <rdf:type rdf:resource="http://lod.taxonconcept.org/ontology/txn.owl#SpeciesConcept"/>
     <wdrs:describedby rdf:resource="http://lod.taxonconcept.org/ses/z9oqP.rdf"/>
    <dcterms:isPartOf rdf:resource="http://lod.taxonconcept.org/ontology/void#TaxonConcept"/>
</owl:Class>

in N3:
<http://lod.taxonconcept.org/ses/z9oqP#Species> 
     a txn:SpeciesConcept,
          owl:Class;
     wdrs:describedby <http://lod.taxonconcept.org/ses/z9oqP.rdf>;
     dcterms:isPartOf <http://lod.taxonconcept.org/ontology/void#TaxonConcept>.
```
In graphical form:

![http://tdwg-rdf.googlecode.com/svn/trunk/file/rdf-related-resource-links.jpg](http://tdwg-rdf.googlecode.com/svn/trunk/file/rdf-related-resource-links.jpg)

From this information, we know that the resource has two types: `owl:Class`[(6)](#6_owl:Class.md) and `txn:SpeciesConcept` (where `owl:` is an abbreviation for ` http://www.w3.org/2002/07/owl# ` and `txn:` is an abbreviation for `http://lod.taxonconcept.org/ontology/txn.owl#`).

#### 5.2.2.1. Linking the non-information resource to the document that describes it ####
The description also says that the resource is `wdrs:describedby` [(7)](#7_Protocol_for_Web_Description_Resources_(POWDER).md) the RDF/XML document that was returned by the server.  This property links the non-information, abstract resource (the taxon concept) to the information resource that describes it in RDF.  The term `foaf:isPrimaryTopicOf` [(8)](#8_FOAF_Vocabulary_Specification.md) can also be used to relate resources to documents that describe them.  By providing this triple, a semantic client can know precisely how the delivered document is related to the described resource.  The client can then examine the RDF describing the delivered document (also included in the delivered document) to find out things such as its language, modification date, and many other properties not shown here:
```
in XML:
<bibo:Document rdf:about="http://lod.taxonconcept.org/ses/z9oqP.rdf">
    <dcterms:language>en</dcterms:language>
    <dcterms:modified>2012-02-02T23:05:47-0600</dcterms:modified>
</bibo:Document>

in N3:
<http://lod.taxonconcept.org/ses/z9oqP.rdf> 
     a bibo:Document;
     dcterms:language "en";
     dcterms:modified "2012-02-02T23:05:47-0600".
```

#### 5.2.2.2. Linking the non-information resource to a vocabulary or dataset of which it is a part ####

The description of the species concept contains a triple which says that the resource `dcterms:isPartOf` another resource that is not described by the delivered RDF document itself.  If possible, that URI could be dereferenced to find out more about that collective entity and perhaps to discover the URIs of other resources similar to the one being described.  In Dublin and Darwin Cores, each term is described as `rdfs:isDefinedBy` the vocabulary which contains it.  [(9)](#9_Dublin_Core_RDF_definitions.md)  In those cases, the RDF describing the vocabulary (with URI `http://purl.org/dc/terms/`) is included in the same document which contains the RDF describing the term (which has the URI `http://purl.org/dc/terms/creator`) and is delivered along with it when there is a request to dereference the term URI.

In graphical form this can be represented as:

![http://tdwg-rdf.googlecode.com/svn/trunk/file/rdf-terms-related-to-vocabulary.jpg](http://tdwg-rdf.googlecode.com/svn/trunk/file/rdf-terms-related-to-vocabulary.jpg)

Resources which are part of a dataset and described in separate documents can be backlinked to a file which describes the dataset using the `void:inDataset` property.  This method is described in [section 5.3.3.](#5.3.3._Providing_information_about_the_data_which_are_available.md)

### 5.2.3. Summary of this strategy ###

The RDF descriptions of several related resources can be provided in a single document which is delivered when any of the URIs of those resources is dereferenced.  This can be accomplished using hash URIs where non-information resources are differentiated by assigning them various hash tags such as
```
http://lod.taxonconcept.org/ses/z9oqP#Image
http://lod.taxonconcept.org/ses/z9oqP#Occurrence 
http://lod.taxonconcept.org/ses/z9oqP#Individual 
http://lod.taxonconcept.org/ses/z9oqP#Identification 
```
The document (an information resource) is delivered by the server based on some rule which tells it how to process the base URI ` http://lod.taxonconcept.org/ses/z9oqP`.  Differentiating non-information resources by hash tags is a commonly used convention, but not a requirement.

A non-information resource can be linked by triples that relate it to other resources which are documents that describe it (such as RDF/XML documents and web pages) or which are collective entities that group the non-information resource with other similar resources.  The descriptions of these other similar resources may be included in the same document that describes the non-information resource, or the descriptions may be retrieved by the client if it wants to try to dereference the URIs of the related resources.

In this manner, a semantic client can "crawl" the web of links to discover other resources and to catalog the relationships among the resources by storing the triples that record those links.

## 5.3. Facilitating the discovery of RDF metadata which is incorporated in a dataset ##

The method described in the previous section is adequate for a small number of URIs, such as those identifying terms in a vocabulary.  However, it is a relatively inefficient way of collecting larger amounts of RDF metadata. If the only descriptions of the resources identified by the URIs are found in individual documents, a client would have to periodically crawl all of the linked documents to discover any changes that might have occurred in the metadata.

### 5.3.1. Using RSS to summarize the content of a small dataset ###
RSS [(10)](#10_RSS_specification.md) was formerly an abbreviation for "RDF Site Summary" [(11)](#11_History_of_RSS_in_Wikipedia.md).  Since that is exactly what we want to do (summarize a site in RDF), RSS can be used to inform web crawlers what metadata files are available to be crawled. [(12)](#12_Publishing_Web_Data_by_Sindice.md)  Importantly, RSS can also allow the crawlers to detect new files and to know when existing pages have changed.

#### 5.3.1.1. Example ####
The following example is a fragment from the page http://bioimages.vanderbilt.edu/rdf/images.rss
```
In RDF/XML:
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:rss="http://purl.org/rss/1.0/"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcterms="http://purl.org/dc/terms/"
>
  <rss:channel rdf:about="http://bioimages.vanderbilt.edu/rdf/images.rss">
    <rss:title>Images in the Bioimages database</rss:title>
    <rss:link>http://bioimages.vanderbilt.edu/</rss:link>
    <rss:description>This channel provides an RDF link to all images in the database so that they can be discovered by Linked Data clients.</rss:description>
    <dcterms:isReferencedBy rdf:resource="http://bioimages.vanderbilt.edu/index.rdf"/>
    <rss:items>
      <rdf:Seq>
        <rdf:li resource="http://bioimages.vanderbilt.edu/baskauf/04005"/>
        <rdf:li resource="http://bioimages.vanderbilt.edu/baskauf/12804"/>
        <rdf:li resource="http://bioimages.vanderbilt.edu/baskauf/12802"/>
      </rdf:Seq>
    </rss:items>
  </rss:channel>
  <rss:item rdf:about="http://bioimages.vanderbilt.edu/baskauf/04005">
     <rss:title>Image of Metrosideros sp. (Myrtaceae) - bark - of a large tree</rss:title>
     <rss:link>http://bioimages.vanderbilt.edu/baskauf/04005</rss:link>
     <dc:date>2011-09-22T22:32:15</dc:date>
  </rss:item>
  <rss:item rdf:about="http://bioimages.vanderbilt.edu/baskauf/12804">
     <rss:title>Image of Rhus aromatica (Anacardiaceae) - whole tree (or vine) - general</rss:title>
     <rss:link>http://bioimages.vanderbilt.edu/baskauf/12804</rss:link>
     <dc:date>2011-09-22T22:31:39</dc:date>
  </rss:item>
  <rss:item rdf:about="http://bioimages.vanderbilt.edu/baskauf/12802">
     <rss:title>Image of Dalea gattingeri (Fabaceae) - whole plant - juvenile</rss:title>
     <rss:link>http://bioimages.vanderbilt.edu/baskauf/12802</rss:link>
     <dc:date>2011-09-22T22:31:39</dc:date>
  </rss:item>
</rdf:RDF>
```
(This example is not presented in N3 due to complications involving the blank node required by the `rdf:Seq` container.)

#### 5.3.1.2. Explanation of the example ####
An instance of the class `rss:channel` is a descriptive document that contains the list of resources being described in the "feed".  The instances of the class `rss:item` are the individual resources that are being described.  In this case the `rss:item` instances are the described resources whose URIs will be dereferenced to acquire the metadata which describes them.  The `rss:items` property of the channel points to an instance of the `rdf:Seq` class, a container class used to group related resources.  The `rdf:li` properties of the `rdf:Seq` instance point to the items that are being described on the site.  Note: the RDF container classes are not widely used outside of RSS because they make it more difficult to query the data using SPARQL (see [section 6.](Beginners6SPARQL.md) of this guide).

Within the individual `rss:channel` and `rss:item` descriptions, the `rss:title` property is a human readable description of the resource; `rss:title` is a subproperty of `dcterms:title`.  The `rss:link` property is a URL which points to an html rendering of the resource.  The `dc:date` is understood to be the date on which the resource was updated and effectively serves as the modification date which a semantic client would use to determine whether the resource needed to be crawled again.  It is the `<rss:item rdf:about="…">` tag which provides the actual RDF-containing link to the resource which is to be crawled.  `rss:title` and `rss:link` do not really provide any useful information for a semantic client, although they make the RSS page readable in an RSS reader.  In this example, both the HTML and RDF/XML resources are accessed through the same URI because content-negotiation will redirect the client to the document containing the requested type of information.

#### 5.3.1.3. Limitations of using RSS to index a site ####
Although an RSS document reduces the number of documents which a crawler would need to dereference to update its store of information about a database, a single RSS document would be too large to index more than a few thousand resources.  One option would be to have several RSS documents, but even this would be problematic for an RDF database that contained millions of triples.

### 5.3.2. Serving data from large databases ###
If a database is large, it is not practical to convert those data to static documents, nor is it practical for a consuming application to receive those data in the form of XML documents which must be parsed.  The [W3C RDB2RDF Working Group](http://www.w3.org/2001/sw/rdb2rdf/) has produced a [Recommendation](http://www.w3.org/TR/r2rml/) for a Relational Database to RDF mapping language called R2RML.  This language is for "expressing customized mappings from relational databases to RDF datasets. Such mappings provide the ability to view existing relational data in the RDF data model, expressed in a structure and target vocabulary of the mapping author's choice."  The working group provides [use cases and examples](http://www.w3.org/TR/2010/WD-rdb2rdf-ucr-20100608/#uc).

#### 5.3.2.1. Serving data from an existing relational database as RDF ####
It is possible to implement an interface which allows a traditional relational database to serve RDF metadata.

The D2QR Platform [(13)](#13_The_D2RQ_Platform_v0.7_user_manual_and_language_specification.md) provides a mapping language that facilitates mapping and translation.  With this interface, the database can serve the data as Linked Data and can also respond to SPARQL queries (see [section 6.](Beginners6SPARQL.md)).  D2QR also permits dumping the entire database into a file as RDF in various forms. [(14)](#14_D2RQ_RDF_data_dumps.md)

Virtuoso [(15)](#15_Virtuoso.md) can transparently access native relational data as well as RDF data stored in its database.  It allows SPARQL queries.

Triplify [(16)](#16_Triplify.md) is an application that can make content of small (less than 100MB database content) web-accessible databases also available as RDF.  It converts the results of SQL queries into RDF.

Triplifier [(17)](#17_Triplifier.md) is being developed by the BiSciCol project (http://biscicol.blogspot.com/) to input data from flat data formats (spreadsheets, Darwin Core Archives) and relational databases, and output RDF triples.

ezDBDB [(18)](#18_ezDBDB.md) converts metadata from simple data sources like spreadsheets into RDF and provides an opportunity to cache the resulting data in a triplestore and make it available to the LOD cloud.

Bio2RDF Description at http://dx.doi.org/10.1016/j.jbi.2008.03.004 "documents from public bioinformatics databases such as Kegg, PDB, MGI, HGNC and several of NCBI’s databases can now be made available in RDF format through a unique URL in the form of `http://bio2rdf.org/namespace:id`"

#### 5.3.2.2. Loading RDF data into a triple store ####
There are a number of applications [(19)](#19_Wikipedia_article_on_triplestore.md) which permit the storage of RDF as raw triples.  Triple stores are relatively efficient at storing large amounts of data [(20)](#20_Large_triplestores.md) to the range of hundreds of billions to trillions of triples.  They are also efficiently queried using the SPARQL query language.  The total number triples available can be increased if the store also infers triples based on properties such as `owl:sameAs`, `rdfs:subClassOf`, `owl:TransitiveProperty` which relate explicitly declared triples. See [section 7.6.4.](Beginners7OWL#7.6.4._Statements_of_equivalence_in_OWL.md) and [section 7.6.5.](Beginners7OWL#7.6.5._OWL_property_characteristics.md) for more on these OWL properties.  For information on the storage cost of triples having non-literal objects vs. those having literal objects, see http://docs.openlinksw.com/virtuoso/virtuosofaq.html#virtuosofaq1 (thanks to Pete DeVries for pointing this out).

A user can set up a locally managed triple store for whatever purpose is desired.  The user can then choose which RDF sources to load into that store and exert quality control over those data by loading only sources which are trusted.  Examples are TaxonConcept [(21)](#21_TaxonConcept_datasets.md) and a TDWG-RDF/OWL Task Group sandbox. [(22)](#22_TDWG_RDF/OWL_Task_Group_sandbox.md)

There are also a number of "public" triple stores which scrape other sources and subsequently provide access to those data.  Dbpedia [(23)](#23_DBpedia_home_page.md) extracts data from Wikipedia and makes it available as RDF triples.  OpenLink has extracted [(24)](#24_OpenLink_Search.md) over 15 billion triples which are searchable.  Sindice provides a "Semantic Web Index" [(25)](#25_Sindice_Semantic_Web_Index.md) which accesses hundreds of millions of documents and makes the data in those documents available.  Adding data to one of the sources scraped by these organizations makes those triples publically accessible.  However, these sources are only as reliable as the data sources they include in their triplestore.

### 5.3.3. Providing information about the data which are available using VoID ###

VoID is a vocabulary for expressing metadata about RDF datasets [(26)](#26_Describing_Linked_Datasets_with_the_VoID_Vocabulary.md)  (`void: = http://rdfs.org/ns/void# `).   It provides basic information about the dataset, such as the project's homepage, name, publisher, size of dataset, etc.  The database description can also provide access information about documents which can serve as the starting point for crawling the database, SPARQL endpoints, and compressed or uncompressed RDF data dumps of the database content.  The description can also link to example resources which illustrate the types of data available.

Within the dataset description, the term `void:rootResource` can be used to describe one or a few central entry points for a dataset which could provide starting points for crawling the dataset.

Discovery of the dataset description can be supported by using the property `void:inDataset` in the description of an RDF document which is part of the dataset.  For example, if the document document.rdf is provided upon the dereferencing of a URI identifying an entity described by the dataset, the description of document.rdf could include the triple
```
http://example.org/document.rdf   void:inDataset   http://example.org/void.rdf#dataset
```

where ` http://example.org/void.rdf#dataset` represents the URI of the dataset and `http://example.org/void.rdf` is a retrievable document which contains the VoID description.

#### 5.3.3.1. Example ####
The following is a fragment from the file http://bioimages.vanderbilt.edu/index.rdf which illustrates how VoID terms can describe a dataset and link to an RSS summary of documents which can be crawled to obtain the data contained in the dataset.

```
In RDF/XML:
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:foaf="http://xmlns.com/foaf/0.1/"
xmlns:void="http://rdfs.org/ns/void#"
>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/">
   <dcterms:title>Bioimages image database</dcterms:title>
   <dcterms:description>This collection contains approximately 10 000 images, primarily of live plants, although a few other organisms are represented. There are also a number of images of North American ecoregions.</dcterms:description>
   <rdfs:type rdf:resource ="http://rdfs.org/ns/void#Dataset" />
   <dcterms:type rdf:resource ="http://purl.org/dc/dcmitype/Dataset" />
   <dcterms:creator rdf:resource="http://biocol.org/urn:lsid:biocol.org:col:35115"/>
   <dcterms:created>2002-10-21</dcterms:created>
   <foaf:homepage rdf:resource="http://bioimages.vanderbilt.edu/index.htm"/>

<!-- Relationships of the database to other resources.  -->
   <foaf:isPrimaryTopicOf rdf:resource="http://bioimages.vanderbilt.edu/index.rdf" />
   <foaf:isPrimaryTopicOf rdf:resource="http://bioimages.vanderbilt.edu/index.htm" />

   <void:exampleResource>
      <rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/66921">
         <dcterms:description>Image of Quercus lobata (Fagaceae) - whole tree (or vine) - general</dcterms:description>
         <rdfs:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>
      </rdf:Description>
   </void:exampleResource>

   <void:rootResource rdf:resource="http://bioimages.vanderbilt.edu/rdf/images.rss"/>
</rdf:Description>

<!-- Information about the metadata document itself -->
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/index.rdf">
   <dcterms:description>RDF formatted description of the Bioimages image database</dcterms:description>
   <dcterms:creator rdf:resource="http://biocol.org/urn:lsid:biocol.org:col:35115"/>
   <dcterms:language>en</dcterms:language>
   <dcterms:modified>2012-02-11</dcterms:modified>
   <dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/"/>
   <foaf:primaryTopic rdf:resource="http://bioimages.vanderbilt.edu/"/>
</rdf:Description>
</rdf:RDF>

In N3:
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix foaf: <http://xmlns.com/foaf/0.1/>.
@prefix void: <http://rdfs.org/ns/void#>.
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.
<http://bioimages.vanderbilt.edu/> 
	rdfs:type void:Dataset;
	dcterms:type <http://purl.org/dc/dcmitype/Dataset>;
	dcterms:created "2002-10-21";
	dcterms:creator <http://biocol.org/urn:lsid:biocol.org:col:35115>;
	dcterms:description "This collection contains approximately 10 000 images, primarily of live plants, although a few other organisms are represented. There are also a number of images of North American ecoregions.";
	dcterms:title "Bioimages image database";
	void:exampleResource <http://bioimages.vanderbilt.edu/baskauf/66921>;
	foaf:homepage <http://bioimages.vanderbilt.edu/index.htm>;
	void:rootResource <http://bioimages.vanderbilt.edu/rdf/images.rss>;
	foaf:isPrimaryTopicOf <http://bioimages.vanderbilt.edu/index.htm>,
		<http://bioimages.vanderbilt.edu/index.rdf>.

<http://bioimages.vanderbilt.edu/baskauf/66921> 
	rdfs:type <http://purl.org/dc/dcmitype/StillImage>;
	dcterms:description "Image of Quercus lobata (Fagaceae) - whole tree (or vine) - general".

<http://bioimages.vanderbilt.edu/index.rdf> 
	dcterms:creator <http://biocol.org/urn:lsid:biocol.org:col:35115>;
	dcterms:description "RDF formatted description of the Bioimages image database";
	dcterms:language "en";
	dcterms:modified "2012-02-11";
	dcterms:references <http://bioimages.vanderbilt.edu/>;
	foaf:primaryTopic <http://bioimages.vanderbilt.edu/>.
```

Note the following features of this description:
  * The dataset itself is identified by the URI `http://bioimages.vanderbilt.edu/`
  * The descriptive document is identified by the URI `http://bioimages.vanderbilt.edu/index.rdf` and that document is described separately from the dataset.
  * The collection is identified by its Biodiversity Collections Index identifier `http://biocol.org/urn:lsid:biocol.org:col:35115` (an HTTP proxied LSID) and is considered a distinct resource which is the creator and publisher of the dataset.
  * The HTML homepage of the website `http://bioimages.vanderbilt.edu/index.htm` is also a resource which is distinct from the three resources listed above.
  * `void:rootResource` is used to point to the RSS document which links to individual image records in the dataset
  * `void:exampleResource` is used to point to an example document which describes one of the image records in the dataset

If content negation were set up to redirect dereferencing requests for `http://bioimages.vanderbilt.edu/` preferring `content-type: application/rdf+xml` to the document `http://bioimages.vanderbilt.edu/index.rdf` (unfortunately it is not at the present), the property `<void:inDataset rdf:resource="http://bioimages.vanderbilt.edu/"/>` could be assigned to individual RDF image records as a backlink to the VoID database description file.

## 5.4. The Linked Open Data (LOD) Cloud ##

### 5.4.1. What is the LOD Cloud? ###
The "Linked Open Data" (LOD) or simply "Linked Data" model [(4)](#4_Linked_Data.md) embraces the idea that information (in the form of RDF triples) about resources identified by URIs is accessible through HTTP, and that links from one resource to another would permit the discovery of this information by machines (i.e. computer software).  In theory, these machines could collect and interpret this information to do useful things.  In this sense, the LOD "Cloud" (web of linked data) is the machine counterpart of the World Wide Web, which is designed to be understood by humans.

The LOD cloud doesn't exist in a single place any more than the Web does.  Like the Web, it exists as documents and databases on servers distributed around the world.  An RDF document or database sitting on an un-networked computer isn't any more a part of the LOD Cloud than an HTML document sitting on a desktop computer is a part of the Web.  The fact that the RDF can be retrieved through an attempt to dereference the URI of the resource described by the RDF is what makes the RDF part of the Cloud.

### 5.4.2. How can information be discovered in the Cloud? ###

#### 5.4.2.1. Linked Data browsers ####
Information in the form of triples can be discovered and collected in a manner similar to the way that web pages were discovered and read in the early Web: by accessing an RDF document through dereferencing a URI, then discovering additional triples by traversing links which dereference other URIs.  A Linked Data browser can be installed directly on a computer, or it can be accessed through a Web interface on a regular web browser.  The Linked Data browser may collect triples that it encounters during the session and refer to this cache later without the need to dereference the URI again.  The following URLs link to several web-based Linked Data browsers.  They are not always functional and they have differing abilities to dereference and follow links given in the collected metadata.  So a URI which dereferences easily on one browser may produce no results or an error message on another.  Good luck!

**OpenLink Data Explorer** (click Describe)

http://demo.openlinksw.com/rdfbrowser2/

**Zitgist**

http://dataviewer.zitgist.com/

**Marbles**

http://www5.wiwiss.fu-berlin.de/marbles/

**Disco**

http://www4.wiwiss.fu-berlin.de/rdf_browser/

#### 5.4.2.2. Linked Data scrapers ####
Some organizations actively search for and archive triples, then make them available through search interfaces or SPARQL queries [(see part 6)](Beginners6SPARQL.md).  This phenomenon is similar to web search engines which utilize Web Bots to crawl the Web, then index and cache what they find.  Here are some examples.

**Sindice Semantic Web Index**

Can be accessed through the Web interface sig.ma Semantic Information Mashup

http://sig.ma/search

**Ping the Semantic Web**

Can't be accessed through a web browser, but see http://pingthesemanticweb.com/api.php for setting up an interface.

**The Data Hub**

Operated by the Open Knowledge Foundation, the Data Hub is an index of useful sets of data on the Internet.  They do not all provide RDF, but publishing the URI of a site index file there makes it possible for your RDF to be "discovered".

http://thedatahub.org/


# References #

### 1. RFC 3986. Uniform Resource Identifier (URI): Generic Syntax ###

http://tools.ietf.org/html/rfc3986

### 2. Using International Standard Book Numbers as Uniform Resource Names ###

http://tools.ietf.org/html/rfc3187

### 3 References for LSIDs ###

http://xml.coverpages.org/lsid.html

LSID tester

http://darwin.zoology.gla.ac.uk/~rpage/lsid/tester/

LSID web resolver

http://lsid.tdwg.org/

Rod Page's LSID resolver

http://bioguid.info/lsid.php

### 4 Linked Data ###

http://linkeddata.org/

### 5 Internet media types ###
are also sometimes referred to as MIME (Multipurpose Internet Mail Extensions) types.

http://www.iana.org/assignments/media-types/index.html

### 6 owl:Class ###
In the XML serialization, using `owl:Class` as the name of the container element implicitly makes the `rdf:type` assertion.  In the Axiomatic Triples for the Classes of the OWL 2 RDF-Based Vocabulary, `owl:Class` is an `rdfs:subClassOf   rdfs:Class`.  So by inference this also makes the statement
```
http://lod.taxonconcept.org/ses/z9oqP#Species  rdf:type  rdfs:Class
```
In otherwords, this tells us that the resource is being defined indirectly to be an instance of `rdfs:Class`.

### 7 Protocol for Web Description Resources (POWDER) ###

http://www.w3.org/2007/05/powder-s

### 8 FOAF Vocabulary Specification ###

http://xmlns.com/foaf/spec/

### 9 Dublin Core RDF definitions ###

http://dublincore.org/2010/10/11/dcterms.rdf

### 10 RSS specification ###
The definition in RDF can be seen using "view page source" on a web browser.

http://web.resource.org/rss/1.0/

### 11 History of RSS in Wikipedia ###

It is now also known as Really Simple Syndication.

http://en.wikipedia.org/wiki/RSS

### 12 Publishing Web Data by Sindice ###

http://sindice.com/developers/publishing

### 13 The D2RQ Platform v0.7 user manual and language specification ###

http://www4.wiwiss.fu-berlin.de/bizer/D2RQ/spec/

http://www4.wiwiss.fu-berlin.de/bizer/d2rq/

### 14 D2RQ RDF data dumps ###

http://www4.wiwiss.fu-berlin.de/bizer/D2RQ/spec/#dumprdf

### 15 Virtuoso ###

http://virtuoso.openlinksw.com/dataspace/dav/wiki/Main/

http://virtuoso.openlinksw.com/white-papers/

### 16 Triplify ###

http://triplify.org/Overview

### 17 Triplifier ###

http://code.google.com/p/biscicol/

### 18 ezDBDB ###

http://xmalesia.info/ezdbdb/

### 19 Wikipedia article on triplestore ###

http://en.wikipedia.org/wiki/Triplestore

### 20 Large triplestores ###

http://www.w3.org/wiki/LargeTripleStores

### 21 TaxonConcept datasets ###

http://www.taxonconcept.org/sparql-endpoint/

### 22 TDWG RDF/OWL Task Group sandbox ###

http://tdwg-rdf.net/

### 23 DBpedia home page ###

http://dbpedia.org/About

### 24 OpenLink Search ###
http://lod.openlinksw.com/

### 25 Sindice Semantic Web Index ###
http://sindice.com/

The Sindice triplestore can be searched interactively using the Sig.ma Semantic Information Mashup which allows you to create a set of triples from multiple sources either cached by Sindice or loaded from URIs.

http://sig.ma/search

### 26 Describing Linked Datasets with the VoID Vocabulary ###
Note: VoID is not a W3C Recommendation.  However, it seems to be the primary existing vocabulary for describing linked datasets.

http://www.w3.org/TR/void/

http://vocab.deri.ie/void


---

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