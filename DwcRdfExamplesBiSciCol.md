![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Examples of Darwin Core as RDF using BiSciCol object properties #

**Date:** (Created) 1 July 2013; (Last modified) 26 November 2014

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** These examples follow the Darwin Core RDF Guide. They assume the data model of BiSciCol (http://biscicol.blogspot.com/ ) and use its object properties to link the class instances.  See http://code.google.com/p/tdwg-rdf/wiki/BiodiversityOntologies for a comparison of some data models that provide object terms that can be used with Darwin Core.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**


## 1 A specimen and its associated occurrence ##

<img src='http://tdwg-rdf.googlecode.com/svn/trunk/file/biscicol-specimen-obj-prop.png' height='200' width='3855' />

[Click here to view image in your default viewer](http://tdwg-rdf.googlecode.com/svn/trunk/file/biscicol-specimen-obj-prop.jpg)

This is a relatively simple example where an Occurrence is documented by a single PreservedSpecimen.  The BiSciCol model for interpreting Darwin Core archives is described at http://biscicol.blogspot.com/2013_03_01_archive.html and the BiSciCol terms are described at http://biscicol.org/terms/index.html .  In this example, the Event and Location instances are identified using the BCID system described at http://biscicol.blogspot.com/2013/05/sneak-peeks-biscicol-style.html . The `http://n2t.net/ark:/` IRIs do not actually represent the resources with which they are associated in this example - they are simply included to show the form of IRI used in the BCID system.

### 1.1 As RDF/XML: ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/biscicol-specimen.rdf).

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- 
This RDF is structured using BiSciCol object properties as described at http://biscicol.blogspot.com/2013_03_01_archive.html 
The BiSciCol Term Index is at biscicol.org/terms/index.html
Note: this example does not include an instance of Geological Context
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
xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#"
xmlns:bsc="http://biscicol.org/terms/index.html#"
xmlns:ro="http://www.obofoundry.org/ro/ro.owl#"
>
<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861">
     <!-- In the BiSciCol blog example, a specimen is considered a subclass of an occurrence, so typed as both here -->
     <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/PreservedSpecimen" />
     <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Occurrence" />
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
     <dwc:recordedBy>Oliver P. Pearson</dwc:recordedBy>
     <dwciri:recordedBy rdf:resource ="http://viaf.org/viaf/263074474" />
     <dwc:recordNumber>7101</dwc:recordNumber>
     <bsc:depends_on rdf:resource="http://n2t.net/ark:/21547/Et2" />
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
    <dwciri:toTaxonConcept rdf:resource="http://zoobank.org/306F5618-D154-47D5-81BB-697CB2A83EE7"/>
    <bsc:depends_on rdf:resource="http://zoobank.org/306F5618-D154-47D5-81BB-697CB2A83EE7"/>
    <bsc:depends_on rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861"/>
</rdf:Description>

<rdf:Description rdf:about="http://n2t.net/ark:/21547/Et2">
     <dwc:eventDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1983-11-16</dwc:eventDate>
     <rdf:type rdf:resource ="http://purl.org/dc/dcmitype/Event" />
     <bsc:related_to rdf:resource="http://n2t.net/ark:/21547/c2" />
</rdf:Description>

<rdf:Description rdf:about="http://n2t.net/ark:/21547/c2">
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
     <dcterms:references rdf:resource="http://n2t.net/ark:/21547/Et2"/>
     <dcterms:references rdf:resource="http://n2t.net/ark:/21547/c2"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson"/>
</rdf:Description>
</rdf:RDF>
```

### 1.2 As RDF/Turtle: ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/biscicol-specimen.ttl).

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
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>.
@prefix bsc: <http://biscicol.org/terms/index.html#>.
@prefix ro: <http://www.obofoundry.org/ro/ro.owl#>.

<http://arctos.database.museum/guid/MVZ:Mamm:165861> 
	dc:creator "University of California Berkeley Museum of Vertebrate Zoology";
	dcterms:created "1983-11-16"^^xsd:date;
	dcterms:creator <http://biocol.org/urn:lsid:biocol.org:col:34777>;
	dcterms:description "Preserved specimen http://arctos.database.museum/guid/MVZ:Mamm:165861"@en;
	dcterms:identifier 
		"http://arctos.database.museum/guid/MVZ:Mamm:165861",
		"MVZ:Mamm:165861";
	dcterms:type dcmitype:PhysicalObject;
	dwc:basisOfRecord "PreservedSpecimen";
	dwc:catalogNumber "165861";
	dwc:collectionCode "Mamm";
	dwc:institutionCode "MVZ";
	dwc:otherCatalogNumbers "12272";
	dwc:preparations "skin; skull; skeleton";
	dwc:recordNumber "7101";
	dwc:recordedBy "Oliver P. Pearson";
	dwc:sex "female";
	dwciri:inCollection <http://biocol.org/urn:lsid:biocol.org:col:34777>;
	dwciri:recordedBy <http://viaf.org/viaf/263074474>;
	bsc:depends_on <http://n2t.net/ark:/21547/Et2>;
	a 	dwc:Occurrence,
		dwc:PreservedSpecimen.
		
<http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson> 
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
	dwc:vernacularName 
		"colonial tuco-tuco"@en,
		"tuco-tuco colonial"@es;
	dwciri:identifiedBy <http://viaf.org/viaf/263074474>;
	dwciri:toTaxonConcept <http://zoobank.org/306F5618-D154-47D5-81BB-697CB2A83EE7>;
	bsc:depends_on 
		<http://arctos.database.museum/guid/MVZ:Mamm:165861>,
		<http://zoobank.org/306F5618-D154-47D5-81BB-697CB2A83EE7>;
	a dwc:Identification.
	
<http://n2t.net/ark:/21547/Et2> 
	dwc:eventDate "1983-11-16"^^xsd:date;
	bsc:related_to <http://n2t.net/ark:/21547/c2>;
	a dcmitype:Event.
                                
<http://n2t.net/ark:/21547/c2> 
	dwc:continent "South America";
	dwc:coordinateUncertaintyInMeters "30"^^xsd:int;
	dwc:country "Argentina";
	dwc:countryCode "AR";
	dwc:county "Los Lagos";
	dwc:decimalLatitude "-40.9684722"^^xsd:decimal;
	dwc:decimalLongitude "-71.1918056"^^xsd:decimal;
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

<http://arctos.database.museum/guid/MVZ:Mamm:165861.rdf> 
	dc:creator "Arctos Museum Database";
	dc:language "en";
	dcterms:description "RDF formatted descriptions";
	dcterms:language <http://id.loc.gov/vocabulary/languages/eng>;
	dcterms:modified "2013-06-27T10:26:34"^^xsd:dateTime;
	dcterms:references 
		<http://arctos.database.museum/guid/MVZ:Mamm:165861>,
		<http://arctos.database.museum/guid/MVZ:Mamm:165861#1999-01-27pearson>,
		<http://n2t.net/ark:/21547/Et2>,
		<http://n2t.net/ark:/21547/c2>;
	a foaf:Document.
```