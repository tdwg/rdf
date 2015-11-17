# RDF representation of a tc:TaxonConcept instance and its associated reference #
This example uses terms from the TDWG TaxonConcept and TaxonName ontologies as well as other well-known vocabularies.  There are other properties included in the TaxonConcept ontology that could be used but are not shown here in order to focus on the predicates used to relate the major defining components of the taxon graph.

## Graphical representation ##

<img src='http://tdwg-rdf.googlecode.com/svn/trunk/file/taxon.jpg' align='center' />

Notes:

1. Standard conventions are followed: oval nodes are URI references, rectangular nodes are literals, arrows represent predicates with the subject at the tail and object at the head.  Predicate URIs are listed in red.

2. Namespace abbreviations are defined in the XML example (below); `tc:, tn:, rdf:, dcterms:, and foaf:` are real namespaces and `gnub:` is made up.

3. The URIs are real and mostly dereferenceable except for the `tn:TaxonConcept` instance URI which is fake.

4. The triples in the upper portion of this graph are contained in the taxon RDF serializations below.  The triples in the lower portion of the graph are mostly contained in the DOI RDF serializations at the bottom of the page.

5. Neither the uBio `tn:TaxonName` instance nor the `gnub:Reference` instance are typed as instances of those classes in the RDF which results from dereferencing their URIs.  Those `rdf:type` assertions are made in the RDF for the `tc:Taxon` RDF.  The `bibo:Article` type assertion is made in the RDF that results from dereferencing the DOI.

6. The RDF which results from dereferencing the uBio URI is not discussed here as it does not follow the TDWG Taxon Name ontology.

7. The term used to connect the identification instance to the taxon is not specified and is out of scope of the current discussion.  That question should be addressed in the future. (Note added 2013-10-13: the Darwin Core RDF Guide ([view draft](DwcRdfGuideProposal#2.7.4_Description_of_a_taxonomic_entity.md)) defines the term `dwcuri:toTaxonConcept` to serve this purpose.)

8. The taxon instance is explicitly typed as `tc:TaxonConcept` in the RDF.  However, even if this were not done, a reasoner could infer this since the four other predicates having the taxon as their subject are declared to have `tc:TaxonConcept` as their domain in the ontology.

In an older version of the ontology `tc:TaxonConcept` is declared to be a class equivalent to `tc:Taxon`.

## tc:TaxonConcept instance RDF/XML serialization ##

```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:gnub="http://globalnames.org/vocabulary/"
xmlns:tc="http://rs.tdwg.org/ontology/voc/TaxonConcept#"
xmlns:tn="http://rs.tdwg.org/ontology/voc/TaxonName#"
>
<tc:TaxonConcept rdf:about="http://globalnames.org/gnub/12345678-90AB-CDEF-1234-567890ABCDEF">

<tc:nameString>Campylorhamphus Bertoni, W 1901</tc:nameString>
<tc:hasName>
     <tn:TaxonName rdf:about="http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:281"/>
</tc:hasName>

<tc:accordingToString>Claramunt Derryberry et al. 2010</tc:accordingToString>
<tc:accordingTo>
     <gnub:Reference rdf:about="http://dx.doi.org/10.1525/auk.2009.09022"/>
</tc:accordingTo>

</tc:TaxonConcept>
</rdf:RDF>
```
Notes:

1. An `rdf:type` assertion of `tn:TaxonName` was made for the object of the `tc:hasName` triple since uBio doesn't type its names.  You can use http://linkeddata.informatik.hu-berlin.de/uridbg/ to dereference the uBio URI to see what properties are provided (it's a real URI).

2. Similarly, the `rdf:type` assertion of `gnub:Reference` is made for the object of the `tc:accordingTo` triple.  This is a made-up class whose purpose is to show that we could assert additional types for the reference which are not asserted by CrossRef in the RDF that they provide when the URI is dereferenced.  Similarly, one could use such type declarations to differentiate between references that simply use the name (i.e. referenced by TNUs) and those which provide a detailed description of how the author defines the taxon.

3. The form of the `tc:accordingToString` string follows the TCS guidelines.  The `tc:nameString` string is the string provided by uBio for the name.

4. It is likely that there will be many more properties provided for the `tc:TaxonConcept` instance.  In particular, properties relating it to parent and child taxa would be likely.  TCS describes a property called "MicroReference" which is an additional qualification for the reference which could provide more specific page or table information within the publication.  The TDWG Common ontology defines the term `tcom:microReference` (http://rs.tdwg.org/ontology/voc/Common#microReference) which serves this purpose.

## tc:TaxonConcept instance RDF/Turtle serialization ##
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix gnub: <http://globalnames.org/vocabulary/>.
@prefix tc: <http://rs.tdwg.org/ontology/voc/TaxonConcept#>.
@prefix tn: <http://rs.tdwg.org/ontology/voc/TaxonName#>.

<http://globalnames.org/gnub/12345678-90AB-CDEF-1234-567890ABCDEF> tc:accordingTo <http://dx.doi.org/10.1525/auk.2009.09022>;
                                                                   tc:accordingToString "Claramunt Derryberry et al. 2010";
                                                                   tc:hasName <http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:281>;
                                                                   tc:nameString "Campylorhamphus Bertoni, W 1901";
                                                                   a tc:TaxonConcept.
<http://www.ubio.org/authority/metadata.php?lsid=urn:lsid:ubio.org:namebank:281> a tn:TaxonName.
<http://dx.doi.org/10.1525/auk.2009.09022> a gnub:Reference.
```

## DOI-identified reference instance RDF/XML serialization ##

```
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:owl="http://www.w3.org/2002/07/owl#"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:bibo="http://purl.org/ontology/bibo/"
xmlns:prism="http://prismstandard.org/namespaces/basic/2.1/"
xmlns:foaf="http://xmlns.com/foaf/0.1/"
xmlns:tc="http://rs.tdwg.org/ontology/voc/TaxonConcept#"
xmlns:tn="http://rs.tdwg.org/ontology/voc/TaxonName#"
>

<rdf:Description rdf:about="http://dx.doi.org/10.1525/auk.2009.09022">
     <dcterms:identifier>10.1525/auk.2009.09022</dcterms:identifier>
     <owl:sameAs rdf:resource="info:doi/10.1525/auk.2009.09022"/>
     <owl:sameAs rdf:resource="doi:10.1525/auk.2009.09022"/>
     <bibo:doi>10.1525/auk.2009.09022</bibo:doi>
     <prism:doi>10.1525/auk.2009.09022</prism:doi>
     <dcterms:date>2010</dcterms:date>
     <dcterms:title>Polyphyly of Campylorhamphus, and Description of a New Genus for C. pucherani (Dendrocolaptinae)</dcterms:title>
     <dcterms:publisher>University of California Press</dcterms:publisher>
     <dcterms:isPartOf rdf:resource="http://id.crossref.org/issn/0004-8038"/>
     <dcterms:creator rdf:resource="http://id.crossref.org/contributor/santiago-claramunt-1v2j098b7oyjc"/>
     <dcterms:creator rdf:resource="http://id.crossref.org/contributor/elizabeth-p-derryberry-1v2j098b7oyjc"/>
     <dcterms:creator rdf:resource="http://id.crossref.org/contributor/r-terry-chesser-1v2j098b7oyjc"/>
     <dcterms:creator rdf:resource="http://id.crossref.org/contributor/alexandre-aleixo-1v2j098b7oyjc"/>
     <dcterms:creator rdf:resource="http://id.crossref.org/contributor/robb-t-brumfield-1v2j098b7oyjc"/>
     <bibo:volume>127</bibo:volume>
     <bibo:pageStart>430</bibo:pageStart>
     <bibo:pageEnd>439</bibo:pageEnd>
     <prism:volume>127</prism:volume>
     <prism:startingPage>430</prism:startingPage>
     <prism:endingPage>439</prism:endingPage>
     <rdf:type rdf:resource="http://purl.org/ontology/bibo/Article"/>
</rdf:Description>

<rdf:Description rdf:about="http://id.crossref.org/issn/0004-8038">
     <dcterms:identifier>0004-8038</dcterms:identifier>
     <bibo:issn>0004-8038</bibo:issn>
     <prism:issn>0004-8038</prism:issn>
     <bibo:eissn>1938-4254</bibo:eissn>
     <prism:eIssn>1938-4254</prism:eIssn>
     <owl:sameAs rdf:resource="urn:issn:0004-8038"/>
     <dcterms:title>The Auk</dcterms:title>
     <dcterms:hasPart rdf:resource="http://dx.doi.org/10.1525/auk.2009.09022"/>
     <rdf:type rdf:resource="http://purl.org/ontology/bibo/Journal"/>
</rdf:Description>

<rdf:Description rdf:about="http://id.crossref.org/contributor/santiago-claramunt-1v2j098b7oyjc">
     <foaf:name>Santiago Claramunt</foaf:name>
     <foaf:givenName>Santiago</foaf:givenName>
     <foaf:familyName>Claramunt</foaf:familyName>
     <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
</rdf:Description>

<rdf:Description rdf:about="http://id.crossref.org/contributor/elizabeth-p-derryberry-1v2j098b7oyjc">
     <foaf:name>Elizabeth P. Derryberry</foaf:name>
     <foaf:givenName>Elizabeth P.</foaf:givenName>
     <foaf:familyName>Derryberry</foaf:familyName>
     <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
</rdf:Description>

<rdf:Description rdf:about="http://id.crossref.org/contributor/r-terry-chesser-1v2j098b7oyjc">
     <foaf:name>R. Terry Chesser</foaf:name>
     <foaf:givenName>R. Terry</foaf:givenName>
     <foaf:familyName>Chesser</foaf:familyName>
<rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
</rdf:Description>

<rdf:Description rdf:about="http://id.crossref.org/contributor/alexandre-aleixo-1v2j098b7oyjc">
     <foaf:name>Alexandre Aleixo</foaf:name>
     <foaf:givenName>Alexandre</foaf:givenName>
     <foaf:familyName>Aleixo</foaf:familyName>
     <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
</rdf:Description>

<rdf:Description rdf:about="http://id.crossref.org/contributor/robb-t-brumfield-1v2j098b7oyjc">
     <foaf:name>Robb T. Brumfield</foaf:name>
     <foaf:givenName>Robb T.</foaf:givenName>
     <foaf:familyName>Brumfield</foaf:familyName>
     <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
</rdf:Description>
</rdf:RDF>
```

Notes:

1. The document shown here is a cleaned up version of the actual document provided by CrossRef. But it contains exactly the same triples.

2. Since the RDF is generated by a provider who is not necessarily concerned with taxa, we are constrained to the property terms chosen by CrossRef.  Fortunately, they nearly exclusively use well-known vocabularies, namely Dublin Core, PRISM, BIBO, and FOAF.  So they provide a model which might be advisable for us to follow in the generation of reference instances that are not identified by DOIs.

3. Their choice of typing vocabulary (BIBO) is probably more appropriate in this case than the more generic DCMI types which would probably type most reference instances as `dcmitype:Text`.

4. The authors are typed as `foaf:Person`.  However, the `dcterms:creator` property has a range of `dcterms:Agent`.  So a reasoner would infer that type for the authors as well.  In addition, `foaf:Person` is a subclass of `foaf:Agent`. So a reasoner would infer that type as well.  Since `dcterms:creator` is declared to be an equivalent property to `foaf:maker` by both FOAF and DCMI, a reasoner could infer the authorship to be an `foaf:maker` property as well.

5. The RDF provided by dereferencing the DOI provides two elements that are required for both TNUs and taxon concepts: authorship and a date.  However, the lack of structure in the authorship properties does not permit discovery of some information such as first authorship and order of authorship.  First authorship could be parsed from the literal object of the `tc:accordingToString` property of the taxon instance.  But the order of authorship is not available directly from the RDF.

6. The author URIs are not dereferenceable at this point.  Because the `dcterms:creator` triples are provided through dereferencing the DOI, the creator of the taxon instance cannot force the use of some other system of identifying taxon authors, such as a biodiversity informatics database of authors, collectors, etc.  However, with some work, such a database could include `owl:sameAs` statements connecting those author URIs to the author URIs minted by CrossRef.

## DOI-identified reference instance RDF Turtle serialization ##

```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix owl: <http://www.w3.org/2002/07/owl#>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix bibo: <http://purl.org/ontology/bibo/>.
@prefix prism: <http://prismstandard.org/namespaces/basic/2.1/>.
@prefix foaf: <http://xmlns.com/foaf/0.1/>.
@prefix tc: <http://rs.tdwg.org/ontology/voc/TaxonConcept#>.
@prefix tn: <http://rs.tdwg.org/ontology/voc/TaxonName#>.

<http://dx.doi.org/10.1525/auk.2009.09022> prism:doi "10.1525/auk.2009.09022";
                                           prism:endingPage "439";
                                           prism:startingPage "430";
                                           prism:volume "127";
                                           dcterms:creator <http://id.crossref.org/contributor/alexandre-aleixo-1v2j098b7oyjc>,
                                                           <http://id.crossref.org/contributor/elizabeth-p-derryberry-1v2j098b7oyjc>,
                                                           <http://id.crossref.org/contributor/robb-t-brumfield-1v2j098b7oyjc>,
                                                           <http://id.crossref.org/contributor/r-terry-chesser-1v2j098b7oyjc>,
                                                           <http://id.crossref.org/contributor/santiago-claramunt-1v2j098b7oyjc>;
                                           dcterms:date "2010";
                                           dcterms:identifier "10.1525/auk.2009.09022";
                                           dcterms:isPartOf <http://id.crossref.org/issn/0004-8038>;
                                           dcterms:publisher "University of California Press";
                                           dcterms:title "Polyphyly of Campylorhamphus, and Description of a New Genus for C. pucherani (Dendrocolaptinae)";
                                           bibo:doi "10.1525/auk.2009.09022";
                                           bibo:pageEnd "439";
                                           bibo:pageStart "430";
                                           bibo:volume "127";
                                           a bibo:Article;
                                           owl:sameAs <doi:10.1525/auk.2009.09022>,
                                                      <info:doi/10.1525/auk.2009.09022>.
<http://id.crossref.org/issn/0004-8038> prism:eIssn "1938-4254";
                                        prism:issn "0004-8038";
                                        dcterms:hasPart <http://dx.doi.org/10.1525/auk.2009.09022>;
                                        dcterms:identifier "0004-8038";
                                        dcterms:title "The Auk";
                                        bibo:eissn "1938-4254";
                                        bibo:issn "0004-8038";
                                        a bibo:Journal;
                                        owl:sameAs <urn:issn:0004-8038>.
<http://id.crossref.org/contributor/alexandre-aleixo-1v2j098b7oyjc> a foaf:Person;
                                                                    foaf:familyName "Aleixo";
                                                                    foaf:givenName "Alexandre";
                                                                    foaf:name "Alexandre Aleixo".
<http://id.crossref.org/contributor/elizabeth-p-derryberry-1v2j098b7oyjc> a foaf:Person;
                                                                          foaf:familyName "Derryberry";
                                                                          foaf:givenName "Elizabeth P.";
                                                                          foaf:name "Elizabeth P. Derryberry".
<http://id.crossref.org/contributor/robb-t-brumfield-1v2j098b7oyjc> a foaf:Person;
                                                                    foaf:familyName "Brumfield";
                                                                    foaf:givenName "Robb T.";
                                                                    foaf:name "Robb T. Brumfield".
<http://id.crossref.org/contributor/r-terry-chesser-1v2j098b7oyjc> a foaf:Person;
                                                                   foaf:familyName "Chesser";
                                                                   foaf:givenName "R. Terry";
                                                                   foaf:name "R. Terry Chesser".
<http://id.crossref.org/contributor/santiago-claramunt-1v2j098b7oyjc> a foaf:Person;
                                                                      foaf:familyName "Claramunt";
                                                                      foaf:givenName "Santiago";
                                                                      foaf:name "Santiago Claramunt".
```