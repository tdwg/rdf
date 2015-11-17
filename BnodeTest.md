

# The RDF #
This is a test of the behavior of RDF involving a Dublin Core term, `dcterms:creator` (which is defined to have a non-literal range of `dcterms:Agent`) written in different forms and with the Agent as either a blank node or a named URI reference node.  To see a graphical version of the RDF graph, go to the W3C RDF validator http://www.w3.org/RDF/Validator/ and either paste in the RDF/XML, or check by the URI listed below.

## RDF/XML ##

File (without comments) at http://bioimages.vanderbilt.edu/rdf/examples/bnode-test.rdf
```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dcterms="http://purl.org/dc/terms/"
>
<!--Document 0 has the creator specified with the parseType shortcut 
(no rdf:type declaration)-->
<rdf:Description rdf:about="http://example.org/document0.html">
     <dcterms:creator rdf:parseType="Resource">
          <rdf:value>Author 0</rdf:value>
     </dcterms:creator>
     <dcterms:title>Document 0</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries"/>
</rdf:Description>

<!--Document 1 has the creator specified with the parseType shortcut 
 but has an explicit declaration of the creator's type-->
<rdf:Description rdf:about="http://example.org/document1.html">
     <dcterms:creator rdf:parseType="Resource">
          <rdf:type rdf:resource="http://purl.org/dc/terms/Agent"/>
          <rdf:value>Author 1</rdf:value>
     </dcterms:creator>
     <dcterms:title>Document 1</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries"/>
</rdf:Description>

<!--Document 2 has the creator specified using the class as the XML container 
element name, creating an implicit declaration of the creator's type-->
<rdf:Description rdf:about="http://example.org/document2.html">
     <dcterms:creator>
          <dcterms:Agent>
              <rdf:value>Author 2</rdf:value>
          </dcterms:Agent>
     </dcterms:creator>
     <dcterms:title>Document 2</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries"/>
</rdf:Description>

<!--Document 3 uses the generic Description XML with an explicit declaration of the creator's type-->
<rdf:Description rdf:about="http://example.org/document3.html">
     <dcterms:creator>
          <rdf:Description>
               <rdf:type rdf:resource="http://purl.org/dc/terms/Agent"/>
               <rdf:value>Author 3</rdf:value>
          </rdf:Description>
     </dcterms:creator>
     <dcterms:title>Document 3</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries"/>
</rdf:Description>

<!--Document 4 has the creator specified using the class as the XML container 
element name, (implicit type declaration) and has a named URI node rather 
than a blank node-->
<rdf:Description rdf:about="http://example.org/document4.html">
     <dcterms:creator>
          <dcterms:Agent rdf:about="http://example.org/author4">
              <rdf:value>Author 4</rdf:value>
          </dcterms:Agent>
     </dcterms:creator>
     <dcterms:title>Document 4</dcterms:title>
     <dcterms:isPartOf rdf:resource="http://example.org/bookSeries"/>
</rdf:Description>
</rdf:RDF>
```

## RDF/Turtle ##

File at http://bioimages.vanderbilt.edu/rdf/examples/bnode-test.ttl
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.

<http://example.org/author4> a dcterms:Agent;
                             rdf:value "Author 4".
<http://example.org/document0.html> dcterms:creator [rdf:value "Author 0"];
                                    dcterms:isPartOf <http://example.org/bookSeries>;
                                    dcterms:title "Document 0".
<http://example.org/document1.html> dcterms:creator [rdf:value "Author 1" ; 
                                                     a dcterms:Agent];
                                    dcterms:isPartOf <http://example.org/bookSeries>;
                                    dcterms:title "Document 1".
<http://example.org/document2.html> dcterms:creator [rdf:value "Author 2" ; 
                                                     a dcterms:Agent];
                                    dcterms:isPartOf <http://example.org/bookSeries>;
                                    dcterms:title "Document 2".
<http://example.org/document3.html> dcterms:creator [rdf:value "Author 3" ; 
                                                     a dcterms:Agent];
                                    dcterms:isPartOf <http://example.org/bookSeries>;
                                    dcterms:title "Document 3".
<http://example.org/document4.html> dcterms:creator <http://example.org/author4>;
                                    dcterms:isPartOf <http://example.org/bookSeries>;
                                    dcterms:title "Document 4".
```

## RDF/N3 ##
http://bioimages.vanderbilt.edu/rdf/examples/bnode-test.n3
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix dcterms: <http://purl.org/dc/terms/>.

_:autos1 <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 0".
_:autos2 a <http://purl.org/dc/terms/Agent>;
         <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 1".
_:autos3 a <http://purl.org/dc/terms/Agent>;
         <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 2".
_:autos4 a <http://purl.org/dc/terms/Agent>;
         <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 3".
<http://example.org/author4> a <http://purl.org/dc/terms/Agent>;
                             <http://www.w3.org/1999/02/22-rdf-syntax-ns#value> "Author 4".
<http://example.org/document0.html> <http://purl.org/dc/terms/creator> _:autos1;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries>;
                                    <http://purl.org/dc/terms/title> "Document 0".
<http://example.org/document1.html> <http://purl.org/dc/terms/creator> _:autos2;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries>;
                                    <http://purl.org/dc/terms/title> "Document 1".
<http://example.org/document2.html> <http://purl.org/dc/terms/creator> _:autos3;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries>;
                                    <http://purl.org/dc/terms/title> "Document 2".
<http://example.org/document3.html> <http://purl.org/dc/terms/creator> _:autos4;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries>;
                                    <http://purl.org/dc/terms/title> "Document 3".
<http://example.org/document4.html> <http://purl.org/dc/terms/creator> <http://example.org/author4>;
                                    <http://purl.org/dc/terms/isPartOf> <http://example.org/bookSeries>;
                                    <http://purl.org/dc/terms/title> "Document 4".
```

# SPARQL queries #
I tried these on FireFox, Opera, IE, Chrome, and Safari.

FireFox and Opera ask to open the first query with a helper application (text or RDF editor) so if you don't want to bother doing that, skip to the second query and you can see the results directly in the browser window.  IE, Safari, and Chrome wanted to use a helper application for all of them.  So if you don't want to configure an editor use either FireFox or Opera for the minimum time and annoyance.

The queries were performed on the dataset http://bioimages.vanderbilt.edu/rdf/examples/bnode-test.rdf loaded into the TG sandbox at http://tdwg-rdf.net/store2/ .  Apparently the sandbox can only parse XML, so if in the future you want to experiment and have created RDF in Turtle or N3, you will have to convert it to XML first.  I used rdfEditor http://www.dotnetrdf.org/content.asp?pageID=rdfEditor on a Windows platform to make the conversions.

All queries use the following prefixes:
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
```
Replace the default text in the box with this text, then skip a line and enter the queries below one at at time.

## query 1 ##
The purpose of this query was to see if all books can be found.
```
SELECT ?book 
WHERE {
  ?book dcterms:isPartOf <http://example.org/bookSeries>.
} 
```
## query 2 ##
The purpose of this query was to construct a list of author names.
```
CONSTRUCT {
?author rdf:value ?name.
} 
WHERE {
  ?author rdf:value ?name.
  ?book dcterms:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries>.
} 
```
## query 3 ##
The purpose of this query was to construct a book/author name list
```
CONSTRUCT {
?book dc:creator ?name.
} 
WHERE {
  ?author rdf:value ?name.
  ?book dcterms:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries>.
}
```
## query 4 ##
The purpose of this query was to display the type of the author.  No type, no author listed.
```
CONSTRUCT {
?author rdf:type ?class.
} 
WHERE {
  ?author a ?class.
  ?book dcterms:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries>.
} 
```
## query 5 ##
The purpose of this query was to display the type of the book's author.  If the type of dcterms:creator is not known, the book will not be listed.  Note that the predicate is a fake - CONSTRUCT doesn't care!
```
CONSTRUCT {
?book dcterms:authorType ?class.
} 
WHERE {
  ?author a ?class.
  ?book dcterms:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries>.
} 
```
## query 6 ##
The purpose of this query was to list books/authors for books which have agents as authors.  If the type of the dcterms:creator is not known, the book should not be listed.
```
CONSTRUCT {
?book dc:creator ?name.
} 
WHERE {
  ?author a dcterms:Agent.
  ?author rdf:value ?name.
  ?book dcterms:creator ?author.
  ?book dcterms:isPartOf <http://example.org/bookSeries>.
} 
```