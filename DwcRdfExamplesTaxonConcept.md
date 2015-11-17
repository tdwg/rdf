![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Examples of Darwin Core as RDF using TaxonConcept Ontology object properties #

**Date:** (Created) 30 June 2013; (Last modified) 26 November 2014

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** These examples follow the Darwin Core RDF Guide. They assume the data model of the TaxonConcept Ontology (http://www.taxonconcept.org/ ) and use its object properties to link the class instances.  See http://code.google.com/p/tdwg-rdf/wiki/BiodiversityOntologies for a comparison of some data models that provide object terms that can be used with Darwin Core.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**


This example describes the specimen which is referenced in the Darwin Core RDF Guide, http://arctos.database.museum/guid/MVZ:Mamm:165861 using the data model of the TaxonConcept Ontology (http://www.taxonconcept.org/ see also http://code.google.com/p/tdwg-rdf/wiki/TaxonConceptOntologyDiagrams for additional information) written by Peter DeVries.  Since this is an example of an application of the use of Darwin Core terms according to the Guide, it does not make use of many of the properties that are available in the TaxonConcept Ontology.  For instance, it does not make use of the lightweight tags defined for various kinds of resources which type those resources as instances of that kind of resource class for the particular species (e.g. an occurrence of _Ctenomys sociabilis_).

In some cases, the TaxonConcept object properties have range and domain properties which assert types present in the TaxonConcept Ontology.  In recognition of that, the resources have been explicitly typed as instances of TaxonConcept Ontology classes as well as of the Darwin Core type vocabulary classes recommended in the Darwin Core RDF Guide.

For an example of an occurrence record marked up using the TaxonConcept Ontology exclusively, see http://ocs.taxonconcept.org/ocs/f522444a-2dd9-400e-be59-47213ef38cb9.rdf .  That file was used as a reference for the creation of this example.  In that example, the occurrence was documented by an image and the basisOfRecord was given as the image.  It is not clear whether the example given here is correct in including the specimen information as part of the metadata for the occurrence instance (there is no known property for relating occurrences to specimens in the ontology). Thus this use reflects the conceptual view that specimens are subClassOf occurrence, which is not necessarily the view of the TaxonConcept Ontology.

Also note that the taxon concept to which the `dwciri:toTaxon` property links is not specifically based on the TDWG TCS Model, but on the somewhat broader view of a taxon concept that is embodied in the TaxonConcept Ontology.

## 1 A specimen and its associated occurrence ##

This is a relatively simple example where an Occurrence is documented by a single PreservedSpecimen

<img src='http://tdwg-rdf.googlecode.com/svn/trunk/file/taxonconcept-specimen-obj-prop.png' height='200' width='3855' />

[Click here to view image in your default viewer](http://tdwg-rdf.googlecode.com/svn/trunk/file/taxonconcept-specimen-obj-prop.jpg)

### 1.1 As RDF/XML ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/taxonconcept-occurrence.rdf).

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
xmlns:dsw="http://purl.org/dsw/"
xmlns:mix="http://www.loc.gov/mix/v20"
xmlns:bibo="http://purl.org/ontology/bibo/"
xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#"
xmlns:txn="http://lod.taxonconcept.org/ontology/txn.owl#"
>
<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual">
     <rdf:type rdf:resource ="http://lod.taxonconcept.org/ontology/txn.owl#SpeciesIndividual" />
     <dcterms:type rdf:resource ="http://purl.org/dc/dcmitype/PhysicalObject" />
     <dcterms:description xml:lang="en">Individual organism http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual</dcterms:description>
     <txn:individualHasCurrentIdentificationAssertion rdf:resource ="http://arctos.database.museum/guid/MVZ:Mamm:165861#Identification_0001" />
     <txn:individualHasOccurrence rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence" />
     <txn:individualHasSpeciesConcept rdf:resource ="http://lod.taxonconcept.org/ses/3tYE7#Species" />
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#Identification_0001">
    <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Identification" />
    <rdf:type rdf:resource ="http://lod.taxonconcept.org/ontology/txn.owl#Identification" />
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
    <dwciri:toTaxon rdf:resource="http://lod.taxonconcept.org/ses/3tYE7#Species"/>
    <txn:identificationHasSpeciesConcept rdf:resource="http://lod.taxonconcept.org/ses/3tYE7#Species"/>
    <txn:identificationOfIndividual rdf:resource ="http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual" />
    <txn:identificationHasOccurrence rdf:resource ="http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence" />
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence">
     <!-- This example combines the metadata for the Occurrence and PreservedSpecimen (i.e. considers the specimen to be an occurrence) -->
     <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/PreservedSpecimen" />
     <rdf:type rdf:resource ="http://rs.tdwg.org/dwc/terms/Occurrence" />
     <rdf:type rdf:resource ="http://lod.taxonconcept.org/ontology/txn.owl#Occurrence" />
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
     <!-- the TaxonConcept Ontology does not represent Event as a separate class -->
     <dwc:eventDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1983-11-16</dwc:eventDate>
     <txn:startDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1983-11-16</txn:startDate>
     <txn:endDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1983-11-16</txn:endDate>     
     <txn:occurrenceHasIndividual rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual" />
     <txn:occurrenceHasSpeciesConcept rdf:resource="http://lod.taxonconcept.org/ses/3tYE7#Species" />
     <txn:occurrenceHasArea rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Area" />
</rdf:Description>

<rdf:Description rdf:about="http://arctos.database.museum/guid/MVZ:Mamm:165861#Area">
     <rdf:type rdf:resource ="http://purl.org/dc/terms/Location" />
     <rdf:type rdf:resource ="http://lod.taxonconcept.org/ontology/txn.owl#Area" />
     <dwc:decimalLatitude rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">-40.9684722</dwc:decimalLatitude>
     <dwc:decimalLongitude rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">-71.1918056</dwc:decimalLongitude>
     <dwc:geodeticDatum>EPSG:4326</dwc:geodeticDatum>
     <dwc:minimumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">1075</dwc:minimumElevationInMeters>
     <dwc:maximumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">1075</dwc:maximumElevationInMeters>
     <dwc:coordinateUncertaintyInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#int">30</dwc:coordinateUncertaintyInMeters>
     <owl:sameAs rdf:resource="http://www.w3.org/2003/01/geo/wgs84_pos#-40.9684722,-71.1918056;u=30" />
     <geo:lat rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">-40.9684722</geo:lat>
     <geo:long rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">-71.1918056</geo:long>
     <geo:alt rdf:datatype="http://www.w3.org/2001/XMLSchema#int">1075</geo:alt>
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
     <txn:areaHasOccurrence rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence" />
     <txn:areaHasIndividual rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual" />
     <txn:areaHasObservedSpeciesConcept rdf:resource="http://lod.taxonconcept.org/ses/3tYE7#Species" />
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
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Identification_0001"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence"/>
     <dcterms:references rdf:resource="http://arctos.database.museum/guid/MVZ:Mamm:165861#Area"/>
</rdf:Description>
</rdf:RDF>
```

### 1.2 As RDF/Turtle ###

Download [this file](http://tdwg-rdf.googlecode.com/svn/trunk/example/taxonconcept-occurrence.ttl).

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
@prefix txn: <http://lod.taxonconcept.org/ontology/txn.owl#>.

<http://arctos.database.museum/guid/MVZ:Mamm:165861#Area> 
	txn:areaHasIndividual <http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual>;
	txn:areaHasObservedSpeciesConcept <http://lod.taxonconcept.org/ses/3tYE7#Species>;
	txn:areaHasOccurrence <http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence>;
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
	a 	txn:Area,
	dcterms:Location;
	owl:sameAs <http://www.w3.org/2003/01/geo/wgs84_pos#-40.9684722,-71.1918056;u=30>;
	geo:alt "1075"^^xsd:int;
	geo:lat "-40.9684722"^^xsd:decimal;
	geo:long "-71.1918056"^^xsd:decimal.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861#Identification_0001> 
	txn:identificationHasOccurrence <http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence>;
	txn:identificationHasSpeciesConcept <http://lod.taxonconcept.org/ses/3tYE7#Species>;
	txn:identificationOfIndividual <http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual>;
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
	dwciri:toTaxon <http://lod.taxonconcept.org/ses/3tYE7#Species>;
	a 	txn:Identification,
		dwc:Identification.
		
<http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual> 
	txn:individualHasCurrentIdentificationAssertion <http://arctos.database.museum/guid/MVZ:Mamm:165861#Identification_0001>;
	txn:individualHasOccurrence <http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence>;
	txn:individualHasSpeciesConcept <http://lod.taxonconcept.org/ses/3tYE7#Species>;
	dcterms:description "Individual organism http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual"@en;
	dcterms:type dcmitype:PhysicalObject;
	a 	txn:SpeciesIndividual.
	
<http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence> 
	txn:endDate "1983-11-16"^^xsd:date;
	txn:occurrenceHasArea <http://arctos.database.museum/guid/MVZ:Mamm:165861#Area>;
	txn:occurrenceHasIndividual <http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual>;
	txn:occurrenceHasSpeciesConcept <http://lod.taxonconcept.org/ses/3tYE7#Species>;
	txn:startDate "1983-11-16"^^xsd:date;
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
	dwc:eventDate "1983-11-16"^^xsd:date;
	dwc:institutionCode "MVZ";
	dwc:otherCatalogNumbers "12272";
	dwc:preparations "skin; skull; skeleton";
	dwc:recordNumber "7101";
	dwc:recordedBy "Oliver P. Pearson";
	dwc:sex "female";
	dwciri:inCollection <http://biocol.org/urn:lsid:biocol.org:col:34777>;
	dwciri:recordedBy <http://viaf.org/viaf/263074474>;
	a 	txn:Occurrence,
		dwc:Occurrence,
		dwc:PreservedSpecimen.
		
<http://arctos.database.museum/guid/MVZ:Mamm:165861.rdf> 
	dc:creator "Arctos Museum Database";
	dc:language "en";
	dcterms:description "RDF formatted descriptions";
	dcterms:language <http://id.loc.gov/vocabulary/languages/eng>;
	dcterms:modified "2013-06-27T10:26:34"^^xsd:dateTime;
	dcterms:references 
		<http://arctos.database.museum/guid/MVZ:Mamm:165861#Area>,
		<http://arctos.database.museum/guid/MVZ:Mamm:165861#Identification_0001>,
		<http://arctos.database.museum/guid/MVZ:Mamm:165861#Individual>,
		<http://arctos.database.museum/guid/MVZ:Mamm:165861#Occurrence>;
	a foaf:Document.
```