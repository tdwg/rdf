**Contents**



## Introduction ##

In response to [Rod Page's challenge](http://lists.tdwg.org/pipermail/tdwg-tag/2011-September/002381.html), in follow-up to [discussions on creating a biodiversity RDF sandbox](http://piratepad.net/iEvoBio11-BoF-reportouts), and in furtherance of our mission, we will load as much biodiversity data as we can into a triplestore. We'll use this page to inventory the data we probably want to include. Where possible, include links to rdf representations of the data (data dumps, sparql endpoints, etc.)

## Biodiversity RDF datasets and other semantic web infrastructure ##

  * taxonconcept.org http://www.taxonconcept.org/sparql-endpoint/ This SPARQL endpoint has 23 million triples and includes some other related databases. Queries can be done directly on that endpoint at http://lsd.taxonconcept.org/sparql for a generic web interface and at http://lsd.taxonconcept.org/isparql for a human-friendly interface.  Datasets include the Global Name Index (GNI), DBpedia, geonames, etc. in addition to Pete's taxonconcept.org database.
  * Natural Solutions virtuoso triple store: so far we have put in Rod's datasets on frogs. http://82.96.149.133:8890/sparql
Feel Free to play with the SPARQL interface.

### Specimens at Royal Botanic Garden Edinburgh ###

Described in Hyam, R.D., Drinkwater, R.E. & Harris, D.J. Stable citations for herbarium specimens on the internet: an illustration from a taxonomic revision of Duboscia (Malvaceae) Phytotaxa 73: 17–30 (2012). http://www.mapress.com/phytotaxa/content/2012/f/pt00073p030.pdf

Example resource: http://data.rbge.org.uk/herb/E00435912 which dereferences to a web page or RDF/XML via a 303 redirect.

RDF/XML:
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:tap="http://rs.tdwg.org/tapir/1.0"
xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:hyam="http://hyam.net/tapir2sw#"
xmlns:dwc="http://rs.tdwg.org/dwc/terms/" xmlns:dwcc="http://rs.tdwg.org/dwc/curatorial/"
xmlns:dc="http://purl.org/dc/terms/"
xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#">

<!--This is metadata about this metadata document-->
<rdf:Description
rdf:about="http://data.rbge.org.uk/service/rdf/herb.php?guid=http://data.rbge.org.uk/herb/E00435912">
<dc:creator>Simple PHP RDF Script</dc:creator>
<dc:created>2013-11-10T01:46:58+00:00</dc:created>
<dc:hasVersion rdf:resource="http://elmer.rbge.org.uk/bgbase/vherb/bgbasevherb.php?cfg=bgbase/vherb/fulldetails.cfg%26amp;specimens_specimen__num=E00435912" />
</rdf:Description>

<!--This is metadata about this specimen-->
<rdf:Description rdf:about="http://data.rbge.org.uk/herb/E00435912">

<!-- Assertions made in simple Dublin Core -->
<dc:title>Goldsmith, M. #207 Duboscia macrocarpa Bocq.</dc:title>
<dc:description>A herbarium specimen of Duboscia macrocarpa Bocq. collected by Goldsmith, M. #207 </dc:description>
<dc:creator>Goldsmith, M.</dc:creator>
<dc:created>1973</dc:created>

<!-- <geo:Point> -->
<geo:lat>2.866667</geo:lat>
<geo:long>16.466667</geo:long>
<!-- </geo:Point> -->

<!-- Assertions based on experimental version of Darwin Core -->
<dwc:SampleID>http://data.rbge.org.uk/herb/E00435912</dwc:SampleID>
<dc:modified>2011-08-19 00:00:00</dc:modified>
<dwc:BasisOfRecord>Specimen</dwc:BasisOfRecord>
<dwc:InstitutionCode>http://biocol.org/urn:lsid:biocol.org:col:15670</dwc:InstitutionCode>
<dwc:CollectionCode>E</dwc:CollectionCode>
<dwc:CatalogNumber>E00435912</dwc:CatalogNumber>
<dwc:ScientificName>Duboscia macrocarpa Bocq.</dwc:ScientificName>
<dwc:Family>Malvaceae</dwc:Family>
<dwc:Genus>Duboscia</dwc:Genus>
<dwc:SpecificEpithet>macrocarpa</dwc:SpecificEpithet>
<dwc:HigherGeography>Tropical Africa</dwc:HigherGeography>
<dwc:Country>CF</dwc:Country>
<dwc:StateProvince>Sangha-Mbaere</dwc:StateProvince>
<dwc:Locality>Bai Hoku.</dwc:Locality>
<dwc:DecimalLongitude>16.466667</dwc:DecimalLongitude>
<dwc:DecimalLatitude>2.866667</dwc:DecimalLatitude>
<dwc:EarliestDateCollected>1973</dwc:EarliestDateCollected>
<dwc:Collector>Goldsmith, M.</dwc:Collector>
<dc:relation><rdf:Description rdf:about="http://data.rbge.org.uk/images/393342" ><dc:identifier rdf:resource="http://data.rbge.org.uk/images/393342" /><dc:type rdf:resource="http://purl.org/dc/dcmitype/Image" /><dc:subject rdf:resource="http://data.rbge.org.uk/herb/E00435912" /><dc:format>image/jpeg</dc:format><dc:description xml:lang="en">Image of herbarium specimen</dc:description><dc:created>2011-08-22T11:38:48Z</dc:created></rdf:Description></dc:relation>
</rdf:Description>

</rdf:RDF> 
```

RDF/Turtle:
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix xsi: <http://www.w3.org/2001/XMLSchema-instance>.
@prefix tap: <http://rs.tdwg.org/tapir/1.0>.
@prefix xs: <http://www.w3.org/2001/XMLSchema>.
@prefix hyam: <http://hyam.net/tapir2sw#>.
@prefix dwc: <http://rs.tdwg.org/dwc/terms/>.
@prefix dwcc: <http://rs.tdwg.org/dwc/curatorial/>.
@prefix dc: <http://purl.org/dc/terms/>.
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>.

<http://data.rbge.org.uk/herb/E00435912> 
	dc:created "1973";
	dc:creator "Goldsmith, M.";
	dc:description "A herbarium specimen of Duboscia macrocarpa Bocq. collected by Goldsmith, M. #207 ";
	dc:modified "2011-08-19 00:00:00";
	dc:relation <http://data.rbge.org.uk/images/393342>;
	dc:title "Goldsmith, M. #207 Duboscia macrocarpa Bocq.";
	dwc:BasisOfRecord "Specimen";
	dwc:CatalogNumber "E00435912";
	dwc:CollectionCode "E";
	dwc:Collector "Goldsmith, M.";
	dwc:Country "CF";
	dwc:DecimalLatitude "2.866667";
	dwc:DecimalLongitude "16.466667";
	dwc:EarliestDateCollected "1973";
	dwc:Family "Malvaceae";
	dwc:Genus "Duboscia";
	dwc:HigherGeography "Tropical Africa";
	dwc:InstitutionCode "http://biocol.org/urn:lsid:biocol.org:col:15670";
	dwc:Locality "Bai Hoku.";
	dwc:SampleID "http://data.rbge.org.uk/herb/E00435912";
	dwc:ScientificName "Duboscia macrocarpa Bocq.";
	dwc:SpecificEpithet "macrocarpa";
	dwc:StateProvince "Sangha-Mbaere";
	geo:lat "2.866667";
	geo:long "16.466667".
<http://data.rbge.org.uk/images/393342> 
	dc:created "2011-08-22T11:38:48Z";
	dc:description "Image of herbarium specimen"@en;
	dc:format "image/jpeg";
	dc:identifier <http://data.rbge.org.uk/images/393342>;
	dc:subject <http://data.rbge.org.uk/herb/E00435912>;
	dc:type <http://purl.org/dc/dcmitype/Image>.
<http://data.rbge.org.uk/service/rdf/herb.php?guid=http://data.rbge.org.uk/herb/E00435912> 
	dc:created "2013-11-10T01:46:58+00:00";
	dc:creator "Simple PHP RDF Script";
	dc:hasVersion <http://elmer.rbge.org.uk/bgbase/vherb/bgbasevherb.php?cfg=bgbase/vherb/fulldetails.cfg%26amp;specimens_specimen__num=E00435912>.
```
Note: this RDF uses a bit of fanciful Darwin Core (incorrect case, dwc:Collector, etc.)

### Specimens in ARCTOS/University of Alaska Museum of the North ###

HTTP URIs for specimens such as http://arctos.database.museum/guid/UAM:Ento:230092 which is the same for all specimens in the ARCTOS system.  However, UA Museum of the North also uses DOIs such as http://dx.doi.org/10.7299/X7VQ32SJ which redirect in a browser to the same web page as the ARCTOS HTTP URI.

Dereferencing the DOI requesting RDF/XML gets:
```
<rdf:RDF
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:owl="http://www.w3.org/2002/07/owl#"
xmlns:j.0="http://purl.org/dc/terms/" >
<rdf:Description rdf:about="http://dx.doi.org/10.7299/X7VQ32SJ">
<j.0:creator>Derek S. Sikes</j.0:creator>
<j.0:publisher>University of Alaska Museum</j.0:publisher>
<j.0:title>UAM:Ento:230092 - Grylloblatta campodeiformis</j.0:title>
<j.0:date>2004</j.0:date>
<owl:sameAs>doi:10.7299/X7VQ32SJ</owl:sameAs>
<owl:sameAs>info:doi/10.7299/X7VQ32SJ</owl:sameAs>
<j.0:identifier>10.7299/X7VQ32SJ</j.0:identifier>
</rdf:Description>
</rdf:RDF>
```

In RDF/Turtle:
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix owl: <http://www.w3.org/2002/07/owl#>.

<http://dx.doi.org/10.7299/X7VQ32SJ> 
	<http://purl.org/dc/terms/creator> "Derek S. Sikes";
	<http://purl.org/dc/terms/date> "2004";
	<http://purl.org/dc/terms/identifier> "10.7299/X7VQ32SJ";
	<http://purl.org/dc/terms/publisher> "University of Alaska Museum";
	<http://purl.org/dc/terms/title> "UAM:Ento:230092 - Grylloblatta campodeiformis";
	owl:sameAs "doi:10.7299/X7VQ32SJ",
	        "info:doi/10.7299/X7VQ32SJ".
```

Dereferencing the HTTP URI requesting RDF/XML gets this file (which has some validation problems):
```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:tap="http://rs.tdwg.org/tapir/1.0"
xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:hyam="http://hyam.net/tapir2sw#"
xmlns:dwc="http://rs.tdwg.org/dwc/terms/" xmlns:dwcc="http://rs.tdwg.org/dwc/curatorial/"
xmlns:dc="http://purl.org/dc/terms/"
xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#">
<!--
So, we pretty much just made this all up. It's a
nifty way to test out content negotiation, but we have no idea
if the RDF is actually useful to anyone.
If you have actual use for rdf, and would like us to do something different,
just drop up an email (you probably know who we are, right?) or fill
out the contact form at http://arctos.database.museum/contact.cfm
We'd love to hear your feedback. Or just tell us you found this thing.

This document in no way represents all information available from Arctos.
-->
<rdf:Description rdf:about="http://arctos.database.museum/guid/UAM:Ento:230092">
<dc:creator>Sayde Ridling</dc:creator>
<dc:created>2012-11-29</dc:created>
<dc:hasVersion rdf:resource="http://arctos.database.museum/guid/UAM:Ento:230092" />
</rdf:Description>
<!-- This is metadata about this specimen -->
<rdf:Description rdf:about="http://arctos.database.museum/guid/UAM:Ento:230092">
<dc:title>UAM:Ento:230092 - UAM Insects 230092 Grylloblatta campodeiformis</dc:title>
<dc:description>UAM Insects 230092 Grylloblatta campodeiformis</dc:description>
<geo:Point>
<geo:lat>50.8657666667</geo:lat>
<geo:long>-115.2110333333</geo:long>
</geo:Point>
<!-- Assertions based on experimental version of Darwin Core -->
<dc:modified>2013-09-18</dc:modified>
<dwc:SampleID>http://arctos.database.museum/guid/UAM:Ento:230092</dwc:SampleID>
<dwc:BasisOfRecord>PreservedSpecimen</dwc:BasisOfRecord>
<dwc:InstitutionCode>UAM</dwc:InstitutionCode>
<dwc:CollectionCode>Ento</dwc:CollectionCode>
<dwc:CatalogNumber>230092</dwc:CatalogNumber>
<dwc:ScientificName>Grylloblatta campodeiformis</dwc:ScientificName>
<dwc:HigherTaxon>Animalia Arthropoda Insecta Gryllablattodea Grylloblattidae Grylloblatta campodeiformis Walker 1914</dwc:HigherTaxon>
<dwc:Kingdom></dwc:Kingdom>
<dwc:Phylum>Arthropoda</dwc:Phylum>
<dwc:Class>Insecta</dwc:Class>
<dwc:Order>Gryllablattodea</dwc:Order>
<dwc:Family>Grylloblattidae</dwc:Family>
<dwc:Genus>Grylloblatta</dwc:Genus>
<dwc:Species>Grylloblatta campodeiformis</dwc:Species>
<dwc:Subspecies></dwc:Subspecies>
<dwc:IdentifiedBy>Karl J. Jarvis</dwc:IdentifiedBy>
<dwc:HigherGeography>North America, Canada, Alberta</dwc:HigherGeography>
<dwc:ContinentOcean>North America</dwc:ContinentOcean>
<dwc:Country>Canada</dwc:Country>
<dwc:StateProvince>Alberta</dwc:StateProvince>
<dwc:IslandGroup></dwc:IslandGroup>
<dwc:Island></dwc:Island>
<dwc:County></dwc:County>
<dwc:Locality>Kananaskis. Galatca, trail to Lilian Lake N of Rt. 40 S of Kananaskis Village</dwc:Locality>
<dwc:DecimalLongitude>50.8657666667</dwc:DecimalLongitude>
<dwc:DecimalLatitude>-115.2110333333</dwc:DecimalLatitude>
<dwc:HorizontalDatum>World Geodetic System 1984</dwc:HorizontalDatum>
<dwc:OriginalCoordinateSystem>degrees dec. minutes</dwc:OriginalCoordinateSystem>
<dwc:VerbatimCoordinates>50d 51.946m N/115d 12.662m W</dwc:VerbatimCoordinates>
<dwc:GeoreferenceSource>Field GPS Unit</dwc:GeoreferenceSource>
<dwc:GeoreferenceProtocol>MaNIS georeferencing guidelines</dwc:GeoreferenceProtocol>
<dwc:CoordinateUncertaintyInMeters>10</dwc:CoordinateUncertaintyInMeters>
<dwc:MinimumElevationInMeters>1761.744</dwc:MinimumElevationInMeters>
<dwc:MaximumElevationInMeters>1798.32</dwc:MaximumElevationInMeters>
<dwc:VerbatimElevation>5780-5900 ft</dwc:VerbatimElevation>
<dwc:MinimumDepthInMeters></dwc:MinimumDepthInMeters>
<dwc:MaximumDepthInMeters></dwc:MaximumDepthInMeters>
<dwc:TypeStatus>voucher of <a href="http://arctos.database.museum/name/Grylloblatta campodeiformis"><i>Grylloblatta campodeiformis</i> Walker 1914</a>, page 227 in <a href="http://arctos.database.museum/publication/10006536">Jarvis %26amp; Whiting 2006</a></dwc:TypeStatus>
<dwc:Sex>female </dwc:Sex>
<dwc:Preparations>vial (100% ethanol) whole organism</dwc:Preparations>
<dwc:IndividualCount>1</dwc:IndividualCount>
<dwc:AgeClass>adult </dwc:AgeClass>
<dwc:OtherCatalogNumbers>GenBank=DQ457228; GenBank=DQ457263; GenBank=DQ457300; secondary identifier=BYU_gb32.1</dwc:OtherCatalogNumbers>
<dwc:GenBankNum>http://www.ncbi.nlm.nih.gov/nuccore/DQ457228; http://www.ncbi.nlm.nih.gov/nuccore/DQ457263; http://www.ncbi.nlm.nih.gov/nuccore/DQ457300</dwc:GenBankNum>
<dwc:RelatedCatalogedItems></dwc:RelatedCatalogedItems>
<dwc:Collector>Derek S. Sikes</dwc:Collector>
<dwc:EarliestDateCollected>2004-10-09</dwc:EarliestDateCollected>
<dwc:LatestDateCollected>2004-10-09</dwc:LatestDateCollected>
<dwc:VerbatimCollectingDate>9 Oct 2004</dwc:VerbatimCollectingDate>
<dwc:Remarks>DNA Holotype GB 32.1 left side mid and hind legs removed for molecular data, hind leg in vial with specimen.</dwc:Remarks>
<dwc:ImageURL>http://arctos.database.museum/MediaSearch.cfm?action=search%26amp;media_id=10322363,10322362</dwc:ImageURL>
</rdf:Description>
</rdf:RDF>
```

In RDF/Turtle (after fixing invalid RDF):
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix xsi: <http://www.w3.org/2001/XMLSchema-instance>.
@prefix tap: <http://rs.tdwg.org/tapir/1.0>.
@prefix xs: <http://www.w3.org/2001/XMLSchema>.
@prefix hyam: <http://hyam.net/tapir2sw#>.
@prefix dwc: <http://rs.tdwg.org/dwc/terms/>.
@prefix dwcc: <http://rs.tdwg.org/dwc/curatorial/>.
@prefix dc: <http://purl.org/dc/terms/>.
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>.

<http://arctos.database.museum/guid/UAM:Ento:230092> 
	dc:created "2012-11-29";
	dc:creator "Sayde Ridling";
	dc:description "UAM Insects 230092 Grylloblatta campodeiformis";
	dc:hasVersion <http://arctos.database.museum/guid/UAM:Ento:230092>;
	dc:modified "2013-09-18";
	dc:title "UAM:Ento:230092 - UAM Insects 230092 Grylloblatta campodeiformis";
	dwc:AgeClass "adult ";
	dwc:BasisOfRecord "PreservedSpecimen";
	dwc:CatalogNumber "230092";
	dwc:Class "Insecta";
	dwc:CollectionCode "Ento";
	dwc:Collector "Derek S. Sikes";
	dwc:ContinentOcean "North America";
	dwc:CoordinateUncertaintyInMeters "10";
	dwc:Country "Canada";
	dwc:County "";
	dwc:DecimalLatitude "-115.2110333333";
	dwc:DecimalLongitude "50.8657666667";
	dwc:EarliestDateCollected "2004-10-09";
	dwc:Family "Grylloblattidae";
	dwc:GenBankNum "http://www.ncbi.nlm.nih.gov/nuccore/DQ457228; http://www.ncbi.nlm.nih.gov/nuccore/DQ457263; http://www.ncbi.nlm.nih.gov/nuccore/DQ457300";
	dwc:Genus "Grylloblatta";
	dwc:GeoreferenceProtocol "MaNIS georeferencing guidelines";
	dwc:GeoreferenceSource "Field GPS Unit";
	dwc:HigherGeography "North America, Canada, Alberta";
	dwc:HigherTaxon "Animalia Arthropoda Insecta Gryllablattodea Grylloblattidae Grylloblatta campodeiformis Walker 1914";
	dwc:HorizontalDatum "World Geodetic System 1984";
	dwc:IdentifiedBy "Karl J. Jarvis";
	dwc:ImageURL "http://arctos.database.museum/MediaSearch.cfm?action=search%26amp;media_id=10322363,10322362";
	dwc:IndividualCount "1";
	dwc:InstitutionCode "UAM";
	dwc:Island "";
	dwc:IslandGroup "";
	dwc:Kingdom "";
	dwc:LatestDateCollected "2004-10-09";
	dwc:Locality "Kananaskis. Galatca, trail to Lilian Lake N of Rt. 40 S of Kananaskis Village";
	dwc:MaximumDepthInMeters "";
	dwc:MaximumElevationInMeters "1798.32";
	dwc:MinimumDepthInMeters "";
	dwc:MinimumElevationInMeters "1761.744";
	dwc:Order "Gryllablattodea";
	dwc:OriginalCoordinateSystem "degrees dec. minutes";
	dwc:OtherCatalogNumbers "GenBank=DQ457228; GenBank=DQ457263; GenBank=DQ457300; secondary identifier=BYU_gb32.1";
	dwc:Phylum "Arthropoda";
	dwc:Preparations "vial (100% ethanol) whole organism";
	dwc:RelatedCatalogedItems "";
	dwc:Remarks "DNA Holotype GB 32.1 left side mid and hind legs removed for molecular data, hind leg in vial with specimen.";
	dwc:SampleID "http://arctos.database.museum/guid/UAM:Ento:230092";
	dwc:ScientificName "Grylloblatta campodeiformis";
	dwc:Sex "female ";
	dwc:Species "Grylloblatta campodeiformis";
	dwc:StateProvince "Alberta";
	dwc:Subspecies "";
	dwc:TypeStatus "voucher of Grylloblatta campodeiformis Walker 1914, page 227 in Jarvis %26amp; Whiting 2006";
	dwc:VerbatimCollectingDate "9 Oct 2004";
	dwc:VerbatimCoordinates "50d 51.946m N/115d 12.662m W";
	dwc:VerbatimElevation "5780-5900 ft";
	geo:lat "50.8657666667";
	geo:long "-115.2110333333".
```
Also contains some non-standard Darwin Core (incorrect case, dwc:Collector, dwc:AgeClass, etc.)

### Specimen in Linked Open Data Of Ecology ###

Example HTTP URI: http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023

Dereferences in a browser showing results of a SPARQL query.  Dereferences as RDF/XML through 303 redirect.

In RDF/XML:
```
<?xml version="1.0"?>
<rdf:RDF
    xmlns:muo="http://purl.oclc.org/NET/muo/muo#"
    xmlns:geospecies="http://rdf.geospecies.org/ont/geospecies#"
    xmlns:fdp="http://ecowlim.tfri.gov.tw/lode/resource/fdp/"
    xmlns:dwc="http://rs.tdwg.org/dwc/terms/"
    xmlns:taif="http://ecowlim.tfri.gov.tw/lode/resource/taif/"
    xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
    xmlns:foaf="http://xmlns.com/foaf/0.1/"
    xmlns:dbp_void="http://dbpedia.org/void/"
    xmlns:taif_lit="http://ecowlim.tfri.gov.tw/lode/resource/lit/taif/"
    xmlns:dc="http://purl.org/dc/terms/"
    xmlns:eco_lit="http://ecowlim.tfri.gov.tw/lode/resource/lit/eco/"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
    xmlns:prv="http://purl.org/net/provenance/ns#"
    xmlns:fdp_lit="http://ecowlim.tfri.gov.tw/lode/resource/lit/fdp/"
    xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#"
    xmlns:dbpprop="http://dbpedia.org/property/"
    xmlns:skos="http://www.w3.org/2004/02/skos/core#"
    xmlns:flyhorse_lit="http://ecowlim.tfri.gov.tw/lode/resource/lit/flyhorse/"
    xmlns:id="http://purl.org/twc/ontologies/identity.owl#"
    xmlns:event="http://purl.org/NET/c4dm/event.owl#"
    xmlns:tl="http://purl.org/NET/c4dm/timeline.owl#"
    xmlns:protons="http://proton.semanticweb.org/2005/04/protons#"
    xmlns:taibnet_lit="http://ecowlim.tfri.gov.tw/lode/resource/lit/taibnet/"
    xmlns:time="http://www.w3.org/2006/time#"
    xmlns:dbpedia="http://dbpedia.org/resource/"
    xmlns:void="http://rdfs.org/ns/void#"
    xmlns:firedb_lit="http://ecowlim.tfri.gov.tw/lode/resource/lit/firedb/"
    xmlns:lode_void="http://ecowlim.tfri.gov.tw/lode/resource/void/"
    xmlns:eco="http://ecowlim.tfri.gov.tw/lode/resource/eco/"
    xmlns:firedb="http://ecowlim.tfri.gov.tw/lode/resource/firedb/"
    xmlns:d2r="http://sites.wiwiss.fu-berlin.de/suhl/bizer/d2r-server/config.rdf#"
    xmlns:scovo="http://purl.org/NET/scovo#"
    xmlns:owl="http://www.w3.org/2002/07/owl#"
    xmlns:ucum_area="http://purl.oclc.org/NET/muo/ucum/unit/area/"
    xmlns:flyhorse="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/"
    xmlns:taibnet="http://ecowlim.tfri.gov.tw/lode/resource/taibnet/"
    xmlns:dbpowl="http://dbpedia.org/ontology/"
    xmlns:ucum_length="http://purl.oclc.org/NET/muo/ucum/unit/length/"
    xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#">
  <rdf:Description rdf:about="http://ecowlim.tfri.gov.tw/lode/data/flyhorse/Specimen/5023?output=xml">
    <rdfs:label>RDF description of Flyhorse DB Insect Specimen #5023</rdfs:label>
    <foaf:primaryTopic>
      <owl:Thing rdf:about="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023">
        <foaf:depiction>http://fact.tfri.gov.tw/smec/TFRI/m_images/00013880.jpg</foaf:depiction>
        <geo:location rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11"/>
        <dwc:identifiedBy xml:lang="en">W. Hwang</dwc:identifiedBy>
        <eco:collectedInEvent>
          <rdf:Description rdf:about="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002">
            <event:product rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023"/>
            <event:hasProduct rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023"/>
          </rdf:Description>
        </eco:collectedInEvent>
        <dwc:identifiedBy xml:lang="zh-tw">黃文伯</dwc:identifiedBy>
        <flyhorse:dateIdentified rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2004-03-19"/>
        <eco:inPreservationTray rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11"/>
        <eco:dateTime rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2004-03-19"/>
        <rdf:type rdf:parseType="Resource">
          <rdfs:seeAlso rdf:resource="http://ecowlim.tfri.gov.tw/lode/pathdata/rdf:type/flyhorse/Specimen/5023"/>
        </rdf:type>
        <rdf:type rdf:resource="http://www.w3.org/2000/01/rdf-schema#Resource"/>
        <dwc:maximumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#float"
        >0</dwc:maximumElevationInMeters>
        <eco:isSampleOfSpecies>
          <rdf:Description rdf:about="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Species/Papilio_bianor_takasago">
            <eco:hasSample rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023"/>
            <flyhorse:hasSample rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023"/>
          </rdf:Description>
        </eco:isSampleOfSpecies>
        <eco:identifiedBy rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/W.Hwang"/>
        <flyhorse:identifiedBy rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/W.Hwang"/>
        <eco:dateTime rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2006-07-11"/>
        <dwc:country xml:lang="en">Taiwan</dwc:country>
        <dwc:recordedBy xml:lang="zh-tw">張玉珍</dwc:recordedBy>
        <eco_lit:dateTime rdf:datatype="http://www.w3.org/2001/XMLSchema#date"
        >1985-07-25</eco_lit:dateTime>
        <flyhorse:inPreservationTray rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11"/>
        <flyhorse:changedDate rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2006-07-11"/>
        <rdfs:label>Flyhorse DB Insect Specimen #5023</rdfs:label>
        <dwc:locality xml:lang="en">Yangmingshan</dwc:locality>
        <dwc:dateIdentified rdf:datatype="http://www.w3.org/2001/XMLSchema#date"
        >2004-03-19</dwc:dateIdentified>
        <flyhorse:recordedBy rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/Y.C.Chang"/>
        <dwc:minimumElevationInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#float"
        >0</dwc:minimumElevationInMeters>
        <eco:recordedBy rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/Y.C.Chang"/>
        <dwc:country xml:lang="zh-tw">中華民國台灣</dwc:country>
        <dwc:recordedBy xml:lang="en">Y. C. Chang</dwc:recordedBy>
        <foaf:based_near rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11"/>
        <event:producedIn rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002"/>
        <flyhorse:isSampleOfSpecies rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Species/Papilio_bianor_takasago"/>
        <eco:dateIdentified rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2004-03-19"/>
        <flyhorse:collectedInEvent rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002"/>
        <eco_lit:dateCollected rdf:datatype="http://www.w3.org/2001/XMLSchema#date"
        >1985-07-25</eco_lit:dateCollected>
        <rdf:type rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/eco/Specimen"/>
        <rdf:type rdf:resource="http://purl.org/NET/c4dm/event.owl#Product"/>
        <dwc:county xml:lang="en">Taipei City</dwc:county>
        <rdf:type rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen"/>
        <dwc:locality xml:lang="zh-tw">陽明山</dwc:locality>
        <rdf:type rdf:resource="http://www.w3.org/2003/01/geo/wgs84_pos#SpatialThing"/>
        <flyhorse_lit:spcmID xml:lang="en">5023</flyhorse_lit:spcmID>
        <dwc:county xml:lang="zh-tw">台北市</dwc:county>
        <event:produced_in rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002"/>
        <flyhorse_lit:dateCollected rdf:datatype="http://www.w3.org/2001/XMLSchema#date"
        >1985-07-25</flyhorse_lit:dateCollected>
        <eco:location rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11"/>
        <flyhorse_lit:localityCode xml:lang="en">TC13</flyhorse_lit:localityCode>
        <flyhorse_lit:countyCode xml:lang="en">TC</flyhorse_lit:countyCode>
        <eco:changedDate rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2006-07-11"/>
      </owl:Thing>
    </foaf:primaryTopic>
  </rdf:Description>
  <rdf:Description rdf:about="http://ecowlim.tfri.gov.tw/lode/resource/void/Dataset">
    <void:exampleResource rdf:resource="http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023"/>
  </rdf:Description>
</rdf:RDF>
```

In RDF/Turtle:
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix muo: <http://purl.oclc.org/NET/muo/muo#>.
@prefix geospecies: <http://rdf.geospecies.org/ont/geospecies#>.
@prefix fdp: <http://ecowlim.tfri.gov.tw/lode/resource/fdp/>.
@prefix dwc: <http://rs.tdwg.org/dwc/terms/>.
@prefix taif: <http://ecowlim.tfri.gov.tw/lode/resource/taif/>.
@prefix foaf: <http://xmlns.com/foaf/0.1/>.
@prefix dbp_void: <http://dbpedia.org/void/>.
@prefix taif_lit: <http://ecowlim.tfri.gov.tw/lode/resource/lit/taif/>.
@prefix dc: <http://purl.org/dc/terms/>.
@prefix eco_lit: <http://ecowlim.tfri.gov.tw/lode/resource/lit/eco/>.
@prefix prv: <http://purl.org/net/provenance/ns#>.
@prefix fdp_lit: <http://ecowlim.tfri.gov.tw/lode/resource/lit/fdp/>.
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>.
@prefix dbpprop: <http://dbpedia.org/property/>.
@prefix skos: <http://www.w3.org/2004/02/skos/core#>.
@prefix flyhorse_lit: <http://ecowlim.tfri.gov.tw/lode/resource/lit/flyhorse/>.
@prefix id: <http://purl.org/twc/ontologies/identity.owl#>.
@prefix event: <http://purl.org/NET/c4dm/event.owl#>.
@prefix tl: <http://purl.org/NET/c4dm/timeline.owl#>.
@prefix protons: <http://proton.semanticweb.org/2005/04/protons#>.
@prefix taibnet_lit: <http://ecowlim.tfri.gov.tw/lode/resource/lit/taibnet/>.
@prefix time: <http://www.w3.org/2006/time#>.
@prefix dbpedia: <http://dbpedia.org/resource/>.
@prefix void: <http://rdfs.org/ns/void#>.
@prefix firedb_lit: <http://ecowlim.tfri.gov.tw/lode/resource/lit/firedb/>.
@prefix lode_void: <http://ecowlim.tfri.gov.tw/lode/resource/void/>.
@prefix eco: <http://ecowlim.tfri.gov.tw/lode/resource/eco/>.
@prefix firedb: <http://ecowlim.tfri.gov.tw/lode/resource/firedb/>.
@prefix d2r: <http://sites.wiwiss.fu-berlin.de/suhl/bizer/d2r-server/config.rdf#>.
@prefix scovo: <http://purl.org/NET/scovo#>.
@prefix owl: <http://www.w3.org/2002/07/owl#>.
@prefix ucum_area: <http://purl.oclc.org/NET/muo/ucum/unit/area/>.
@prefix flyhorse: <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/>.
@prefix taibnet: <http://ecowlim.tfri.gov.tw/lode/resource/taibnet/>.
@prefix dbpowl: <http://dbpedia.org/ontology/>.
@prefix ucum_length: <http://purl.oclc.org/NET/muo/ucum/unit/length/>.

<http://ecowlim.tfri.gov.tw/lode/data/flyhorse/Specimen/5023?output=xml> 
	rdfs:label "RDF description of Flyhorse DB Insect Specimen #5023";
	foaf:primaryTopic <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023>.
<http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002> 
	event:hasProduct <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023>;
	event:product <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023>.
<http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Species/Papilio_bianor_takasago> 
	eco:hasSample <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023>;
	flyhorse:hasSample <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023>.
<http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023> 
	eco:changedDate <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2006-07-11>;
	eco:collectedInEvent <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002>;
	eco:dateIdentified <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2004-03-19>;
	eco:dateTime <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2004-03-19>,
	           <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2006-07-11>;
	eco:identifiedBy <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/W.Hwang>;
	eco:inPreservationTray <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11>;
	eco:isSampleOfSpecies <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Species/Papilio_bianor_takasago>;
	eco:location <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11>;
	eco:recordedBy <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/Y.C.Chang>;
	flyhorse:changedDate <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2006-07-11>;
	flyhorse:collectedInEvent <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002>;
	flyhorse:dateIdentified <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Date/2004-03-19>;
	flyhorse:identifiedBy <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/W.Hwang>;
	flyhorse:inPreservationTray <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11>;
	flyhorse:isSampleOfSpecies <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Species/Papilio_bianor_takasago>;
	flyhorse:recordedBy <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Person/Y.C.Chang>;
	eco_lit:dateCollected "1985-07-25"^^xsd:date;
	eco_lit:dateTime "1985-07-25"^^xsd:date;
	flyhorse_lit:countyCode "TC"@en;
	flyhorse_lit:dateCollected "1985-07-25"^^xsd:date;
	flyhorse_lit:localityCode "TC13"@en;
	flyhorse_lit:spcmID "5023"@en;
	event:producedIn <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002>;
	event:produced_in <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/CollectingEvent/1002>;
	dwc:country "Taiwan"@en,
	          "中華民國台灣"@zh-tw;
	dwc:county "Taipei City"@en,
	         "台北市"@zh-tw;
	dwc:dateIdentified "2004-03-19"^^xsd:date;
	dwc:identifiedBy "W. Hwang"@en,
	               "黃文伯"@zh-tw;
	dwc:locality "Yangmingshan"@en,
	           "陽明山"@zh-tw;
	dwc:maximumElevationInMeters "0"^^xsd:float;
	dwc:minimumElevationInMeters "0"^^xsd:float;
	dwc:recordedBy "Y. C. Chang"@en,
	             "張玉珍"@zh-tw;
	a [rdfs:seeAlso <http://ecowlim.tfri.gov.tw/lode/pathdata/rdf:type/flyhorse/Specimen/5023>],
	eco:Specimen,
	flyhorse:Specimen,
	event:Product,
	rdfs:Resource,
	owl:Thing,
	geo:SpatialThing;
	rdfs:label "Flyhorse DB Insect Specimen #5023";
	geo:location <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11>;
	foaf:based_near <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Prestray/33L1-11>;
	foaf:depiction "http://fact.tfri.gov.tw/smec/TFRI/m_images/00013880.jpg".
lode_void:Dataset void:exampleResource <http://ecowlim.tfri.gov.tw/lode/resource/flyhorse/Specimen/5023>.
```