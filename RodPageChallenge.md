# Rod Page's Challenge #

Rod posted a [challenge](http://lists.tdwg.org/pipermail/tdwg-tag/2011-September/002381.html) to the community, which he developed [further](http://iphylo.blogspot.com/2011/10/tdwg-challenge-what-is-rdf-good-for.html) before the 2011 TDWG meeting.  He offered a set of RDF-ized data on frogs.  These data are now loaded into at least two triplestores ([here](http://tdwg-rdf.phylodiversity.net/store2/) and [here](http://82.96.149.133:8890/sparql)).

As a first prize, Rod offered to announce in his [blog](http://iphylo.blogspot.com) that the challenge entry sucked.  And for a second prize, he'd say the entry sucked more!

## Linking data ##

As an example of linking up the different datasets, but not making new inferences, here's a question: **Find all the species in the genus _Bufo_ which have long/lats in Genbank, and optionally get their conservations status from Wikipedia**. Try the SPARQL query for yourself in the http://tdwg-rdf.phylodiversity.net/store2/ triplestore:

```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX uni: <http://purl.uniprot.org/core/> 
PREFIX dcterms: <http://purl.org/dc/terms/> 
PREFIX dbp: <http://dbpedia.org/ontology/> 
PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> 

CONSTRUCT {
  ?gb dcterms:subject ?sp .
  ?sp uni:scientificName ?sn .
  ?sp rdfs:seeAlso ?dbp .
  ?dbp dbp:conservationStatus ?cons .
  ?gb dcterms:relation _:occ .
  _:occ geo:long ?long .
  _:occ geo:lat ?lat .
}
WHERE {
  # Where name is Bufo and rank is genus
  ?gen uni:scientificName "Bufo" .
  ?gen uni:rank uni:Genus .
  # go down two subclasses, check it's a species
  ?sect rdfs:subClassOf ?gen .
  ?sp rdfs:subClassOf ?sect .
  ?sp uni:rank uni:Species .
  ?sp uni:scientificName ?sn .
  # link to genbank and find those with occurrences
  ?gb dcterms:subject ?sp .
  ?gb dcterms:relation [
     geo:long ?long ;
     geo:lat ?lat ] .
  # optionally, link to DBpedia and get the conservation status
  OPTIONAL {
    ?sp rdfs:seeAlso ?dbp .
    ?dbp dbp:conservationStatus ?cons . }
}	  
```

This gives results for 254 occurrences of the form (here serialized in turtle):
```
<http://bio2rdf.org/genbank:HM770001>
    dcterms:relation [
        geo:lat "14.83" ;
        geo:long "-24.73"
    ] ;
    dcterms:subject <http://purl.uniprot.org/taxonomy/8390> .

<http://purl.uniprot.org/taxonomy/8390>
    uni:scientificName "Amietophrynus regularis" ;
    rdfs:seeAlso <http://dbpedia.org/resource/Amietophrynus_regularis> .

<http://dbpedia.org/resource/Amietophrynus_regularis>
    dbp:conservationStatus "LC"@en .
```

## Basic inference ##

With the 4sr reasoner for 4store, reasoning over rdfs concepts is possible.  Try this query:

```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX uni: <http://purl.uniprot.org/core/>

SELECT ?n WHERE {
  ?s uni:scientificName ?n .
  ?s rdfs:subClassOf <http://purl.uniprot.org/taxonomy/651673> .
}
```

in a [tdwg test triplestore](http://tdwg-rdf.phylodiversity.net/store2/), both with and without inference.

## Appendix: Data provided by Rod ##

Below are snippets (in turtle) of the data objects provided:

### General info: Wikipedia/DBpedia (dbpedia.rdf) ###

**Note** Rod's original file had a error: a `</rdf:RDF>` at line 7502.  The fixed file is at http://tdwd-rdf.net/static/rdmpage/dbpedia.rdf.

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix dbpedia-owl: <http://dbpedia.org/ontology/> .
@prefix dbpprop: <http://dbpedia.org/property/> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .
@prefix grs: <http://www.georss.org/georss/> .

<http://dbpedia.org/resource/Acanthixalus_spinosus>
    dbpedia-owl:abstract "Acanthixalus spinosus es una especie de anfibios de la familia Hyperoliidae. Habita en Camerún, República del Congo, República Democrática del Congo, Gabón, Nigeria y, posiblemente Angola, República Centroafricana y Guinea Ecuatorial. Su hábitat natural incluye bosques tropicales o subtropicales secos y a baja altitud y zonas previamente boscosas ahora degradadas. Está amenazada de extinción por la pérdida de su hábitat natural."@es, "Acanthixalus spinosus est une espèce d'amphibien de la famille des Hyperoliidae."@fr, "Acanthixalus spinosus is a species of frog in the Hyperoliidae family. It is found in Cameroon, Republic of the Congo, Democratic Republic of the Congo, Gabon, Nigeria, possibly Angola, possibly Central African Republic, and possibly Equatorial Guinea. Its natural habitats are subtropical or tropical moist lowland forests and heavily degraded former forest. It is threatened by habitat loss."@en ;
    dbpedia-owl:class <http://dbpedia.org/resource/Amphibian> ;
    dbpedia-owl:conservationStatus "LC"@en ;
    dbpedia-owl:conservationStatusSystem "IUCN3.1"@en ;
    dbpedia-owl:family <http://dbpedia.org/resource/Hyperoliidae> ;
    dbpedia-owl:genus <http://dbpedia.org/resource/Acanthixalus> ;
    dbpedia-owl:kingdom <http://dbpedia.org/resource/Animal> ;
    dbpedia-owl:order <http://dbpedia.org/resource/Frog> ;
    dbpedia-owl:phylum <http://dbpedia.org/resource/Chordate> ;
    dbpprop:binomial "Acanthixalus spinosus"@en ;
    dbpprop:classis <http://dbpedia.org/resource/Amphibian> ;
    dbpprop:familia <http://dbpedia.org/resource/Hyperoliidae> ;
    dbpprop:genus "Acanthixalus"@en ;
    dbpprop:name "Acanthixalus spinosus"@en ;
    dbpprop:ordo <http://dbpedia.org/resource/Frog> ;
    dbpprop:phylum <http://dbpedia.org/resource/Chordate> ;
    dbpprop:regnum <http://dbpedia.org/resource/Animal> ;
    dbpprop:species "A. spinosus"@en ;
    dbpprop:status "LC"@en ;
    dbpprop:statusSystem "IUCN3.1"@en ;
    dbpprop:wikiPageUsesTemplate <http://dbpedia.org/resource/Template:Taxobox> ;
    dcterms:subject <http://dbpedia.org/resource/Category:Acanthixalus> ;
    a dbpedia-owl:Amphibian, dbpedia-owl:Animal, dbpedia-owl:Eukaryote, dbpedia-owl:Species, <http://umbel.org/umbel/rc/Amphibian>, owl:Thing ;
    rdfs:comment "Acanthixalus spinosus es una especie de anfibios de la familia Hyperoliidae. Habita en Camerún, República del Congo, República Democrática del Congo, Gabón, Nigeria y, posiblemente Angola, República Centroafricana y Guinea Ecuatorial. Su hábitat natural incluye bosques tropicales o subtropicales secos y a baja altitud y zonas previamente boscosas ahora degradadas. Está amenazada de extinción por la pérdida de su hábitat natural."@es, "Acanthixalus spinosus est une espèce d'amphibien de la famille des Hyperoliidae."@fr, "Acanthixalus spinosus is a species of frog in the Hyperoliidae family. It is found in Cameroon, Republic of the Congo, Democratic Republic of the Congo, Gabon, Nigeria, possibly Angola, possibly Central African Republic, and possibly Equatorial Guinea. Its natural habitats are subtropical or tropical moist lowland forests and heavily degraded former forest. It is threatened by habitat loss."@en ;
    rdfs:label "Acanthixalus spinosus"@en, "Acanthixalus spinosus"@es, "Acanthixalus spinosus"@fr ;
    owl:sameAs <http://dbpedia.org/resource/Acanthixalus_spinosus>, <http://rdf.freebase.com/ns/m/02w2206> ;
    foaf:name "Acanthixalus spinosus"@en ;
    foaf:page <http://en.wikipedia.org/wiki/Acanthixalus_spinosus> .

<http://www4.wiwiss.fu-berlin.de/flickrwrappr/photos/Acanthixalus>
    owl:sameAs <http://dbpedia.org/resource/Acanthixalus> .

<http://en.wikipedia.org/wiki/Acanthixalus>
    foaf:primaryTopic <http://dbpedia.org/resource/Acanthixalus> .

<http://www4.wiwiss.fu-berlin.de/flickrwrappr/photos/Acanthixalus_spinosus>
    owl:sameAs <http://dbpedia.org/resource/Acanthixalus_spinosus> .

<http://en.wikipedia.org/wiki/Acanthixalus_spinosus>
    foaf:primaryTopic <http://dbpedia.org/resource/Acanthixalus_spinosus> .
```

### Occurrences: Genbank (genbank.rdf) ###

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .
@prefix tcommon: <http://rs.tdwg.org/ontology/voc/Common#> .
@prefix toccurrence: <http://rs.tdwg.org/ontology/voc/TaxonOccurrence#> .
@prefix uniprot: <http://purl.uniprot.org/core/> .

<http://bio2rdf.org/genbank:EU566842>
    dcterms:created "2008-07-06" ;
    dcterms:description "Xenopus borealis voucher MHNG:Herp:2644.64 cytochrome oxidase subunit I (COI) gene, partial cds; mitochondrial." ;
    dcterms:modified "2010-12-23" ;
    dcterms:relation [
        dcterms:identifier "MHNG:Herp:2644.64" ;
        toccurrence:country "Kenya" ;
        toccurrence:decimalLatitude "0.66" ;
        toccurrence:decimalLongitude "37.5" ;
        toccurrence:identifiedToString "Xenopus borealis" ;
        toccurrence:verbatimCoordinates "0.66 N 37.5 E" ;
        a toccurrence:TaxonOccurrence ;
        geo:lat "0.66" ;
        geo:long "37.5"
    ] ;
    dcterms:subject <http://purl.uniprot.org/taxonomy/8354> ;
    dcterms:title "EU566842" ;
    a uniprot:Molecule .
```


### Names: Index of organism names (ion.rdf) ###

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix tdwg_pc: <http://rs.tdwg.org/ontology/voc/PublicationCitation#> .
@prefix tdwg_co: <http://rs.tdwg.org/ontology/voc/Common#> .
@prefix tdwg_tn: <http://rs.tdwg.org/ontology/voc/TaxonName#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:lsid:organismnames.com:name:3152799>
    dc:Title "Xenopus laevis borealis" ;
    dc:creator <http://www.organismnames.com> ;
    dc:identifier "urn:lsid:organismnames.com:name:3152799" ;
    tdwg_co:PublishedIn "Reptiles and Amphibians collected by the Lake Rudolf Rift Valley Expedition, 1934. Annals & Magazine of Natural History Series 10, 18 1936: pp. 594-609.   [Zoological Record Volume 73]" ;
    tdwg_co:microreference "" ;
    tdwg_tn:nameComplete "Xenopus laevis borealis" ;
    tdwg_tn:nomenclaturalCode tdwg_tn:ICZN ;
    a tdwg_tn:TaxonName ;
    rdfs:seeAlso <http://www.organismnames.com/namedetails.htm?lsid=3152799> .
```


### Taxonomy hierarchy: Uniprot taxonomy (uniprot.rdf) ###

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix : <http://purl.uniprot.org/core/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix bibo: <http://purl.org/ontology/bibo/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

<file:///home/cam/Desktop/rdf/uniprot.rdf>
    a owl:Ontology ;
    owl:imports <http://purl.uniprot.org/core/> .

<http://purl.uniprot.org/taxonomy/1001626>
    :otherName "Bufo shaartusiensis Pisanets, Mezhzherin, and Shcherbak, 1996", "Bufo viridis shaartusiensis" ;
    :partOfLineage false ;
    :rank :Species ;
    :scientificName "Bufo shaartusiensis" ;
    a :Taxon ;
    rdfs:subClassOf <http://purl.uniprot.org/taxonomy/651673> .
```

### Literature: Crossref (crossref.rdf) ###

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix ns0: <http://purl.org/dc/terms/> .

<http://dx.doi.org/10.1111/j.1096-3642.1988.tb00880.x>
    <http://prismstandard.org/namespaces/basic/2.1/doi> "10.1111/j.1096-3642.1988.tb00880.x" ;
    <http://prismstandard.org/namespaces/basic/2.1/endingPage> "38" ;
    <http://prismstandard.org/namespaces/basic/2.1/startingPage> "1" ;
    <http://prismstandard.org/namespaces/basic/2.1/volume> "94" ;
    ns0:creator <http://id.crossref.org/contributor/david-c-cannatella-1zt56awxdhgrh>, <http://id.crossref.org/contributor/linda-trueb-1zt56awxdhgrh> ;
    ns0:date "1988-09-15Z"^^<http://www.w3.org/2001/XMLSchema#date> ;
    ns0:identifier "10.1111/j.1096-3642.1988.tb00880.x" ;
    ns0:isPartOf <http://id.crossref.org/issn/0024-4082> ;
    ns0:title "Evolution of pipoid frogs: intergeneric relationships of the aquatic frog family Pipidae (Anura)" ;
    <http://purl.org/ontology/bibo/doi> "10.1111/j.1096-3642.1988.tb00880.x" ;
    <http://purl.org/ontology/bibo/pageEnd> "38" ;
    <http://purl.org/ontology/bibo/pageStart> "1" ;
    <http://purl.org/ontology/bibo/volume> "94" ;
    a <http://purl.org/ontology/bibo/Article> ;
    <http://www.w3.org/2002/07/owl#sameAs> <doi:10.1111/j.1096-3642.1988.tb00880.x>, <info:doi/10.1111/j.1096-3642.1988.tb00880.x> .

<http://id.crossref.org/issn/0024-4082>
    <http://prismstandard.org/namespaces/basic/2.1/eIssn> "1096-3642" ;
    <http://prismstandard.org/namespaces/basic/2.1/issn> "0024-4082" ;
    ns0:hasPart <http://dx.doi.org/10.1111/j.1096-3642.1988.tb00880.x>, <http://dx.doi.org/10.1111/j.1096-3642.1995.tb01427.x>, <http://dx.doi.org/10.1111/j.1096-3642.2006.00223.x>, <http://dx.doi.org/10.1111/j.1096-3642.2008.00397.x>, <http://dx.doi.org/10.1111/j.1096-3642.2008.00424.x>, <http://dx.doi.org/10.1111/j.1096-3642.2008.00440.x>, <http://dx.doi.org/10.1111/j.1096-3642.2008.00466.x>, <http://dx.doi.org/10.1111/j.1096-3642.2009.00579.x>, <http://dx.doi.org/10.1111/j.1096-3642.2010.00641.x>, <http://dx.doi.org/10.1111/j.1096-3642.2010.00652.x> ;
    ns0:identifier "0024-4082" ;
    ns0:title "Zoological Journal of the Linnean Society" ;
    <http://purl.org/ontology/bibo/eissn> "1096-3642" ;
    <http://purl.org/ontology/bibo/issn> "0024-4082" ;
    a <http://purl.org/ontology/bibo/Journal> ;
    <http://www.w3.org/2002/07/owl#sameAs> <urn:issn:0024-4082> .

<http://id.crossref.org/contributor/david-c-cannatella-1zt56awxdhgrh>
    a <http://xmlns.com/foaf/0.1/Person> ;
    <http://xmlns.com/foaf/0.1/familyName> "CANNATELLA" ;
    <http://xmlns.com/foaf/0.1/givenName> "DAVID C." ;
    <http://xmlns.com/foaf/0.1/name> "DAVID C. CANNATELLA" .
```


### Glue: ION x DOI (ion\_doi.rdf) ###

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix tdwg_pc: <http://rs.tdwg.org/ontology/voc/PublicationCitation#> .
@prefix tdwg_co: <http://rs.tdwg.org/ontology/voc/Common#> .
@prefix tdwg_tn: <http://rs.tdwg.org/ontology/voc/TaxonName#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:lsid:organismnames.com:name:701301>
    tdwg_co:publishedInCitation <http://dx.doi.org/10.1111/j.1096-3642.1988.tb00880.x> ;
    a tdwg_tn:TaxonName .
```

### Glue: Uniprot x Wikipedia (linkout.rdf) ###

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<http://purl.uniprot.org/taxonomy/888540>
    rdfs:seeAlso <http://dbpedia.org/resource/Telmatobius_yuracare> .
```