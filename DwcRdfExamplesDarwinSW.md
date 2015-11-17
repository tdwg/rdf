![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Examples of Darwin Core as RDF using Darwin-SW object properties #

**Date:** (Created) 27 June 2013; (Last modified) 26 November 2014

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** These examples follow the Darwin Core RDF Guide. They assume the data model of Darwin-SW (version 0.3; http://code.google.com/p/darwin-sw/ ) and use its object properties to link the class instances.  See http://code.google.com/p/tdwg-rdf/wiki/BiodiversityOntologies for a comparison of some data models that provide object terms that can be used with Darwin Core.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**


## 1 A specimen and its associated occurrence ##

This is a relatively simple example where an Occurrence is documented by a single PreservedSpecimen

<img src='http://tdwg-rdf.googlecode.com/svn/trunk/file/specimen-obj-pro-only.png' height='200' width='3855' />

[Click here to view image in your default viewer](http://tdwg-rdf.googlecode.com/svn/trunk/file/specimen-obj-pro-only.jpg)

### 1.1 As RDF/XML ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/dsw-0-3-specimen.rdf).

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- 
This RDF is structured using object properties defined at http://code.google.com/p/darwin-sw/ version 0.3 
-->
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
xmlns:owl="http://www.w3.org/2002/07/owl#"
xmlns:dwc="http://rs.tdwg.org/dwc/terms/"
xmlns:dwciri="http://rs.tdwg.org/dwc/iri/"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcmitype="http://purl.org/dc/dcmitype/"
xmlns:foaf="http://xmlns.com/foaf/0.1/"
xmlns:ac="http://rs.tdwg.org/ac/terms/"
xmlns:xmp="http://ns.adobe.com/xap/1.0/"
xmlns:xmpRights="http://ns.adobe.com/xap/1.0/rights/"
xmlns:dsw="http://purl.org/dsw/"
xmlns:mix="http://www.loc.gov/mix/v20"
xmlns:bibo="http://purl.org/ontology/bibo/"
>
<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#ind">
     <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Organism" />
     <dwc:organismScope>multicellular organism</dwc:organismScope>
     <dcterms:type rdf:resource ="http://purl.org/dc/dcmitype/PhysicalObject" />
     <dcterms:description xml:lang="en">Organism http://arctos.database.museum/guid/MVZ:Mamm:165861#ind</dcterms:description>
     <dsw:hasIdentification rdf:resource ="http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson" />
     <dsw:hasOccurrence rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#occ" />
     <dsw:hasDerivative rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861" />
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson">
    <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Identification" />
    <dwc:identifiedBy>Oliver P. Pearson</dwc:identifiedBy>
    <dwciri:identifiedBy rdf:resource ="http://viaf.org/viaf/263074474" />
    <dwc:dateIdentified rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1999-01-27</dwc:dateIdentified>
    <dwc:scientificName>Ctenomys sociabilis Pearson and Christie, 1985</dwc:scientificName>
    <dwc:vernacularName xml:lang="en">colonial tuco-tuco</dwc:vernacularName>
    <dwc:vernacularName xml:lang="es">tuco-tuco colonial</dwc:vernacularName>
    <dwc:class>Mammalia</dwc:class>
    <dwc:order>Rodentia</dwc:order>
    <dwc:family>Ctenomyidae</dwc:family>
    <dwc:genus>Ctenomys</dwc:genus>
    <dwc:specificEpithet>sociabilis</dwc:specificEpithet>
    <dwc:typeStatus>holotype of Ctenomys sociabilis. Pearson O. P., and M. I. Christie. 1985. Historia Natural, 5(37):388</dwc:typeStatus>
    <dwc:scientificNameAuthorship>Pearson and Christie, 1985</dwc:scientificNameAuthorship>
    <dwc:namePublishedInYear>1985</dwc:namePublishedInYear>
    <dwc:taxonRank>species</dwc:taxonRank>
    <dwc:nameAccordingTo>Oliver P. Pearson. 1985. Los tuco-tucos (genera Ctenomys) de los Parques Nacionales Lanin y Nahuel Huapi, Argentina. Historia Natural 5(37):337-343.</dwc:nameAccordingTo>
    <dwc:identificationRemarks xml:lang="en">ID from citation in Pearson 1985.</dwc:identificationRemarks>
    <dwciri:toTaxon rdf:resource="http://zoobank.org/306F5618-D154-47D5-81BB-697CB2A83EE7"/>
    <dsw:identifies rdf:resource ="http://arctos.database.museum/guid/MVZ:Mamm:165861#ind" />
    <dsw:idBasedOn rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861"/>
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861">
     <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/PreservedSpecimen" />
     <dcterms:type rdf:resource ="http://purl.org/dc/dcmitype/PhysicalObject" />
     <dcterms:description xml:lang="en">Preserved specimen http://arctos.database.museum/guid/MVZ:Mamm:165861</dcterms:description>
     <dwc:basisOfRecord>PreservedSpecimen</dwc:basisOfRecord>
     <dc:creator>University of California Berkeley Museum of Vertebrate Zoology</dc:creator>
     <dcterms:creator rdf:resource="http://biocol.org/urn:lsid:biocol.org:col:34777" />
     <dcterms:created rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1983-11-16</dcterms:created>
     <dwc:institutionCode>MVZ</dwc:institutionCode>
     <dwc:collectionCode>Mamm</dwc:collectionCode>
     <dwc:catalogNumber>165861</dwc:catalogNumber>
     <dwc:otherCatalogNumbers>12272</dwc:otherCatalogNumbers>
     <dcterms:identifier>MVZ:Mamm:165861</dcterms:identifier>
     <dcterms:identifier>http://arctos.database.museum/guid/MVZ:Mamm:165861</dcterms:identifier>     
     <dwciri:inCollection rdf:resource ="http://biocol.org/urn:lsid:biocol.org:col:34777" />
     <dwc:preparations>skin; skull; skeleton</dwc:preparations>
     <dwc:sex>female</dwc:sex>
     <dsw:derivedFrom rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#ind" />
     <dsw:evidenceFor rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#occ" />
     <dsw:idBasisForId rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson"/>
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#occ">
     <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Occurrence" />
     <dwc:recordedBy>Oliver P. Pearson</dwc:recordedBy>
     <dwciri:recordedBy rdf:resource ="http://viaf.org/viaf/263074474" />
     <dwc:recordNumber>7101</dwc:recordNumber>
     <dsw:atEvent rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#eve" />
     <dsw:occurrenceOf rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#ind" />
     <dsw:hasEvidence rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861" />
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#eve">
     <dwc:eventDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1983-11-16</dwc:eventDate>
     <rdf:type rdf:resource ="http://purl.org/dc/dcmitype/Event" />
     <dsw:eventOf rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#occ" />
     <dsw:locatedAt rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#loc" />
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#loc">
     <rdf:type rdf:resource ="http://purl.org/dc/terms/Location" />
     <dwc:decimalLatitude rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">-40.9684722</dwc:decimalLatitude>
     <dwc:decimalLongitude rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">-71.1918056</dwc:decimalLongitude>
     <dwc:geodeticDatum>EPSG:4326</dwc:geodeticDatum>
     <dwc:minimumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">1075</dwc:minimumElevationInMeters>
     <dwc:maximumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">1075</dwc:maximumElevationInMeters>
     <dwc:coordinateUncertaintyInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">30</dwc:coordinateUncertaintyInMeters>
     <dwc:continent>South America</dwc:continent>
     <dwc:country>Argentina</dwc:country>
     <dwc:countryCode>AR</dwc:countryCode>
     <dwc:stateProvince>Neuquen</dwc:stateProvince>
     <dwc:county>Los Lagos</dwc:county>
     <dwc:locality>Estancia Fortin Chacabuco, 3 km S and 2 km W Cerro Puntudo, Depto. Los Lagos</dwc:locality>
     <dwc:verbatimLocality>Estancia Fortin Chacabuco, 3 km S and 2 km W Co. Puntudo</dwc:verbatimLocality>
     <dwc:locationRemarks xml:lang="en">The colony was just N of the fence and just E of the stream according to Michael Christie, who verified on Google Earth (about 40. 58' 06 to 07" and 71. 11' 30 to 31")</dwc:locationRemarks>
     <dwc:georeferenceSources>Google Earth (assumed v.6)</dwc:georeferenceSources>
     <dwc:georeferenceProtocol>MaNIS georeferencing guidelines</dwc:georeferenceProtocol>
     <dwciri:inDescribedPlace rdf:resource="http://sws.geonames.org/3846077/"/>
     <dsw:locates rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#eve" />
</rdf:Description>

<!--
Information about the metadata document itself
-->
<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861.rdf">
     <dcterms:description>RDF formatted descriptions</dcterms:description>
     <rdf:type rdf:resource ="http://xmlns.com/foaf/0.1/Document" />
     <dc:creator>Arctos Museum Database</dc:creator>
     <dc:language>en</dc:language>
     <dcterms:language rdf:resource="http://id.loc.gov/vocabulary/languages/eng" />
     <dcterms:modified rdf:datatype ="http://www.w3.org/2001/XMLSchema#dateTime">2013-06-27T10:26:34</dcterms:modified>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#occ"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#ind"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#eve"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#loc"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson"/>
</rdf:Description>
</rdf:RDF>
```

### 1.2 As RDF/Turtle ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/dsw-0-3-specimen.ttl).

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix owl: <http://www.w3.org/2002/07/owl#>.
@prefix dwc: <http://rs.tdwg.org/dwc/terms/>.
@prefix dwciri: <http://rs.tdwg.org/dwc/iri/>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix dc: <http://purl.org/dc/elements/1.1/>.
@prefix dcmitype: <http://purl.org/dc/dcmitype/>.
@prefix foaf: <http://xmlns.com/foaf/0.1/>.
@prefix ac: <http://rs.tdwg.org/ac/terms/>.
@prefix xmp: <http://ns.adobe.com/xap/1.0/>.
@prefix xmpRights: <http://ns.adobe.com/xap/1.0/rights/>.
@prefix dsw: <http://purl.org/dsw/>.
@prefix mix: <http://www.loc.gov/mix/v20>.
@prefix bibo: <http://purl.org/ontology/bibo/>.

<http://arctos.database.museum/guid/MVZ:Mamm:165861> 
	dc:creator "University of California Berkeley Museum of Vertebrate Zoology";
	dcterms:created "1983-11-16"^^xsd:date;
	dcterms:creator <http://biocol.org/urn:lsid:biocol.org:col:34777>;
	dcterms:description "Preserved specimen http://arctos.database.museum/guid/MVZ:Mamm:165861"@en;
	dcterms:identifier "http://arctos.database.museum/guid/MVZ:Mamm:165861",
	                "MVZ:Mamm:165861";
	dcterms:type dcmitype:PhysicalObject;
	dsw:derivedFrom <http://arctos.database.museum/guid/MVZ:Mamm:165861#ind>;
	dsw:evidenceFor <http://arctos.database.museum/guid/MVZ:Mamm:165861#occ>;
	dsw:idBasisForId <http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson>;
	dwc:basisOfRecord "PreservedSpecimen";
	dwc:catalogNumber "165861";
	dwc:collectionCode "Mamm";
	dwc:institutionCode "MVZ";
	dwc:otherCatalogNumbers "12272";
	dwc:preparations "skin; skull; skeleton";
	dwc:sex "female";
	dwciri:inCollection <http://biocol.org/urn:lsid:biocol.org:col:34777>;
	a dwc:PreservedSpecimen.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson> 
	dsw:idBasedOn <http://arctos.database.museum/guid/MVZ:Mamm:165861>;
	dsw:identifies <http://arctos.database.museum/guid/MVZ:Mamm:165861#ind>;
	dwc:class "Mammalia";
	dwc:dateIdentified "1999-01-27"^^xsd:date;
	dwc:family "Ctenomyidae";
	dwc:genus "Ctenomys";
	dwc:identificationRemarks "ID from citation in Pearson 1985."@en;
	dwc:identifiedBy "Oliver P. Pearson";
	dwc:nameAccordingTo "Oliver P. Pearson. 1985. Los tuco-tucos (genera Ctenomys) de los Parques Nacionales Lanin y Nahuel Huapi, Argentina. Historia Natural 5(37):337-343.";
	dwc:namePublishedInYear "1985";
	dwc:order "Rodentia";
	dwc:scientificName "Ctenomys sociabilis Pearson and Christie, 1985";
	dwc:scientificNameAuthorship "Pearson and Christie, 1985";
	dwc:specificEpithet "sociabilis";
	dwc:taxonRank "species";
	dwc:typeStatus "holotype of Ctenomys sociabilis. Pearson O. P., and M. I. Christie. 1985. Historia Natural, 5(37):388";
	dwc:vernacularName "colonial tuco-tuco"@en,
	                  "tuco-tuco colonial"@es;
	dwciri:identifiedBy <http://viaf.org/viaf/263074474>;
	dwciri:toTaxon <http://zoobank.org/306F5618-D154-47D5-81BB-697CB2A83EE7>;
	a dwc:Identification.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861#eve> 
	dsw:eventOf <http://arctos.database.museum/guid/MVZ:Mamm:165861#occ>;
	dsw:locatedAt <http://arctos.database.museum/guid/MVZ:Mamm:165861#loc>;
	dwc:eventDate "1983-11-16"^^xsd:date;
	a dcmitype:Event.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861#ind> 
	dcterms:description "Organism http://arctos.database.museum/guid/MVZ:Mamm:165861#ind"@en;
	dcterms:type dcmitype:PhysicalObject;
	dsw:hasDerivative <http://arctos.database.museum/guid/MVZ:Mamm:165861>;
	dsw:hasIdentification <http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson>;
	dsw:hasOccurrence <http://arctos.database.museum/guid/MVZ:Mamm:165861#occ>;
        dwc:organismScope "multicellular organism";
	a dwc:Organism.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861#loc> 
	dsw:locates <http://arctos.database.museum/guid/MVZ:Mamm:165861#eve>;
	dwc:continent "South America";
	dwc:coordinateUncertaintyInMeters "30"^^xsd:int;
	dwc:country "Argentina";
	dwc:countryCode "AR";
	dwc:county "Los Lagos";
	dwc:decimalLatitude -40.9684722;
	dwc:decimalLongitude -71.1918056;
	dwc:geodeticDatum "EPSG:4326";
	dwc:georeferenceProtocol "MaNIS georeferencing guidelines";
	dwc:georeferenceSources "Google Earth (assumed v.6)";
	dwc:locality "Estancia Fortin Chacabuco, 3 km S and 2 km W Cerro Puntudo, Depto. Los Lagos";
	dwc:locationRemarks """The colony was just N of the fence and just E of the stream according to Michael Christie, who verified on Google Earth (about 40. 58' 06 to 07\" and 71. 11' 30 to 31\")"""@en;
	dwc:maximumElevationInMeters "1075"^^xsd:int;
	dwc:minimumElevationInMeters "1075"^^xsd:int;
	dwc:stateProvince "Neuquen";
	dwc:verbatimLocality "Estancia Fortin Chacabuco, 3 km S and 2 km W Co. Puntudo";
	dwciri:inDescribedPlace <http://sws.geonames.org/3846077/>;
	a dcterms:Location.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861#occ> 
	dsw:atEvent <http://arctos.database.museum/guid/MVZ:Mamm:165861#eve>;
	dsw:hasEvidence <http://arctos.database.museum/guid/MVZ:Mamm:165861>;
	dsw:occurrenceOf <http://arctos.database.museum/guid/MVZ:Mamm:165861#ind>;
	dwc:recordNumber "7101";
	dwc:recordedBy "Oliver P. Pearson";
	dwciri:recordedBy <http://viaf.org/viaf/263074474>;
	a dwc:Occurrence.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861.rdf> 
	dc:creator "Arctos Museum Database";
	dc:language "en";
	dcterms:description "RDF formatted descriptions";
	dcterms:language <http://id.loc.gov/vocabulary/languages/eng>;
	dcterms:modified "2013-06-27T10:26:34"^^xsd:dateTime;
	dcterms:references <http://arctos.database.museum/guid/MVZ:Mamm:165861>,
	                <http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson>,
	                <http://arctos.database.museum/guid/MVZ:Mamm:165861#eve>,
	                <http://arctos.database.museum/guid/MVZ:Mamm:165861#ind>,
	                <http://arctos.database.museum/guid/MVZ:Mamm:165861#loc>,
	                <http://arctos.database.museum/guid/MVZ:Mamm:165861#occ>;
	a foaf:Document.
```

## 2 Complex example ##

This is a complex example based on a real situation where several images and a specimen were collected to document a seed collection.  It uses terms from Darwin Core and the draft Audubon Core for multimedia metadata.  The resource IRIs are real except for the specimen and the identification associated with it (a specimen was collected, but it's metadata are not yet available.)

In this example, two events are linked to a single location.  There are two occurrences (one associated with each event).  One occurrence is documented by a single image.  A later occurrence is documented by both a specimen and an image.  The Organism instance is a small population of plants, documented by the occurrences and from which the images and specimen were derived.  The population has two Identification instances.  One is based on the two images while the other is based on the specimen.  Each image has four ServiceAccessPoints from which size variants can be acquired. Although there are only several resources involved, it demonstrates how RDF can describe complex situations in a highly normalized way.

<img src='http://tdwg-rdf.googlecode.com/svn/trunk/file/images-obj-pro-only.png' height='200' width='3855' />

[Click here to view image in your default viewer](http://tdwg-rdf.googlecode.com/svn/trunk/file/images-obj-pro-only.jpg)

For the sake of simplicity, the diagram does not show the details of the ServiceAccessPoints.

### 2.1 As RDF/XML ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/dsw-0-3-images.rdf).

```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
xmlns:owl="http://www.w3.org/2002/07/owl#"
xmlns:dwc="http://rs.tdwg.org/dwc/terms/"
xmlns:dwciri="http://rs.tdwg.org/dwc/iri/"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcmitype="http://purl.org/dc/dcmitype/"
xmlns:foaf="http://xmlns.com/foaf/0.1/"
xmlns:ac="http://rs.tdwg.org/ac/terms/"
xmlns:xmp="http://ns.adobe.com/xap/1.0/"
xmlns:xmpRights="http://ns.adobe.com/xap/1.0/rights/"
xmlns:Iptc4xmpExt="http://iptc.org/std/Iptc4xmpExt/2008-02-29/"
xmlns:dsw="http://purl.org/dsw/"
xmlns:mix="http://www.loc.gov/mix/v20"
xmlns:mbank="http://www.morphbank.net/schema/morphbank#"
>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/ind-baskauf/87880">
	<rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Organism" />
	<!--Basic information about the organism-->
	<dcterms:identifier>http://bioimages.vanderbilt.edu/ind-baskauf/87880</dcterms:identifier>
	<dwc:organismRemarks xml:lang="en">Organism represents a small population within a radius of about 1 m.</dwc:organismRemarks>
	<dwc:organismScope>colony</dwc:organismScope>
	<!-- It is not clear exactly what establishmentMeans should be a property of.  Some say dwc:Occurrence rather than an Organism -->
	<dwc:establishmentMeans>native</dwc:establishmentMeans>
	
	<!-- Resources derived from the organism -->
	<foaf:depiction rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880"/>
	<foaf:depiction rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937"/>
	<dcterms:hasPart rdf:resource="http://apsc.apsu.edu/APSC:vascular:39274"/>
	<dsw:hasDerivative rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880"/>
	<dsw:hasDerivative rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937"/>
	<dsw:hasDerivative rdf:resource="http://apsc.apsu.edu/APSC:vascular:39274"/>
	
	<!-- Documented Occurrences of the organism -->
	<dsw:hasOccurrence rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#occ"/>
	<dsw:hasOccurrence rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#occ"/>
	
	<!-- Identifications applied to the organism-->
	<dsw:hasIdentification rdf:resource ="http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf" />
	<dsw:hasIdentification rdf:resource ="http://bioimages.vanderbilt.edu/ind-baskauf/35052#2013-08-21estesld" />
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf">
	<dcterms:description xml:lang="en">Determination of Hedyotis crassifolia Raf.  sensu Gleason Cronquist 1991 for the organism http://bioimages.vanderbilt.edu/ind-baskauf/87880</dcterms:description>
	<rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Identification" />
	<dwc:identifiedBy>Steven J. Baskauf</dwc:identifiedBy>
	<dwciri:identifiedBy rdf:resource ="http://viaf.org/viaf/63557389" />
	<dwc:dateIdentified rdf:datatype="http://www.w3.org/2001/XMLSchema#date">2013-05-08</dwc:dateIdentified>
    <dwc:scientificName>Hedyotis crassifolia Raf.</dwc:scientificName>
    <dwc:vernacularName xml:lang="en">small bluet</dwc:vernacularName>
    <dwc:family>Rubiaceae</dwc:family>
    <dwc:genus>Hedyotis</dwc:genus>
    <dwc:specificEpithet>crassifolia</dwc:specificEpithet>
    <dwc:scientificNameAuthorship>Raf.</dwc:scientificNameAuthorship>
    <dwc:taxonRank>species</dwc:taxonRank>
    <dwc:nameAccordingTo>Gleason, Henry A. and Arthur Cronquist, 1991. Manual of Vascular Plants of Northeastern United States and Adjacent Canada. The New York Botanical Garden, Bronx, NY, US. urn:isbn:0893273651</dwc:nameAccordingTo>

	<!-- Relationship of the determination to other resources -->
	<dsw:idBasedOn rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880"/>
	<dsw:idBasedOn rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937"/>
	<dsw:identifies rdf:resource ="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/ind-baskauf/35052#2013-08-21estesld">
	<dcterms:description xml:lang="en">Determination of Houstonia pusilla Schoepf sensu Terrell 1996 for the organism http://bioimages.vanderbilt.edu/ind-baskauf/87880</dcterms:description>
	<rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Identification" />
	<dwc:identifiedBy>L. Dwayne Estes</dwc:identifiedBy>
	<dwc:dateIdentified rdf:datatype="http://www.w3.org/2001/XMLSchema#date">2013-08-21</dwc:dateIdentified>
    <dwc:scientificName>Houstonia pusilla Schoepf</dwc:scientificName>
    <dwc:vernacularName xml:lang="en">tiny bluet</dwc:vernacularName>
    <dwc:family>Rubiaceae</dwc:family>
    <dwc:genus>Houstonia</dwc:genus>
    <dwc:specificEpithet>pusilla</dwc:specificEpithet>
    <dwc:scientificNameAuthorship>Schoepf</dwc:scientificNameAuthorship>
    <dwc:taxonRank>species</dwc:taxonRank>
    <dwc:nameAccordingTo>Terrell, Edward E., 1996. Revision of Houstonia (Rubiaceae-Hedyotideae). Systematic Botany Monographs 48:1-118 http://www.jstor.org/stable/25027862</dwc:nameAccordingTo>

	<!-- Relationship of the determination to other resources -->
	<dsw:idBasedOn rdf:resource="http://apsc.apsu.edu/APSC:vascular:39274"/>
	<dsw:identifies rdf:resource ="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880">
	<ac:metadataLanguage>en</ac:metadataLanguage>
	<!--Basic information about the image-->
	<rdf:type rdf:resource ="http://purl.org/dc/dcmitype/StillImage" />
	<dcterms:type rdf:resource ="http://purl.org/dc/dcmitype/StillImage" />
	<dcterms:identifier>http://bioimages.vanderbilt.edu/baskauf/87880</dcterms:identifier>
	<dc:creator>Steven J. Baskauf</dc:creator>
	<dcterms:creator rdf:resource ="http://viaf.org/viaf/63557389" />
	<dcterms:created rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2013-03-17T13:52:28</dcterms:created>
	<dwciri:inCollection rdf:resource ="http://biocol.org/urn:lsid:biocol.org:col:35115" />
	
	<!--Other properties of the image related to intellectual property rights, use and attribution guidelines, etc. -->
	<dc:rights>(c) 2013 Steven J. Baskauf</dc:rights>
	<xmpRights:owner>Steven J. Baskauf</xmpRights:owner>
	<Iptc4xmpExt:creditLine>Steven J. Baskauf http://bioimages.vanderbilt.edu/</Iptc4xmpExt:creditLine>
	<mbank:view>463267</mbank:view>
	<dcterms:title xml:lang="en">Hedyotis crassifolia (Rubiaceae) - whole plant - in flower - general view</dcterms:title>
	<xmpRights:UsageTerms xml:lang="en">Available under Creative Commons Attribution-Noncommercial-Share Alike 3.0 license</xmpRights:UsageTerms>
	<xmpRights:WebStatement>http://creativecommons.org/licenses/by-nc-sa/3.0/</xmpRights:WebStatement>
	<dcterms:description xml:lang="en">Image of Hedyotis crassifolia (Rubiaceae) - whole plant - in flower - general view</dcterms:description>
	<ac:attributionLinkURL>http://bioimages.vanderbilt.edu/contact/baskauf.htm</ac:attributionLinkURL>
	<ac:attributionLogoURL>http://bioimages.vanderbilt.edu/contact/baskauf-logo</ac:attributionLogoURL>
	
	<!-- Relationships of the image to other resources.  -->
	<foaf:isPrimaryTopicOf rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880.htm" />
	<dsw:derivedFrom rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
	<foaf:depicts rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
	<dsw:evidenceFor rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#occ" />
	<dsw:isBasisForId rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf"/>
	<!-- Links to ServiceAccessPoints -->
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#bq" />
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#tn" />
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#lq" />
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#gq" />
</rdf:Description>
	
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880#occ">
	<rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Occurrence" />
	<dwc:recordedBy>Steven J. Baskauf</dwc:recordedBy>
	<dwciri:recordedBy rdf:resource ="http://viaf.org/viaf/63557389" />
	<dsw:atEvent rdf:resource ="http://bioimages.vanderbilt.edu/baskauf/87880#eve" />
	<dsw:occurrenceOf rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
	<dsw:hasEvidence rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880" />
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880#eve">
	<rdf:type rdf:resource ="http://purl.org/dc/dcmitype/Event" />
	<dwc:eventDate rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2013-03-17T13:52:28</dwc:eventDate>
	<dsw:eventOf rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#occ" />
	<dsw:locatedAt rdf:resource ="http://bioimages.vanderbilt.edu/baskauf/87880#loc" />
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880#loc">
	<rdf:type rdf:resource ="http://purl.org/dc/terms/Location" />
	<dwc:decimalLatitude rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">36.38371</dwc:decimalLatitude>
	<dwc:decimalLongitude rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">-87.00771</dwc:decimalLongitude>
	<dwc:geodeticDatum>EPSG:4326</dwc:geodeticDatum>
	<dwc:minimumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">200</dwc:minimumElevationInMeters>
	<dwc:maximumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">200</dwc:maximumElevationInMeters>
	<dwc:coordinateUncertaintyInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">10</dwc:coordinateUncertaintyInMeters>
	<dwc:continent>North America</dwc:continent>
	<dwc:country>United States</dwc:country>
	<dwc:countryCode>US</dwc:countryCode>
	<dwc:stateProvince>Tennessee</dwc:stateProvince>
	<dwc:county>Cheatham</dwc:county>
	<dwc:locality>Keri Dr., Pleasant View</dwc:locality>
	<dwciri:inDescribedPlace rdf:resource="http://sws.geonames.org/4612891/"/>
	<dsw:locates rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#eve" />
	<dsw:locates rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#eve" />
</rdf:Description>

<!--
ServiceAccessPoints provide information about alternative versions of the image having different resolutions
-->
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880#bq">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Best Quality</ac:variant>
	<ac:accessURL>http://www.morphbank.net/?id=829502&amp;imgType=jpeg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">3456</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">2304</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880#tn">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Thumbnail</ac:variant>
	<ac:accessURL>http://bioimages.vanderbilt.edu/tn/baskauf/t87880.jpg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">100</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">67</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880#lq">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Lower Quality</ac:variant>
	<ac:accessURL>http://bioimages.vanderbilt.edu/lq/baskauf/w87880.jpg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">480</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">320</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87880#gq">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Good Quality</ac:variant>
	<ac:accessURL>http://bioimages.vanderbilt.edu/gq/baskauf/g87880.jpg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">1024</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">683</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87937">
	<ac:metadataLanguage>en</ac:metadataLanguage>
	<!--Basic information about the image-->
	<rdf:type rdf:resource ="http://purl.org/dc/dcmitype/StillImage" />
	<dcterms:type rdf:resource ="http://purl.org/dc/dcmitype/StillImage" />
	<dcterms:identifier>http://bioimages.vanderbilt.edu/baskauf/87937</dcterms:identifier>
	<dc:creator>Steven J. Baskauf</dc:creator>
	<dcterms:creator rdf:resource ="http://viaf.org/viaf/63557389" />
	<dcterms:created rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2013-04-29T18:31:15</dcterms:created>
	<dwciri:inCollection rdf:resource ="http://biocol.org/urn:lsid:biocol.org:col:35115" />
	
	<!--Other properties of the image related to intellectual property rights, use and attribution guidelines, etc. -->
	<dc:rights>(c) 2013 Steven J. Baskauf</dc:rights>
	<xmpRights:owner>Steven J. Baskauf</xmpRights:owner>
	<Iptc4xmpExt:creditLine>Steven J. Baskauf http://bioimages.vanderbilt.edu/</Iptc4xmpExt:creditLine>
	<mbank:view>463931</mbank:view>
	<dcterms:title xml:lang="en">Hedyotis crassifolia (Rubiaceae) - fruit - lateral or general close-up</dcterms:title>
	<xmpRights:UsageTerms xml:lang="en">Available under Creative Commons Attribution-Noncommercial-Share Alike 3.0 license</xmpRights:UsageTerms>
	<xmpRights:WebStatement>http://creativecommons.org/licenses/by-nc-sa/3.0/</xmpRights:WebStatement>
	<dcterms:description xml:lang="en">Image of Hedyotis crassifolia (Rubiaceae) - fruit - lateral or general close-up</dcterms:description>
	<ac:attributionLinkURL>http://bioimages.vanderbilt.edu/contact/baskauf.htm</ac:attributionLinkURL>
	<ac:attributionLogoURL>http://bioimages.vanderbilt.edu/contact/baskauf-logo</ac:attributionLogoURL>
	
	<!-- Relationships of the image to other resources.  -->
	<foaf:isPrimaryTopicOf rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937.htm" />
	<dsw:derivedFrom rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
	<foaf:depicts rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
	<dsw:evidenceFor rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#occ" />
	<dsw:isBasisForId rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf"/>
	<!-- Links to ServiceAccessPoints -->
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#bq" />
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#tn" />
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#lq" />
	<ac:hasServiceAccessPoint rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#gq" />
</rdf:Description>
	
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87937#occ">
	<rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Occurrence" />
	<dwc:recordedBy>Steven J. Baskauf</dwc:recordedBy>
	<dwciri:recordedBy rdf:resource ="http://viaf.org/viaf/63557389" />
	<dsw:atEvent rdf:resource ="http://bioimages.vanderbilt.edu/baskauf/87937#eve" />
	<dsw:occurrenceOf rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
	<dsw:hasEvidence rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937" />
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87937#eve">
	<rdf:type rdf:resource ="http://purl.org/dc/dcmitype/Event" />
	<dwc:eventDate rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2013-04-29T18:31:15</dwc:eventDate>
	<dsw:eventOf rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#occ" />
	<dsw:locatedAt rdf:resource ="http://bioimages.vanderbilt.edu/baskauf/87880#loc" />
</rdf:Description>

<!--
ServiceAccessPoints provide information about alternative versions of the image having different resolutions
-->
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87937#bq">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Best Quality</ac:variant>
	<ac:accessURL>http://www.morphbank.net/?id=829509&amp;imgType=jpeg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">2304</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">3456</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87937#tn">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Thumbnail</ac:variant>
	<ac:accessURL>http://bioimages.vanderbilt.edu/tn/baskauf/t87880.jpg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">67</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">100</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87937#lq">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Lower Quality</ac:variant>
	<ac:accessURL>http://bioimages.vanderbilt.edu/lq/baskauf/w87880.jpg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">320</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">480</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87937#gq">
	<rdf:type rdf:resource ="http://rs.tdwg.org/ac/type/ServiceAccessPoint" />
	<ac:variant>Good Quality</ac:variant>
	<ac:accessURL>http://bioimages.vanderbilt.edu/gq/baskauf/g87880.jpg</ac:accessURL>
	<dc:format>image/jpeg</dc:format>
	<mix:imageWidth rdf:datatype="http://www.w3.org/2001/XMLSchema#int">683</mix:imageWidth>
	<mix:imageHeight rdf:datatype="http://www.w3.org/2001/XMLSchema#int">1024</mix:imageHeight>
</rdf:Description>

<rdf:Description rdf:about="http://apsc.apsu.edu/APSC:vascular:39274">
	<rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/PreservedSpecimen" />
	<dcterms:type rdf:resource ="http://purl.org/dc/dcmitype/PhysicalObject" />
	<dcterms:description xml:lang="en">Preserved specimen http://apsc.apsu.edu/APSC:vascular:39274</dcterms:description>
	<dwc:basisOfRecord>PreservedSpecimen</dwc:basisOfRecord>
	<dc:creator>Austin Peay State University Herbarium (APSC)</dc:creator>
	<dcterms:creator rdf:resource="http://biocol.org/urn:lsid:biocol.org:col:xxxxx" />
	<dcterms:created rdf:datatype="http://www.w3.org/2001/XMLSchema#date">2013-08-21</dcterms:created>
	<dwc:institutionCode>APSC</dwc:institutionCode>
	<dwc:collectionCode>vascular</dwc:collectionCode>
	<dwc:catalogNumber>39274</dwc:catalogNumber>
	<dcterms:identifier>http://apsc.apsu.edu/APSC:vascular:39274</dcterms:identifier>     
	<dwciri:inCollection rdf:resource ="http://biocol.org/urn:lsid:biocol.org:col:xxxxx" />
	<dwc:preparations>whole plant - dried</dwc:preparations>
	<dcterms:isPartOf rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880"/>
	<dsw:derivedFrom rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880" />
	<dsw:evidenceFor rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#occ" />
	<dsw:isBasisForId rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/35052#2013-08-21estesld"/>
</rdf:Description>

<!--
Information about the metadata document itself
-->
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/ind-baskauf/87880.rdf">
	<rdf:type rdf:resource ="http://xmlns.com/foaf/0.1/Document" />
	<dcterms:identifier>http://bioimages.vanderbilt.edu/ind-baskauf/87880.rdf</dcterms:identifier>
	<dc:creator>Bioimages http://bioimages.vanderbilt.edu/</dc:creator>
	<dcterms:creator rdf:resource="http://biocol.org/urn:lsid:biocol.org:col:35115"/>
	<dc:language>en</dc:language>
	<dcterms:language rdf:resource="http://id.loc.gov/vocabulary/languages/eng"/>
	<dcterms:modified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2013-09-01T20:05:13</dcterms:modified>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#occ"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#eve"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#loc"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#bq"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#tn"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#lq"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87880#gq"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#occ"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#eve"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#bq"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#tn"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#lq"/>
	<dcterms:references rdf:resource="http://bioimages.vanderbilt.edu/baskauf/87937#gq"/>
	<dcterms:references rdf:resource="http://apsc.apsu.edu/APSC:vascular:39274"/>
</rdf:Description>
</rdf:RDF>
```

### 2.2 As RDF/Turtle ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/dsw-0-3-images.ttl).

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix owl: <http://www.w3.org/2002/07/owl#>.
@prefix dwc: <http://rs.tdwg.org/dwc/terms/>.
@prefix dwciri: <http://rs.tdwg.org/dwc/iri/>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix dc: <http://purl.org/dc/elements/1.1/>.
@prefix dcmitype: <http://purl.org/dc/dcmitype/>.
@prefix foaf: <http://xmlns.com/foaf/0.1/>.
@prefix ac: <http://rs.tdwg.org/ac/terms/>.
@prefix xmp: <http://ns.adobe.com/xap/1.0/>.
@prefix xmpRights: <http://ns.adobe.com/xap/1.0/rights/>.
@prefix Iptc4xmpExt: <http://iptc.org/std/Iptc4xmpExt/2008-02-29/>.
@prefix dsw: <http://purl.org/dsw/>.
@prefix mix: <http://www.loc.gov/mix/v20>.
@prefix mbank: <http://www.morphbank.net/schema/morphbank#>.

<http://bioimages.vanderbilt.edu/ind-baskauf/87880> 
	dcterms:hasPart <http://apsc.apsu.edu/APSC:vascular:39274>;
	dcterms:identifier "http://bioimages.vanderbilt.edu/ind-baskauf/87880";
	dsw:hasDerivative 
		<http://apsc.apsu.edu/APSC:vascular:39274>,
		<http://bioimages.vanderbilt.edu/baskauf/87880>,
		<http://bioimages.vanderbilt.edu/baskauf/87937>;
	dsw:hasIdentification 
		<http://bioimages.vanderbilt.edu/ind-baskauf/35052#2013-08-21estesld>,
		<http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf>;
	dsw:hasOccurrence 
		<http://bioimages.vanderbilt.edu/baskauf/87880#occ>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#occ>;
	dwc:organismRemarks "Organism represents a small population within a radius of about 1 m."@en;
        dwc:organismScope "colony";
	dwc:establishmentMeans "native";
	a dwc:Organism;
	foaf:depiction 
		<http://bioimages.vanderbilt.edu/baskauf/87880>,
		<http://bioimages.vanderbilt.edu/baskauf/87937>.
		
<http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf> 
	dcterms:description "Determination of Hedyotis crassifolia Raf.  sensu Gleason Cronquist 1991 for the organism http://bioimages.vanderbilt.edu/ind-baskauf/87880"@en;
	dsw:idBasedOn 
		<http://bioimages.vanderbilt.edu/baskauf/87880>,
		<http://bioimages.vanderbilt.edu/baskauf/87937>;
	dsw:identifies <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dwc:dateIdentified "2013-05-08"^^xsd:date;
	dwc:family "Rubiaceae";
	dwc:genus "Hedyotis";
	dwc:identifiedBy "Steven J. Baskauf";
	dwc:nameAccordingTo "Gleason, Henry A. and Arthur Cronquist, 1991. Manual of Vascular Plants of Northeastern United States and Adjacent Canada. The New York Botanical Garden, Bronx, NY, US. urn:isbn:0893273651";
	dwc:scientificName "Hedyotis crassifolia Raf.";
	dwc:scientificNameAuthorship "Raf.";
	dwc:specificEpithet "crassifolia";
	dwc:taxonRank "species";
	dwc:vernacularName "small bluet"@en;
	dwciri:identifiedBy <http://viaf.org/viaf/63557389>;
	a dwc:Identification.
	
<http://bioimages.vanderbilt.edu/ind-baskauf/35052#2013-08-21estesld> 
	dcterms:description "Determination of Houstonia pusilla Schoepf sensu Terrell 1996 for the organism http://bioimages.vanderbilt.edu/ind-baskauf/87880"@en;
	dsw:idBasedOn <http://apsc.apsu.edu/APSC:vascular:39274>;
	dsw:identifies <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dwc:dateIdentified "2013-08-21"^^xsd:date;
	dwc:family "Rubiaceae";
	dwc:genus "Houstonia";
	dwc:identifiedBy "L. Dwayne Estes";
	dwc:nameAccordingTo "Terrell, Edward E., 1996. Revision of Houstonia (Rubiaceae-Hedyotideae). Systematic Botany Monographs 48:1-118 http://www.jstor.org/stable/25027862";
	dwc:scientificName "Houstonia pusilla Schoepf";
	dwc:scientificNameAuthorship "Schoepf";
	dwc:specificEpithet "pusilla";
	dwc:taxonRank "species";
	dwc:vernacularName "tiny bluet"@en;
	a dwc:Identification.	
	
		
<http://bioimages.vanderbilt.edu/baskauf/87880#occ> 
	dsw:atEvent <http://bioimages.vanderbilt.edu/baskauf/87880#eve>;
	dsw:hasEvidence <http://bioimages.vanderbilt.edu/baskauf/87880>;
	dsw:occurrenceOf <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dwc:recordedBy "Steven J. Baskauf";
	dwciri:recordedBy <http://viaf.org/viaf/63557389>;
	a dwc:Occurrence.
<http://bioimages.vanderbilt.edu/baskauf/87880#eve> 
	dsw:eventOf <http://bioimages.vanderbilt.edu/baskauf/87880#occ>;
	dsw:locatedAt <http://bioimages.vanderbilt.edu/baskauf/87880#loc>;
	dwc:eventDate "2013-03-17T13:52:28"^^xsd:dateTime;
	a dcmitype:Event.
	
<http://bioimages.vanderbilt.edu/baskauf/87937#occ> 
	dsw:atEvent <http://bioimages.vanderbilt.edu/baskauf/87937#eve>;
	dsw:hasEvidence <http://bioimages.vanderbilt.edu/baskauf/87937>;
	dsw:occurrenceOf <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dwc:recordedBy "Steven J. Baskauf";
	dwciri:recordedBy <http://viaf.org/viaf/63557389>;
	a dwc:Occurrence.
<http://bioimages.vanderbilt.edu/baskauf/87937#eve> 
	dsw:eventOf <http://bioimages.vanderbilt.edu/baskauf/87937#occ>;
	dsw:locatedAt <http://bioimages.vanderbilt.edu/baskauf/87880#loc>;
	dwc:eventDate "2013-04-29T18:31:15"^^xsd:dateTime;
	a dcmitype:Event.
	
<http://bioimages.vanderbilt.edu/baskauf/87880#loc> 
	dsw:locates 
		<http://bioimages.vanderbilt.edu/baskauf/87880#eve>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#eve>;
	dwc:continent "North America";
	dwc:coordinateUncertaintyInMeters "10"^^xsd:int;
	dwc:country "United States";
	dwc:countryCode "US";
	dwc:county "Cheatham";
	dwc:decimalLatitude 36.38371;
	dwc:decimalLongitude -87.00771;
	dwc:geodeticDatum "EPSG:4326";
	dwc:locality "Keri Dr., Pleasant View";
	dwc:maximumElevationInMeters "200"^^xsd:int;
	dwc:minimumElevationInMeters "200"^^xsd:int;
	dwc:stateProvince "Tennessee";
	dwciri:inDescribedPlace <http://sws.geonames.org/4612891/>;
	a dcterms:Location.


<http://bioimages.vanderbilt.edu/baskauf/87880> 
	Iptc4xmpExt:creditLine "Steven J. Baskauf http://bioimages.vanderbilt.edu/";
	xmpRights:UsageTerms "Available under Creative Commons Attribution-Noncommercial-Share Alike 3.0 license"@en;
	xmpRights:WebStatement "http://creativecommons.org/licenses/by-nc-sa/3.0/";
	xmpRights:owner "Steven J. Baskauf";
	dc:creator "Steven J. Baskauf";
	dc:rights "(c) 2013 Steven J. Baskauf";
	dcterms:created "2013-03-17T13:52:28"^^xsd:dateTime;
	dcterms:creator <http://viaf.org/viaf/63557389>;
	dcterms:description "Image of Hedyotis crassifolia (Rubiaceae) - whole plant - in flower - general view"@en;
	dcterms:identifier "http://bioimages.vanderbilt.edu/baskauf/87880";
	dcterms:title "Hedyotis crassifolia (Rubiaceae) - whole plant - in flower - general view"@en;
	dcterms:type dcmitype:StillImage;
	dsw:derivedFrom <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dsw:evidenceFor <http://bioimages.vanderbilt.edu/baskauf/87880#occ>;
	dsw:isBasisForId <http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf>;
	ac:attributionLinkURL "http://bioimages.vanderbilt.edu/contact/baskauf.htm";
	ac:attributionLogoURL "http://bioimages.vanderbilt.edu/contact/baskauf-logo";
	ac:hasServiceAccessPoint 
		<http://bioimages.vanderbilt.edu/baskauf/87880#bq>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#gq>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#lq>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#tn>;
	ac:metadataLanguage "en";
	dwciri:inCollection <http://biocol.org/urn:lsid:biocol.org:col:35115>;
	mbank:view "463267";
	a dcmitype:StillImage;
	foaf:depicts <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	foaf:isPrimaryTopicOf <http://bioimages.vanderbilt.edu/baskauf/87880.htm>.
	
<http://bioimages.vanderbilt.edu/baskauf/87880#bq> 
	dc:format "image/jpeg";
	ac:accessURL "http://www.morphbank.net/?id=829502&imgType=jpeg";
	ac:variant "Best Quality";
	mix:imageHeight "2304"^^xsd:int;
	mix:imageWidth "3456"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
<http://bioimages.vanderbilt.edu/baskauf/87880#gq> 
	dc:format "image/jpeg";
	ac:accessURL "http://bioimages.vanderbilt.edu/gq/baskauf/g87880.jpg";
	ac:variant "Good Quality";
	mix:imageHeight "683"^^xsd:int;
	mix:imageWidth "1024"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
<http://bioimages.vanderbilt.edu/baskauf/87880#lq> 
	dc:format "image/jpeg";
	ac:accessURL "http://bioimages.vanderbilt.edu/lq/baskauf/w87880.jpg";
	ac:variant "Lower Quality";
	mix:imageHeight "320"^^xsd:int;
	mix:imageWidth "480"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
<http://bioimages.vanderbilt.edu/baskauf/87880#tn> 
	dc:format "image/jpeg";
	ac:accessURL "http://bioimages.vanderbilt.edu/tn/baskauf/t87880.jpg";
	ac:variant "Thumbnail";
	mix:imageHeight "67"^^xsd:int;
	mix:imageWidth "100"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
	
<http://bioimages.vanderbilt.edu/baskauf/87937> 
	Iptc4xmpExt:creditLine "Steven J. Baskauf http://bioimages.vanderbilt.edu/";
	xmpRights:UsageTerms "Available under Creative Commons Attribution-Noncommercial-Share Alike 3.0 license"@en;
	xmpRights:WebStatement "http://creativecommons.org/licenses/by-nc-sa/3.0/";
	xmpRights:owner "Steven J. Baskauf";
	dc:creator "Steven J. Baskauf";
	dc:rights "(c) 2013 Steven J. Baskauf";
	dcterms:created "2013-04-29T18:31:15"^^xsd:dateTime;
	dcterms:creator <http://viaf.org/viaf/63557389>;
	dcterms:description "Image of Hedyotis crassifolia (Rubiaceae) - fruit - lateral or general close-up"@en;
	dcterms:identifier "http://bioimages.vanderbilt.edu/baskauf/87937";
	dcterms:title "Hedyotis crassifolia (Rubiaceae) - fruit - lateral or general close-up"@en;
	dcterms:type dcmitype:StillImage;
	dsw:derivedFrom <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dsw:evidenceFor <http://bioimages.vanderbilt.edu/baskauf/87937#occ>;
	dsw:isBasisForId <http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf>;
	ac:attributionLinkURL "http://bioimages.vanderbilt.edu/contact/baskauf.htm";
	ac:attributionLogoURL "http://bioimages.vanderbilt.edu/contact/baskauf-logo";
	ac:hasServiceAccessPoint 
		<http://bioimages.vanderbilt.edu/baskauf/87937#bq>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#gq>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#lq>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#tn>;
	ac:metadataLanguage "en";
	dwciri:inCollection <http://biocol.org/urn:lsid:biocol.org:col:35115>;
	mbank:view "463931";
	a dcmitype:StillImage;
	foaf:depicts <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	foaf:isPrimaryTopicOf <http://bioimages.vanderbilt.edu/baskauf/87937.htm>.
	
<http://bioimages.vanderbilt.edu/baskauf/87937#bq> 
	dc:format "image/jpeg";
	ac:accessURL "http://www.morphbank.net/?id=829509&imgType=jpeg";
	ac:variant "Best Quality";
	mix:imageHeight "3456"^^xsd:int;
	mix:imageWidth "2304"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
<http://bioimages.vanderbilt.edu/baskauf/87937#gq> 
	dc:format "image/jpeg";
	ac:accessURL "http://bioimages.vanderbilt.edu/gq/baskauf/g87880.jpg";
	ac:variant "Good Quality";
	mix:imageHeight "1024"^^xsd:int;
	mix:imageWidth "683"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
<http://bioimages.vanderbilt.edu/baskauf/87937#lq> 
	dc:format "image/jpeg";
	ac:accessURL "http://bioimages.vanderbilt.edu/lq/baskauf/w87880.jpg";
	ac:variant "Lower Quality";
	mix:imageHeight "480"^^xsd:int;
	mix:imageWidth "320"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
<http://bioimages.vanderbilt.edu/baskauf/87937#tn> 
	dc:format "image/jpeg";
	ac:accessURL "http://bioimages.vanderbilt.edu/tn/baskauf/t87880.jpg";
	ac:variant "Thumbnail";
	mix:imageHeight "100"^^xsd:int;
	mix:imageWidth "67"^^xsd:int;
	a <http://rs.tdwg.org/ac/type/ServiceAccessPoint>.
	
	
<http://apsc.apsu.edu/APSC:vascular:39274> 
	dc:creator "Austin Peay State University Herbarium (APSC)";
	dcterms:created "2013-08-21"^^xsd:date;
	dcterms:creator <http://biocol.org/urn:lsid:biocol.org:col:xxxxx>;
	dcterms:description "Preserved specimen http://apsc.apsu.edu/APSC:vascular:39274"@en;
	dcterms:identifier "http://apsc.apsu.edu/APSC:vascular:39274";
	dcterms:isPartOf <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dcterms:type dcmitype:PhysicalObject;
	dsw:derivedFrom <http://bioimages.vanderbilt.edu/ind-baskauf/87880>;
	dsw:evidenceFor <http://bioimages.vanderbilt.edu/baskauf/87937#occ>;
	dsw:isBasisForId <http://bioimages.vanderbilt.edu/ind-baskauf/35052#2013-08-21estesld>;
	dwc:basisOfRecord "PreservedSpecimen";
	dwc:catalogNumber "39274";
	dwc:collectionCode "vascular";
	dwc:institutionCode "APSC";
	dwc:preparations "whole plant - dried";
	dwciri:inCollection <http://biocol.org/urn:lsid:biocol.org:col:xxxxx>;
	a dwc:PreservedSpecimen.
	

<http://bioimages.vanderbilt.edu/ind-baskauf/87880.rdf> 
	dc:creator "Bioimages http://bioimages.vanderbilt.edu/";
    dc:language "en";
    dcterms:creator <http://biocol.org/urn:lsid:biocol.org:col:35115>;
    dcterms:identifier "http://bioimages.vanderbilt.edu/ind-baskauf/87880.rdf";
    dcterms:language <http://id.loc.gov/vocabulary/languages/eng>;
    dcterms:modified "2013-09-01T20:05:13"^^xsd:dateTime;
    dcterms:references 
    	<http://apsc.apsu.edu/APSC:vascular:39274>,
		<http://bioimages.vanderbilt.edu/baskauf/87880>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#bq>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#eve>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#gq>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#loc>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#lq>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#occ>,
		<http://bioimages.vanderbilt.edu/baskauf/87880#tn>,
		<http://bioimages.vanderbilt.edu/baskauf/87937>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#bq>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#eve>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#gq>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#lq>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#occ>,
		<http://bioimages.vanderbilt.edu/baskauf/87937#tn>,
		<http://bioimages.vanderbilt.edu/ind-baskauf/87880>,
		<http://bioimages.vanderbilt.edu/ind-baskauf/87880#2013-05-08baskauf>;
a foaf:Document.
```