<h1>Notes from meeting on 2012-03-30 to discuss use of Darwin Core terms in RDF</h1>

Present: John Wieczorek, John Deck, Paul Morris, Bob Morris, Steve Baskauf (who recorded these notes)

The basic issue which was discussed was that people want to use Darwin Core terms as predicates in RDF, but that the definitions of some terms specify that the values of those terms should be strings and that in cases where there are several values, those values should be concatenated and comma separated.  This works well for flat databases which are text-based and which are not set up to handle more than one value for each property.  However, there are users who would like to repeat a property so that each object represents a single resource, and who would like to provide URI references rather than strings as the objects.  This is essentially `Issue 9` in the TDWG RDF/OWL Task Group issue tracker (http://code.google.com/p/tdwg-rdf/issues/detail?id=9 ) and was raised by gsallen@unb.ca on the Task Group survey ( http://code.google.com/p/tdwg-rdf/wiki/Survey ).

As an example, we considered the term dwc:recordedBy, since this was one of the terms mentioned in the survey response.  We considered an example where collectors of specimen foo   were “J. Smith, R. Rodriguez, et al.”  with _smithURI_ as the URI representing “J. Smith” and _rodriquezURI_ as the URI representing “R. Rodriquez”.  If `dwc:recordedBy` were given a single literal value as suggested in the term definition (http://rs.tdwg.org/dwc/terms/index.htm#recordedBy ) the triple would be:
```
_:foo  dwc:recordedBy  “J. Smith, R. Rodriguez, et al.”
```
Other possible renderings could be
```
_:foo dwc:recordedBy “smithURI, rodriquezURI, et al.”
```
[list, but containing URIs as string literals rather than names](concatenated.md)

```
_:foo dwc:recordedBy “smithURI”
_:foo dwc:recordedBy “rodriquezURI”
_:foo dwc:recordedBy “et al.”
```
[i.e. each entity listed separately, but with the URIs given as string literals]

```
_:foo dwc:recordedBy _:smithURI
_:foo dwc:recordedBy _:rodriquezURI
_:foo dwc:recordedBy “et al.”
```
[i.e. each entity listed separately, but with the objects linked as URI references where possible.]

The question was raised as to what user scenario would require the object to be a URI reference rather than a string, since reasoning could be done based on strings as well as URI references.  However, it would not be possible to further link properties to string objects because those strings could not subsequently serve as subjects of other triples since RDF does not currently allow literal subjects.  It was noted that there was really nothing that would prevent providers from using any of these triple forms and that for some applications it would not really matter.  However, for the benefit of more sophisticated reasoning that one might want to facilitate in the future, having clear usage recommendations would make the development of applications simpler.

One mechanism for introducing clarity into the use of Darwin Core terms as RDF predicates would be to create separate terms which were intended to use with URI references.  The existing terms could be reserved for use with literals which conform to the current term definitions.  The [TDWG TaxonConcept Ontology](http://code.google.com/p/tdwg-ontology/source/browse/trunk/ontology/voc/TaxonConcept.owl) follows this model.  The term `tc:nameString` is designated to have a value which is a string representation of the TaxonName, while the term `tc:hasName` is designated to have a value which is the TaxonName (i.e. the object is a URI reference to an abstract entity which is the name).

There are several mechanisms by which terms intended for use with URI objects could be designated.  One would be to create terms within the existing `dwc:` namespace whose term names were systematic modifications of the existing names.  For example, the version of `dwc:recordedBy` which is intended for use with URI references could be designated as `dwc:recordedByURI`.  Another alternative would be to keep the same term names, but to place them under a different namespace that was understood to contain terms that were intended to be used with URIs.  For example `dwcuri:recordedBy` would be the URI reference analogue of the term intended for use with strings (i.e. `dwc:recordedBy`).

Under the first mechanism, it would be necessary to create new terms in accordance with the Darwin Core namespace policy.  That would have the advantage of maintaining the integrity of a single Darwin Core vocabulary list.  However, it also could be time-consuming and require a significant amount of discussion before the terms could be brought into use.

The second mechanism would have the disadvantage of potentially confusing users who are not aware of the rationale for URI references, since the names of the terms in the new namespace would be the same as the names of the terms in the existing namespace.  However, if the documentation were maintained in a document which was separate from the main Darwin Core vocabulary documentation, it would only be accessed by persons who had an interest in using terms with URI references.  Users who intended to use Darwin Core in the traditional manner could be clearly warned away from the new documentation and directed to the pre-existing Darwin Core terms documentation.  Users who wanted to use the current terms in the current manner would not have to concern themselves with the new namespace and confusion could be minimized.  Another advantage would be that the terms could be created under the new (unofficial) namespace and tested without the necessity of making a commitment to this approach.  If the "second namespace" approach seemed to work, then a recommendation to add those terms (under the new namespace) to a standard (Darwin Core or some new standard) could be pursued at a later time.

Under these scenarios, the example could be marked up as follows:

```
[first mechanism]
_:foo  dwc:recordedBy  “J. Smith, R. Rodriguez, et al.”
_:foo  dwc:recordedByURI  _:smithURI
_:foo  dwc:recordedByURI  _:rodriquezURI
```

```
[second mechanism]
_:foo  dwc:recordedBy  “J. Smith, R. Rodriguez, et al.”
_:foo  dwcuri:recordedBy  _:smithURI
_:foo  dwcuri:recordedBy  _:rodriquezURI
```

In the discussion, it was noted that to some extent, the issues involved in establishing recommendations for using these new types of terms and for clarifying the use of the existing terms as RDF predicates is a social, not technical challenge.  However, in contrast to the case of the terms in the Dublin Core `dcterms:` namespace, where some terms are already used in ways that are at odds with the DC recommendations, creating new URI-reference terms are not as likely to confuse users who are less well-acquainted with RDF because people who are not informed about the new terms would be likely to use the existing terms in RDF with literals anyway (as suggested by the existing term definitions).  So there is no need to "educate" people to stop current “incorrect” practices.

The question was also raised as to whether the new terms could be put in the `dsw:` namespace (`http://purl.org/dsw/`).  That is a possibility if the community feels that is a good idea.