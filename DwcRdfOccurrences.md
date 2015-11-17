![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Examples of Darwin Core occurrences in RDF #

**Date:** (Created) 2013-09-04; (Last modified) 2013-09-04

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/standards/147/) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Joel Sachs](mailto:jsachs@csee.umbc.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

an occurrence:
```
<?xml version="1.0" encoding="UTF-8"?>
    
<rdf:RDF
xmlns:rdf = "http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dwc="http://rs.tdwg.org/dwc/terms/#"
xmlns:bb="http://www.cs.umbc.edu/~jsachs/"
xmlns:ethan="http://spire.umbc.edu/ethan/">

<dwc:Occurrence rdf:about="http://www.cs.umbc.edu/~jsachs/occurrences/tdwg2010bioblitz_1835">


<dwc:occurrenceID>
http://www.cs.umbc.edu/~jsachs/occurrences/tdwg2010bioblitz_1835
</dwc:occurrenceID>


<dwc:Identification>
<rdf:Description rdf:about="http://www.cs.umbc.edu/~jsachs/identifications/tdwg2010bioblitz_1835_id_1">

<dwc:scientificName>
Myrmica rubra
</dwc:scientificName>

<dwc:vernacularName>
scale insects
</dwc:vernacularName>

<dwc:taxonConceptID>
urn:lsid:catalogueoflife.org:taxon:e295f666-29c1-102b-9a4a-00304854f820:ac2010
</dwc:taxonConceptID>

<dwc:taxonConceptID rdf:resource="http://spire.umbc.edu/ethan/Myrmica_rubra"/>

<dwc:kingdom>
Animalia
</dwc:kingdom>

<dwc:phylum>
Arthropoda
</dwc:phylum>

<dwc:class>
Insecta
</dwc:class>

<dwc:order>
Hymenoptera
</dwc:order>

</rdf:Description>

</dwc:Identification>

<dwc:eventDate>
29/09/10
</dwc:eventDate>

<dwc:eventTime>
10:29
</dwc:eventTime>

<dwc:occurrenceRemarks rdf:parseType='Literal'>
European fire ants tend brown scale insects.
</dwc:occurrenceRemarks>

<dwc:associatedMedia>
http://farm5.static.flickr.com/4088/5037532695_7261b48ee2_b.jpg
</dwc:associatedMedia>

<dwc:associatedMedia>
http://zoom.it/dozQ
</dwc:associatedMedia>

<dwc:recordedBy>
Elizabeth Sellers
</dwc:recordedBy>

<bb:recording_app>
flickr_technobioblitz_group
</bb:recording_app>

</dwc:Occurrence>
</rdf:RDF>
```

an identification:
```
<?xml version="1.0" encoding="UTF-8"?>
    
<rdf:RDF
xmlns:rdf = "http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dwc="http://rs.tdwg.org/dwc/terms/#"
xmlns:bb="http://www.cs.umbc.edu/~jsachs/"
xmlns:ethan="http://spire.umbc.edu/ethan/">

<dwc:Identification rdf:about="http://www.cs.umbc.edu/~jsachs/identifications/tdwg2010bioblitz_1835_id_1"><dwc:occurrenceID>
http://www.cs.umbc.edu/~jsachs/occurrences/tdwg2010bioblitz_1835
</dwc:occurrenceID>



<dwc:scientificName>
Myrmica rubra
</dwc:scientificName>

<dwc:vernacularName>
scale insects
</dwc:vernacularName>

<dwc:taxonConceptID>
urn:lsid:catalogueoflife.org:taxon:e295f666-29c1-102b-9a4a-00304854f820:ac2010
</dwc:taxonConceptID>

<dwc:taxonConceptID rdf:resource="http://spire.umbc.edu/ethan/Myrmica_rubra"/>

<dwc:kingdom>
Animalia
</dwc:kingdom>

<dwc:phylum>
Arthropoda
</dwc:phylum>

<dwc:class>
Insecta
</dwc:class>

<dwc:order>
Hymenoptera
</dwc:order>

</dwc:Identification>
</rdf:RDF>
```