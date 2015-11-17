**Contents**



# Scenario #
In this scenario, we model two inverse relationships: hasParent and hasChild.  The following namespaces are used, although they could really be anything:
```
PREFIX local: <http://bioimages.vanderbilt.edu/rdf/local#>
PREFIX ns: <http://fake.org/>
```
The relationships can be represented graphically like this:
![http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse-family-properties.png](http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse-family-properties.png)
The two relationships are declared to be inversely related using the `owl:inverseOf` property.  Normally, only one of the `owl:inverseOf` declarations would be required since the second could be inferred from the first.  But to simplify the query, both have been asserted explicitly.

The following graph will be used in the example:

![http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse-family-relationships.png](http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse-family-relationships.png)

The RDF can be viewed as RDF/XML by [clicking here](http://code.google.com/p/tdwg-rdf/source/browse/trunk/example/inverse.rdf) or downloaded by [saving this link](http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse.rdf).  It can be viewed as RDF/Turtle by [clicking here](http://code.google.com/p/tdwg-rdf/source/browse/trunk/example/inverse.ttl) or downloaded by [saving this link](http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse.ttl).

Note that some possible hasParent and hasChild relationships are missing.  The query in the following section will infer these missing triples that are entailed by the `owl:inverseOf` declarations.

# The query #
Here is the whole query:
```
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX local: <http://bioimages.vanderbilt.edu/rdf/local#>
CONSTRUCT {?resource1 ?property2 ?resource2}
FROM <http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse.rdf>
WHERE 
 {
 ?property1 owl:inverseOf ?property2.
 ?resource2 ?property1 ?resource1.
 OPTIONAL 
      {
      ?R3 ?property2 ?resource2.
      FILTER(?R3 = ?resource1).
      }
 FILTER(!BOUND(?R3))
 }
Limit 10
```

The query can be broken down into parts.
```
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX local: <http://bioimages.vanderbilt.edu/rdf/local#>
```
defines the namespace abbreviations that are used in the query.

```
FROM <http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse.rdf>
```
limits the query to a particular graph that has been uploaded to the triplestore.  `http://tdwg-rdf.googlecode.com/svn/trunk/example/inverse.rdf` is the URI of that graph.


```
WHERE 
 {
 ?property1 owl:inverseOf ?property2.
 ?resource2 ?property1 ?resource1.
 }
```
binds the `?property1` variable to URIs which have declared inverses and which serve as a predicate for some triple containing `?resource2` and `?resource1`.

```
CONSTRUCT {?resource1 ?property2 ?resource2}
```
constructs a triple where the two resources have their subject and object positions reversed.  The predicate of that triple is the property which was declared as the inverse of the bound `?property1`.

```
 OPTIONAL 
      {
      ?R3 ?property2 ?resource2.
      FILTER(?R3 = ?resource1).
      }
 FILTER(!BOUND(?R3))
```
is a filter which excludes pre-existing inverse triples.  This ensures that only new triples will be constructed.

# Performing the query #
  1. Navigate to the TDWG RDF Task Group SPARQL sandbox: http://tdwg-rdf.phylodiversity.net/store2/ The graph to which the query is restricted should already be loaded into the triplestore unless somebody has deleted it.
  1. Copy the full query from its listing above and paste it into the "SPARQL query with form" box.
  1. Set RDF Inference to "No"
  1. Click on the "Execute" button. In most browsers, the result will appear as RDF/XML.
  1. To return to the query form, use the back button of the browser.

# What does the result mean? #

The result can be translated to RDF/Turtle using software such as rdfEditor (listed in the [Beginner's Guide to RDF](http://code.google.com/p/tdwg-rdf/wiki/Beginners#0.3.5._Software_tools)).  It looks like this (cleaned up):
```
@prefix local: <http://bioimages.vanderbilt.edu/rdf/local#>.
@prefix ns: <http://fake.org/>.
@prefix owl: <http://www.w3.org/2002/07/owl#>.

ns:jessie
     local:hasParent ns:carol.
     
ns:carmen
     local:hasParent ns:steve.
     
ns:steve
     local:hasChild ns:jessie.
```
By comparing this with the second diagram above, you can see that it provides triples that correspond to the three missing relationships.