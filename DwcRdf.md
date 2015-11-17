> [![](http://tdwg-rdf.googlecode.com/svn/trunk/file/tdwg-logo.png)](http://www.tdwg.org/)

# Cover page for RDF Guide addition to Darwin Core #

[Approved version of the RDF Guide Proposal](DwcRdfGuideFinal.md). See [below](#Version_history.md) for version history.  This document was revised in May 2015.

**Note: because Google Code will be shutting down in 2015-16, please do not make permanent links to this page.  Rather, link to the Darwin Core standard itself at its permanent URL: http://www.tdwg.org/standards/450/ or to the eventual URL of this guide: http://rs.tdwg.org/dwc/terms/guides/rdf/.**

## Background ##

The [Darwin Core](http://www.tdwg.org/standards/450/) [technical specification](http://www.tdwg.org/standards/status-and-categories/) was adopted as a [TDWG Standard](http://www.tdwg.org/standards/) in 2009.  The Darwin Core standard consists of a [Type 1](http://bioimages.vanderbilt.edu/pages/tdwg-stds-spec.pdf) normative document ([dwctermshistory.rdf](http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwctermshistory.rdf)) which defines its terms using [Resource Description Framework (RDF)](http://www.w3.org/TR/rdf11-concepts/), and numerous [Type 2](http://bioimages.vanderbilt.edu/pages/tdwg-stds-spec.pdf) non-normative documents which explain the standard (and are themselves part of the standard).  Many of these non-normative standards documents can be viewed on the [Darwin Core web pages](http://rs.tdwg.org/dwc/index.htm) that are part of the [TDWG website](http://www.tdwg.org/).  Among these non-normative documents are several best-practices guides (the [Text Guide](http://rs.tdwg.org/dwc/terms/guides/text/index.htm) and the [XML Guide](http://rs.tdwg.org/dwc/terms/guides/xml/index.htm)) which explain how to use Darwin Core terms to transmit biodiversity data.

Part 3 of the Darwin Core [Namespace Policy document](http://rs.tdwg.org/dwc/terms/namespace/index.htm) describes how the Darwin Core Standard can be changed or extended.  This is the cover page of the proposal to modify Darwin Core under the Namespace Policy.  The proposal included:
  * an [RDF Guide](DwcRdfGuideProposalRevised.md) that has joined the other best-practices guides as non-normative (Type 2) documents that are part of the standard and which will eventually be part of the Darwin Core web pages on the TDWG website.
  * term additions and modifications necessary to implement the recommendations of the RDF Guide.  Most of these changes involve the addition of terms in a new _dwciri:_ namespace (`http://rs.tdwg.org/dwc/iri/`) These term additions will be added to the normative (Type 1) RDF document and to other documents as necessary for them to function along with the rest of the Darwin Core terms.  These documents may already exist, or documents may be created that are similar to the [quick reference guide](http://rs.tdwg.org/dwc/terms/index.htm) and the documents that are used to facilitate IRI dereferencing (such as [dwcterms.rdf](http://code.google.com/p/darwincore/source/browse/trunk/rdf/dwcterms.rdf)).

Linked to this proposal are several [Type 3](http://bioimages.vanderbilt.edu/pages/tdwg-stds-spec.pdf) documents which will not become part of the standard, but which provide [ancillary information](http://code.google.com/p/tdwg-rdf/wiki/DwCAncillary) to support the guide and to provide examples that include terms outside of Darwin Core.  These documents were NOT part of the proposal nor were they the subject of the public review, but are linked here for informational purposes.  The Guide will link to a single stable landing page (whose URL is to be determined) for ancillary documents on the Darwin Core GitHub site (https://github.com/tdwg/dwc). The landing page will contain links the the various ancillary documents.

## Why was a Darwin Core RDF Guide needed? ##

Since Darwin Core terms can currently be dereferenced as RDF, it would seem like a simple matter to adopt the Darwin Core vocabulary for use in RDF.  However, because Darwin Core is a general-purpose vocabulary, many of its terms are defined to facilitate their use in relatively "flat", text-based databases.  In contrast, RDF is by its nature very normalized and often uses IRI references in place of text literals.  Therefore, there is a need to unambiguously distinguish between terms whose values should be text literals and those whose values should be IRI references.  There is also a need for clarity in how a variety of kinds of identifiers should be referenced in RDF.  The RDF Guide addresses each of these issues.

## What are the main features of the DwC RDF Guide? ##
The guide includes an introduction which explains the need for the Guide and describes the major issues that the Guide will address.  It does not explain RDF in detail but provides a brief introduction with examples at the level of the other Guides.  The Implementation section describes the details of how Darwin Core terms should be used consistently in RDF to facilitate the development of applications that can more easily consume DwC data expressed as RDF.  The Term Reference section divides the Darwin Core terms into categories according to how they will be expected to be used.

## What are the important aspects of implementing DwC as RDF which are detailed in the Guide? ##

1. Some existing DwC terms may be used in RDF in a manner very similar to their use in text and XML.

2. The Guide introduces analogues of existing DwC terms in a new namespace _dwciri:_ (`http://rs.tdwg.org/dwc/iri/`) that are intended to be used exclusively with IRI-referenced objects (or blank nodes).

3. The Guide distinguishes some DwC terms as "convenience terms" whose purpose is to make text-based searching simpler.  It introduces several properties intended for use with non-literal objects that would be used in lieu of the convenience terms to link to IRI referenced (non-literal) objects that are further described using RDF.

4. The Guide recognizes that some existing text-based DwC terms cannot adequately be used in RDF and provides references to suggestions for alternative terms or mechanisms for expressing that information as RDF. These suggestions are included in informational [Type 3](http://bioimages.vanderbilt.edu/pages/tdwg-stds-spec.pdf) [web pages](http://code.google.com/p/tdwg-rdf/wiki/DwCAncillary) which will not become part of the standard itself nor be included in the Darwin Core web pages on the TDWG website.

5. The Guide describes how the imported Dublin Core terms should be used as RDF in a manner consistent with their DCMI definitions.

## What does the DwC RDF Guide NOT do? ##
The Guide does not describe a domain model. It does not define ontological relationships among Darwin Core classes.  It does not mint object properties to link the main DwC classes.

## What process has occurred in the ratification of this proposal? ##

Informal discussions on the [TDWG RDF/OWL Task Group](http://code.google.com/p/tdwg-rdf/)'s [email list](http://groups.google.com/group/tdwg-rdf) and at several meetings resulted in sufficient consensus to begin work on an RDF guide.  Members of the RDF and Darwin Core Task Groups volunteered to write a draft document.  Following a 30 day comment period during which the other task group members were invited to read and comment on the draft, the [document was revised](https://docs.google.com/document/d/1OLyVFuveGX1a0Yt6Niok9FfGxkrghii-xlGYhwO8UqE/edit?usp=sharing).  In July 2013, the RDF Task Group recommended that the draft move forward to official submission as an addition to Darwin Core according to the provisions of the Darwin Core Namespace Policy.  In November 2014 the [guide was modified](https://code.google.com/p/tdwg-rdf/wiki/DwcRdfGuideProposalChanges) to make it consistent with the changes that were made to Darwin Core classes on 2014-10-26. Several suggestions for improvement made by task group members were also incorporated into the draft.  The required 30-day public comment period was [initiated on 2014-11-26](http://lists.tdwg.org/pipermail/tdwg-content/2014-November/003384.html). Following the public comment period, the document was modified in response to two issues [Issue 15](https://code.google.com/p/tdwg-rdf/issues/detail?id=15) and [Issue 16](https://code.google.com/p/tdwg-rdf/issues/detail?id=16). There was insufficient consensus to implement a third suggestion [Issue 14](https://code.google.com/p/tdwg-rdf/issues/detail?id=14). The [final draft](DwcRdfGuideFinal.md) was submitted to the TDWG Executive for official ratification to become part of the Darwin Core standard on 2014-12-29.  The Executive Committee formally approved the guide on 2015-03-27.

## Version history ##
[Document showing comments made by the RDF Task Group during its review](https://docs.google.com/document/d/1OLyVFuveGX1a0Yt6Niok9FfGxkrghii-xlGYhwO8UqE/edit)

[Version of proposed addition as recommended by the task group in July 2013](DwcRdfGuideProposal.md)

[Version showing changes made to the July 2013 version after the October 2014 changes to the Darwin Core classes](DwcRdfGuideProposalChanges.md)

[Document summarizing the changes made to the July 2013 version](https://docs.google.com/document/d/153h1_kyfMllKGgfehVLB7ubzRDDaWtnaGHDDwJ6nkwE/edit?usp=sharing)

[Revised version under consideration during 30-day public comment period](DwcRdfGuideProposalRevised.md) (November-December 2014). Changes made as a result of public comment are shown with strikeout for deletions and bold for insertions.  There was one such set of changes [Issue 15](https://code.google.com/p/tdwg-rdf/issues/detail?id=15).  The hyperlinks to a single placeholder ancillary documents page [https://code.google.com/p/tdwg-rdf/wiki/DwCAncillary](DwCAncillary.md) were also made as a response to [Issue 16](https://code.google.com/p/tdwg-rdf/issues/detail?id=16). No changes were made as a result of [Issue 14](https://code.google.com/p/tdwg-rdf/issues/detail?id=14).

[Final draft submitted to TDWG Executive which includes revisions made as a response to the 30 day public comment period.](DwcRdfGuideFinal.md)