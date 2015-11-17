![http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)  [http://www.tdwg.org](http://www.tdwg.org/)

# Expressing License Properties as RDF #

**Date:** (Created) 24 August 2013; (Last modified) 9 Novenber 2013

**Status:** Not part of any standard ([Type 3](http://www.tdwg.org/fileadmin/tdwg_std_drafts/tdwg_standards_documentation_specification.html#a_3) document); intended to complement the RDF Guide of the Darwin Core Standard (http://www.tdwg.org/standards/450/)

**Permanent URL:** http://

**TDWG Task Group:** [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)

**Contributors:** [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide) (TDWG RDF/OWL Task Group)

**Abstract:** This document discusses terms which can be used to express the license properties of a resource and the circumstances under which the various terms might be used.

![http://i.creativecommons.org/l/by/3.0/88x31.png](http://i.creativecommons.org/l/by/3.0/88x31.png) Licensed under [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/deed)

**Table of Contents:**


The following namespace abbreviations are used in this document:

|vocabulary name|namespace abbreviation|full prefix|
|:--------------|:---------------------|:----------|
|Resource Description Framework|rdf:                  |http://www.w3.org/1999/02/22-rdf-syntax-ns#|
|RDF Schema     |rdfs:                 |http://www.w3.org/2000/01/rdf-schema#|
|Creative Commons Rights Expression Language|cc:                   |http://creativecommons.org/ns#|
|XHTML Vocabulary|xhv:                  |http://www.w3.org/1999/xhtml/vocab#|
|Dublin Core Metadata Terms|dcterms:              |http://purl.org/dc/terms/|
|Dublin Core legacy terms|dc:                   |http://purl.org/dc/elements/1.1/|
|Extensible Metadata Platform Rights Management vocabulary|xmpRights:            |http://ns.adobe.com/xap/1.0/rights/|

## 1 Introduction ##

The Dublin Core Metadata Initiative (DCMI) vocabulary (defined at http://dublincore.org/documents/dcmi-terms/) describes the core relationships among property rights terms.  The property `dcterms:rights` is defined as "information about rights held in and over the resource". These rights can include rights of access (described using the subproperty `dcterms:accessRights`) and intellectual property rights such as copyright.  An important subproperty of `dcterms:rights` is `dcterms:license`, defined as "a legal document giving official permission to do something with the resource".

The Creative Commons organization (http://creativecommons.org/) has standardized a set of licenses which allow creators of intellectual property to retain copyright of their works while allowing certain types of use without requiring permission from the copyright owner.  These licenses are widely used on the Internet and have become the de-facto standard for specifying how works can be reused by others.  Each license is identified by a URI which can be the object of an RDF triple.

## 2 License properties ##

In addition to `dcterms:license`, there are three well-known properties that can be used as predicates in RDF triples describing license properties of a resource.

### 2.1 xmpRights:UsageTerms ###

Audubon Core (supply permanent URL here) specifies that `xmpRights:UsageTerms` should be used to describe "the license statement defining how resources may be used" and provides an example of a string description of a Creative Commons license.  The `xmpRights:` namespace terms are defined in a PDF document rather than as RDF, so following the example of Audubon Core and expressing the value of `xmpRights:UsageTerms` as a literal object in an RDF triple would not introduce any inconsistencies.  The definition of `xmpRights:UsageTerms` does not specify any formal relationship between it and any other property such as `dcterms:license`.  The following examples use `xmpRights:UsageTerms` as an RDF predicate having a literal object:

RDF/XML:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87943">
     <xmpRights:UsageTerms xml:lang="en">Available under Creative Commons Attribution-Noncommercial-Share Alike 3.0 license</xmpRights:UsageTerms>
</rdf:Description>
```

Turtle:
```
<http://bioimages.vanderbilt.edu/baskauf/87943>
     xmpRights:UsageTerms "Available under Creative Commons Attribution-Noncommercial-Share Alike 3.0 license"@en.
```

### 2.2 xhv:license ###

Creative Commons provides guidelines for expressing license information on the Semantic Web in the form of RDFa (http://wiki.creativecommons.org/RDFa).  The following snippet of XHTML contains RDF in the form of RDFa:

```
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/"><img alt="fruit of Hedyotis crassifolia" style="border-width:0" src="http://bioimages.vanderbilt.edu/gq/baskauf/g87943.jpg" /></a>
```

Using the rel="license" attribute of an anchor tag in RDFa asserts an `xhv:license` property (in addition to establishing a generic HTML Link Relation; see http://www.iana.org/assignments/link-relations/link-relations.xml).  A client capable of consuming RDFa would infer the same triple as in these examples:

RDF/XML:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/gq/baskauf/g87943.jpg">
     <xhv:license rdf:resource="http://creativecommons.org/licenses/by-nc-sa/3.0/"/>
</rdf:Description>
```

Turtle:
```
<http://bioimages.vanderbilt.edu/gq/baskauf/g87943.jpg>
     xhv:license <http://creativecommons.org/licenses/by-nc-sa/3.0/>.
```

The term `xhv:license` is itself defined in RDFa at http://www.w3.org/1999/xhtml/vocab/ (view the page source to see the underlying RDFa).  The definition simply states that `xhv:license` is an `rdf:Property` with a text comment that the term "refers to a resource that defines the associated license".  There are no formal semantics that relate `xhv:license` to any other term.

### 2.3 cc:license ###

Creative Commons defines a Creative Commons Rights Expression Language (http://creativecommons.org/ns ; view the page source to see the underlying RDFa which defines the vocabulary) which can be used to describe licenses in RDF.  This vocabulary includes the term `cc:license` which is used to link a work to its license.  The definition of `cc:license` declares it to be `rdfs:subPropertyOf dcterms:license` and to be `owl:sameAs xhv:license`.  Thus an application which is aware of the definition of `cc:license` in RDF can use that definition to infer additional properties that are not necessarily stated explicitly in the RDF describing a work.  For example, if the following RDF is asserted:

RDF/XML:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87943">
     <cc:license rdf:resource="http://creativecommons.org/licenses/by-nc-sa/3.0/"/>
</rdf:Description>
```

Turtle:
```
<http://bioimages.vanderbilt.edu/baskauf/87943>
     cc:license <http://creativecommons.org/licenses/by-nc-sa/3.0/>.
```

a client that conducts inferencing based on the definition of `cc:license` can infer the following triples:

RDF/XML:
```
<rdf:Description rdf:about="http://bioimages.vanderbilt.edu/baskauf/87943">
     <cc:license rdf:resource="http://creativecommons.org/licenses/by-nc-sa/3.0/"/>
     <xhv:license rdf:resource="http://creativecommons.org/licenses/by-nc-sa/3.0/"/>
     <dcterms:license rdf:resource="http://creativecommons.org/licenses/by-nc-sa/3.0/"/>
</rdf:Description>
```

Turtle:
```
<http://bioimages.vanderbilt.edu/baskauf/87943>
     cc:license <http://creativecommons.org/licenses/by-nc-sa/3.0/>;
     xhv:license <http://creativecommons.org/licenses/by-nc-sa/3.0/>;
     dcterms:license <http://creativecommons.org/licenses/by-nc-sa/3.0/>.
```

Additionally, a client could infer additional triples based on the definition of `dcterms:license` which declares it to be `rdfs:subPropertyOf dcterms:rights`, `rdfs:subPropertyOf dc:rights`, and have `rdfs:range dcterms:LicenseDocument`.

A client that is aware of the RDF definition of `cc:license` can infer all of the same triples in the example above from RDF that only explicitly asserts a single triple containing an `xhv:license`. property.  However, a client that is unaware of the RDF definition of `cc:license` cannot make such inferences based solely on the definition of `xhv:license`.

## 3. Implications ##

Providers expressing license information using RDFa should be aware that use of the `rel="license"` attribute asserts explicitly only an `xhv:license` property for the work.  Providers using other serializations of RDF (such as XML or Turtle) to express a `cc:license` for a work should be aware that clients will not necessarily reason all of the possible triples that can be inferred based on the definition of `cc:license`.  If maximum expressiveness is important to the provider, the provider should assert all of the desired license property triples explicitly.

Similarly, consumers and application developers should be aware that providers will not necessarily provide license properties using all of the terms listed above.  They should take this into consideration when designing queries to locate resources having particular license properties.