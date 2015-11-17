# Overall model #

![http://tdwg-rdf.googlecode.com/svn/trunk/file/TDWG_TaxonConceptModel.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/TDWG_TaxonConceptModel.png)

The TaxonConcept model asserts that the species concept can be described by tagging instances of other resources (e.g. images, occurrences, and original descriptions) which provide various perspectives on the taxon.  These instances are tagged using "light-weight tags" that are formed from the species concept URI by adding an appropriate fragment identifier (e.g. "#Image").

Each of the tagged instances is linked to the species concept by dcterm:hasPart (http://purl.org/dc/terms/hasPart).

# Original description component #

![http://tdwg-rdf.googlecode.com/svn/trunk/file/TDWG_TaxonSensu.png](http://tdwg-rdf.googlecode.com/svn/trunk/file/TDWG_TaxonSensu.png)

This diagram shows how resources associated with an original description are linked to the txn:SpeciesOriginalDescription instance.

# Examples #

See http://lod.taxonconcept.org/ses/iuCXz.rdf and http://lod.taxonconcept.org/ses/v6n7p.rdf for examples.

Thanks to Pete DeVries for providing this information.