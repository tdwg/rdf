

# The RDF #
This is a test of the behavior of RDF involving a Dublin Core term, `dcterms:creator` (which is defined to have a non-literal range of `dcterms:Agent`) and `dc:creator` (with no declared range).  To see a graphical version of the RDF graph, go to the W3C RDF validator http://www.w3.org/RDF/Validator/ and either paste in the RDF/XML, or check by the URI listed below.

## RDF/XML ##
File at http://bioimages.vanderbilt.edu/rdf/examples/good-rdf-bad-rdf-test.rdf
```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:dctype="http://purl.org/dc/dcmitype/"
>
<!-- "good" RDF -->
<!-- note: all documents are typed as dctype:Text by their XML container name -->

<!-- Document 5 uses parseType shortcut to create a blank node for the Agent-->
<dctype:Text rdf:about="http://example.org/document5.html">
     <dcterms:creator rdf:parseType="Resource">
          <rdf:value>Author 5</rdf:value>
     </dcterms:creator>
     <dcterms:title>Document 5</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries1"/>
</dctype:Text>

<!-- Document 6 uses a named URI node for the Agent -->
<dctype:Text rdf:about="http://example.org/document6.html">
     <dcterms:creator>
          <dcterms:Agent rdf:about="http://example.org/author6">
              <rdf:value>Author 6</rdf:value>
          </dcterms:Agent>
     </dcterms:creator>
     <dcterms:title>Document 6</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries1"/>
</dctype:Text>

<!-- Document 7 uses the dc: term rather than the dcterms: term -->
<dctype:Text rdf:about="http://example.org/document7.html">
     <dc:creator>Author 7</dc:creator>
     <dcterms:title>Document 7</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries1"/>
</dctype:Text>

<!-- Document 8 uses both the dc:term and the dcterms: term -->
<dctype:Text rdf:about="http://example.org/document8.html">
     <dc:creator>Author 8</dc:creator>
     <dcterms:creator>
          <dcterms:Agent rdf:about="http://example.org/author8">
              <rdf:value>Author 8</rdf:value>
          </dcterms:Agent>
     </dcterms:creator>
     <dcterms:title>Document 8</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries1"/>
</dctype:Text>

<!-- "bad" RDF -->

<!-- Document 9 incorrectly uses a literal for a term (dcterms:creator) defined to have rdfs:Literal range-->
<dctype:Text rdf:about="http://example.org/document9.html">
     <dcterms:creator>Author 9</dcterms:creator>
     <dcterms:title>Document 9</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries1"/>
</dctype:Text>

</rdf:RDF>
```
## RDF/Turtle ##
File at http://bioimages.vanderbilt.edu/rdf/examples/good-rdf-bad-rdf-test.ttl
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dc: <http://purl.org/dc/elements/1.1/>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix dctype: <http://purl.org/dc/dcmitype/>.

<http://example.org/author6> a dcterms:Agent;
                             rdf:value "Author 6".
<http://example.org/author8> a dcterms:Agent;
                             rdf:value "Author 8".
<http://example.org/document5.html> dcterms:creator [rdf:value "Author 5"];
                                    dcterms:isPartOf <http://example.org/bookSeries1>;
                                    dcterms:title "Document 5";
                                    a dctype:Text.
<http://example.org/document6.html> dcterms:creator <http://example.org/author6>;
                                    dcterms:isPartOf <http://example.org/bookSeries1>;
                                    dcterms:title "Document 6";
                                    a dctype:Text.
<http://example.org/document7.html> dc:creator "Author 7";
                                    dcterms:isPartOf <http://example.org/bookSeries1>;
                                    dcterms:title "Document 7";
                                    a dctype:Text.
<http://example.org/document8.html> dc:creator "Author 8";
                                    dcterms:creator <http://example.org/author8>;
                                    dcterms:isPartOf <http://example.org/bookSeries1>;
                                    dcterms:title "Document 8";
                                    a dctype:Text.
<http://example.org/document9.html> dcterms:creator "Author 9";
                                    dcterms:isPartOf <http://example.org/bookSeries1>;
                                    dcterms:title "Document 9";
                                    a dctype:Text.
```
## RDF/N3 ##
File at http://bioimages.vanderbilt.edu/rdf/examples/good-rdf-bad-rdf-test.n3
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dc: <http://purl.org/dc/elements/1.1/>.
@prefix dcterms: <http://purl.org/dc/terms/>.
@prefix dctype: <http://purl.org/dc/dcmitype/>.

_:autos1 <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 5".
<http://example.org/author6> a <http://purl.org/dc/terms/Agent>;
                             <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 6".
<http://example.org/author8> a <http://purl.org/dc/terms/Agent>;
                             <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 8".
<http://example.org/document5.html> <http://purl.org/dc/terms/creator> _:autos1;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries1>;
                                    <http://purl.org/dc/terms/title> "Document 5";
                                    a <http://purl.org/dc/dcmitype/Text>.
<http://example.org/document6.html> <http://purl.org/dc/terms/creator> <http://example.org/author6>;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries1>;
                                    <http://purl.org/dc/terms/title> "Document 6";
                                    a <http://purl.org/dc/dcmitype/Text>.
<http://example.org/document7.html> <http://purl.org/dc/elements/1.1/creator> "Author 7";
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries1>;
                                    <http://purl.org/dc/terms/title> "Document 7";
                                    a <http://purl.org/dc/dcmitype/Text>.
<http://example.org/document8.html> <http://purl.org/dc/elements/1.1/creator> "Author 8";
                                    <http://purl.org/dc/terms/creator> <http://example.org/author8>;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries1>;
                                    <http://purl.org/dc/terms/title> "Document 8";
                                    a <http://purl.org/dc/dcmitype/Text>.
<http://example.org/document9.html> <http://purl.org/dc/terms/creator> "Author 9";
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries1>;
                                    <http://purl.org/dc/terms/title> "Document 9";
                                    a <http://purl.org/dc/dcmitype/Text>.
```
# SPARQL queries #
Use Firefox or Opera if you want to view the results directly in the browser window rather than having the results file opened by a helper application.

The queries were performed on the dataset http://bioimages.vanderbilt.edu/rdf/examples/good-rdf-bad-rdf-test.rdf loaded into the TG sandbox at http://tdwg-rdf.phylodiversity.net/store2/ .

All queries use the following prefixes:
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX dctype: <http://purl.org/dc/dcmitype/>
```
Replace the default text in the box with this text, then skip a line and enter the queries below one at at time.
## query 1 ##
The purpose of this query is to see how the `dcterms:creator` is listed.
```
CONSTRUCT {
?book dcterms:creator ?author.
} 
WHERE {
  ?book dcterms:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries1>.
} 
```
Result same whether inferencing is turned on or not: bnode ID given for document 5, URIs for documents 6 and 8, literal given for document 9.

## query 2 ##
The purpose of this query is to find out what the SPARQL query will say is the class is of the author.  Note: the constructed triples are nonsense because the predicate is not a property.  However, the predicate serves to identify the book associated with the author.
```
CONSTRUCT {
?class ?book ?author.
} 
WHERE {
  ?author a ?class.
  ?book dcterms:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries1>.
} 
```
Result without inferencing: documents 6 and 8 identified as type `dcterms:Agent` because of the XML container element name.  With inferencing: documents 5, 6, 8, and 9 are identified as type `dcterms:Agent` with documents 5 and 9 inferred from the range of `dcterms:creator`.  Note that the reasoner has no problem inferring that the literal object of the `dcterms:creator` of document 9 is an instance of the `dcterms:Agent` class.  The reasoner does not give `rdfs:Literal` as the class of the literal object of the `dcterms:creator` of document 9.

## query 3 ##
The purpose of this query is to figure out what triples are inferred to have `dc:creator` as a predicate.
```
CONSTRUCT {
  ?book dc:creator ?author.
} 
WHERE {
  ?book dc:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries1>.
} 
```
Result with inferencing off: the two documents which have explicit `dc:creator` predicates are given.  With inferencing turned on the result is the same.  Despite the fact that "4sr reasons over ... subProperty", it does not seem to infer `dc:creator` triples from triples containing `dcterms:creator` even though the definition of `dcterms:creator` in RDF states that `dcterms:creator rdfs:subPropertyOf dc:creator`.