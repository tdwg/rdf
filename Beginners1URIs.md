# Beginner's guide to RDF: 1. Resources and URIs #

[go to part 2: What is RDF and what is it for?](Beginners2WhatIsRDF.md)

[Introduction to the Guide](Beginners.md)

**Contents**



## 1.1  What is a resource? ##

A resource is anything that can be defined and which can be assigned an identifier.  As a matter of convenience, resources can be divided into two categories:

_information resource_ - A resource for which all essential characteristics can be transmitted in a message (i.e. a digital resource).  Historically, information resources have been the primary focus of the Web.  When most users enter a URL into a web browser, they assume that the result will be the return of an information resource in the form of a digital file.  Examples: html web page, digital image, pfd file.

_non-information resource_ - A resource that cannot be transmitted electronically.  Non-information resources can be further subdivided into the following categories:
> - _physical resource_ - a material thing.  Examples: an animal, a specimen, a 35 mm slide

> - _abstract resource_ - a non-material, non-electronic thing.  Examples: a taxonomic concept, a relationship, a determination

## 1.2  What is a URI? ##

URI stands for Uniform Resource Identifier [(1)](#1._RFC_3986.__Uniform_Resource_Identifier_(URI):_Generic_Syntax.md).  URIs are text identifiers that conform to one of several schemes that are described by RFCs (Request For Comments) [(2)](#2._An_RFC_is_not_actually_a_request_for_comments..md) registered with the Internet Assigned Numbers Authority (IANA) [(3)](#3._RFC_4395.__Guidelines_and_Registration_Procedures_for_New_URI.md).  Functionally, a URI serves as a "name" for a "thing", but it is a name which is defined formally enough to be managed by a machine.

In the following example,
```
mailto:joe.shmoe@provider.com
```
is an identifier for an email address which follows the mailto URI scheme described by RFC2368 [(4)](#4._RFC_2368.__The_mailto_URL_scheme.md).  A primary feature of a URI is that it should be globally unique (i.e. refer only to one particular thing).  This is nearly always the case.  It is also generally agreed that a URI should be persistent (i.e. that at a later time the URI should refer to the same thing as it does now), although there is no way to guarantee or enforce this.

In the early days of the Internet, resources were exclusively referred to by URLs (Uniform Resource Locators) and there was an expectation that a URL could be used to locate and retrieve an electronic document by means of some transfer protocol (e.g. the URL `http://rs.tdwg.org/dwc/` retrieves an HTML document about Darwin Core).  However, over time it became accepted that identifiers could refer to non-retrievable resources as well.  The broader term URI came into use to represent an identifier for any kind of resource, including non-information resources.  To some extent, the ability of a device to retrieve, represent, or take action related to a resource described by a URI depends on whether the software used by the device "understands" the URI scheme.  For example, most web browsers "understand" a mailto: URI and will use it to initiate an email message to that address using the user's email software.

So in addition to the expectation that URI should be unique and persistent, it is often considered desirable for URIs to be able to "do" something like making it possible to acquire information about the resource.  However, with the exception of URIs following the HTTP URI scheme, it is generally not safe to assume that a URI can be dereferenced [(5)](#5._Resolving_vs._dereferencing.md) to provide information about the resource.  For example, the URI
```
urn:isbn:0893273651
```
uniquely and permanently identifies the book "Manual of Vascular Plants of Northeastern United States and Adjacent Canada", but a Web browser is unlikely to be able to do anything with that URI. [(6)](#6._RFC_2141.__URN_Syntax.md)

### 1.2.1  Rules about the format of URIs ###
In addition to the requirement that a URI follow a standardized scheme, there are syntax rules that must be followed in order for the URI to be valid.  URI components may be arranged in a hierarchical sequence [(7)](#7._URI_syntax_components.md) and also are restricted to being composed of certain characters [(8)](#8._Characters_in_URIs.md).  If a URI scheme makes use of text characters that are not allowed by the URI standard, they must be encoded in UTF-8 format [(9)](#9._RFC_3629._RTF-8.md).  For example, the URI for a Google search for the Spanish word "niña" would be encoded in the URI as
```
http://www.google.com/search?q=ni%F1a
```
where "%F1" is the hexadecimal representation of the UTF-8 encoding of the Spanish character enye (ñ).

### 1.2.2.  What is an HTTP URI? ###
The most well-known URI scheme is the Hypertext Transfer Protocol (HTTP) [(10)](#10._RFC_2616._Hypertext_Transfer_Protocol_-_HTTP/1.1.md) whose development paralleled the development of the World Wide Web (the Web).  HTTP defines a protocol for communication between a client (such as a web browser) and a server (computer web host).  Because of the standardization and widespread acceptance of HTTP, it is the URI scheme preferred by many users who want to describe resources because an HTTP URI not only provides a means to identify an electronic resource, but also the means to deliver it.

In 2002, a controversy arose whether it was acceptable for an HTTP URI to represent a resource that was not a deliverable, electronic document. [(11)](#11._httpRange-14.md)  Ultimately, the consensus was reached that HTTP URIs could identify non-information resources.  A user could determine the nature of the resource in a very practical way: the client could request the resource identified by the URI and if the client was successful in retrieving it, the resource was an information resource.  However, if the client's initial request did not result in retrieving the resource there were two possible outcomes.  The server could redirect the client to a different URI that was capable of providing a document containing information about the resource; this would serve as an indication that the resource was NOT an information resource.  The server could also return an error message in which case the user could conclude nothing about the resource.

From this decision, a general consensus arose that in the case of a non-information resource identified by an HTTP URI, it was a best practice to provide information about the resource (a "representation" [(12)](#12._Terminology_of_HTTP.md) ) in the form requested by the user (e.g. in HTML if requested by a Web browser).  This can be done through a process called content negotiation. [(13)](#13._Content_Negotiation_in_HTTP.md)  However, there are still many cases where an HTTP URI does not provide any information about the resource at all, or leads the user to information indirectly.

### 1.2.3.  What is an IRI? ###
An Internationalized Resource Identifier (IRI) is an identifier extends "the syntax of URIs to a much wider repertoire of characters".[(14)](#14._RFC_3987._Internationalized_Resource_Identifiers_(IRIs).md)  IRIs may contain unicode characters that are used in alphabets other than the Latin character set (A-Z) Since URIs are a subset of IRIs, in any application which uses IRIs can also use conventional URIs.

## 1.3  Examples ##
In this section there are several examples of different types of resources identified by HTTP URIs which have various responses to an attempt to dereference the URI. (For a detailed explanation of how content negotiation can be achieved using various forms of URIs, see the W3C document [Best Practice Recipes for Publishing RDF Vocabularies](http://www.w3.org/TR/swbp-vocab-pub/).)

### 1.3.1. Mosquito species (content negotiation) ###
The HTTP URI
```
http://lod.geospecies.org/ses/4XSQO
```
represents an abstract non-information resource: the species concept for the mosquito Aedes vexans.  Obviously, it is not possible to deliver the mosquito species through the Internet, or even an individual mosquito.  Dereferencing this URI via a web browser redirects to the URI
```
http://lod.geospecies.org/ses/4XSQO?format=html
```
which is an information resource (an HTML web page) about Aedes vexans.

### 1.3.2.  Rock band (hash URI) ###
The HTTP URI
```
http://dbpedialite.org/things/52780#id
```
represents a physical non-information resource: the band U2.  The server ignores the part of the URI after the hash character (#) and returns the document
```
http://dbpedialite.org/things/52780
```
which is an HTML web page about the band.

### 1.3.3.  Rating: a descriptive term for media (poor redirection) ###
The HTTP URI
```
http://ns.adobe.com/xap/1.0/Rating
```
represents an abstract non-information resource: the rating given to a media item.  Although entering this URI into a Web browser does result in redirection to an information resource, that resource provides information about Adobe XMP rather than specifically about Rating.

### 1.3.4. CreditLine: a descriptive term for media (not dereferenceable) ###
The HTTP URI
```
http://iptc.org/std/Iptc4xmpExt/1.0/xmlns/CreditLine
```
represents an abstract non-information resource: the credit line for a media item.  Entering this URI into a Web browser doesn't do anything.  In this case, attaching "`http://iptc.org/std/Iptc4xmpExt/1.0/xmlns/`" to the term "`CreditLine`" simply makes the identifier globally unique but doesn’t actually make use of the HTTP protocol to do anything.

## 1.4. Testing a URI ##
Vapour is a "Linked Data Validator" [(15)](#15._Vapour_Linked_Data_validator_for_checking_URIs.md) which can be used to test whether a URI is dereferenceable and if it dereferences, to determine based on the server response whether the resource identified by the URI is an information resource or not.

http://validator.linkeddata.org/vapour

You can test the above examples to see what happens.


# References: #
An important general reference on this subject is [Architecture of the World Wide Web](http://www.w3.org/TR/webarch/), a W3C Recommendation.

### 1. RFC 3986.  Uniform Resource Identifier (URI): Generic Syntax ###
http://tools.ietf.org/html/rfc3986

### 2. An RFC is not actually a request for comments. ###
It's a memo published by the Internet Engineering Task Force (IETF; http://www.ietf.org/) which is responsible for managing the standards of the Internet.  An RFC starts out as a somewhat informal proposal or description of a new idea.  The RFC may eventually be adopted as an Internet standard.

Search for an RFC: http://www.ietf.org/rfc.html

Full list: http://www.ietf.org/download/rfc-index.txt

### 3. RFC 4395.  Guidelines and Registration Procedures for New URI Schemes ###
http://tools.ietf.org/html/rfc4395

A list of registered URI schemes and the RFCs that describe them is at:
http://www.iana.org/assignments/uri-schemes.html

### 4. RFC 2368.  The mailto URL scheme ###
http://tools.ietf.org/html/rfc2368

### 5. Resolving vs. dereferencing ###
The terms "resolving" and "dereferencing" a URI are sometimes colloquially used interchangeably.  Technically, "URI 'resolution' is the process of determining an access mechanism and the appropriate parameters necessary to dereference a URI; this resolution may require several iterations.  To use that access mechanism to perform an action on the URI's resource is to 'dereference' the URI."  (Definition from RFC3986 at http://tools.ietf.org/html/rfc3986#section-1.2.2)

### 6. RFC 2141.  URN Syntax ###
For more information on the URN URI scheme, see:
http://tools.ietf.org/html/rfc2141
and
http://www.iana.org/assignments/urn-namespaces/urn-namespaces.xml
for a list of registered types of URNs.

### 7. URI syntax components ###
A description of the syntax of URIs is at:
http://tools.ietf.org/html/rfc3986#section-3

### 8. Characters in URIs ###
http://tools.ietf.org/html/rfc3986#section-2

### 9. RFC 3629. UTF-8 ###
http://tools.ietf.org/html/rfc3629

### 10. RFC 2616. Hypertext Transfer Protocol - HTTP/1.1 ###
http://tools.ietf.org/html/rfc2616

### 11. httpRange-14 ###
This controversy became known as "httpRange-14" and is described at
http://www.w3.org/2001/tag/issues.html#httpRange-14

See also http://www.jenitennison.com/blog/node/168 for more discussion on the httpRange-14 issue.

### 12. Terminology of HTTP ###
See definitions of "resource" and "representation" at
http://tools.ietf.org/html/rfc2616#section-1.3

### 13. Content Negotiation in HTTP ###
Content negotiation is described at:
http://tools.ietf.org/html/rfc2616#section-12

### 14. RFC 3987. Internationalized Resource Identifiers (IRIs) ###
http://tools.ietf.org/html/rfc3987

### 15. Vapour Linked Data validator for checking URIs ###
http://validator.linkeddata.org/vapour


---

Thanks to Paul Murray for helpful feedback.

Questions? Comments? Contact [Steve Baskauf](mailto:steve.baskauf@vanderbilt.edu?subject=RDFguide)

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.