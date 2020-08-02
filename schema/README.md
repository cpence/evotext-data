---
description: The format for our canonical JSON data storage
---

# Canonical JSON Schema

This is a canonical schema description, `https://data.sciveyor.com/schema`.  
The current `version` described by this documentation is 5.

All of our data at rest are transformed into a canonical JSON format that we use to normalize them and make them easier to process at scale into other kinds of required formats.

## Current Schema

```javascript
{
    "schema": "https://data.sciveyor.com/schema",
    "version": 5,

    "id": "any string ID, must be unique across the entire corpus",
    "doi": "10.1234/5678 (should include if available)",
    "externalIds": [
        "type:value",
        "scopus:1234",
        "pmid:1234",
        "...:..."
    ],
    
    "license": "short, human-readable form of the document license",
    "licenseUrl": "URL to further information about licensing terms",
    
    "dataSource": "short, human-readable explanation of the source of this data",
    "dataSourceUrl": "url of the form https://data.sciveyor.com/source/asdf",
    "dataSourceVersion": 1,
    
    "type": "article",
    
    "title": "title of article",
    "authors": [
        {
            "name": "name in natural First Last order",
            "first": "if available",
            "middle": "a parsed version",
            "last": "of the name",
            "prefix": "Dr. Prof.",
            "suffix": "IV",
            "affiliation": "free-form data",
            "externalIds": [
                "type:value",
                "orcid:0001-1234-1234-1234",
                "researcherid:A-1234-5678"
            ]
        },
        { "name": "further authors" },
        { "name": "only the name field is mandatory" }
    ],

    "date": "date of canonical publication (see below)",
    "dateElectronic": "date of first electronic publication",
    "dateAccepted": "date the paper was accepted",
    "dateReceived": "date the paper was received",

    "journal": "journal in which article is published",
    "volume": "volume number",
    "number": "issue number",
    "pages": "page range of article (prefer format xxx-yyy)",
    
    "keywords": ["array", "of", "keywords", "if", "available"],
    "tags": ["see", "below"],
    
    "abstract": "abstract of article, if available",
    
    "fullText": "full text of article"
}
```

A few notes on this format:

* The `schema` parameter is the URL for this page, containing the schema definition.
* The `version` parameter is the _schema version,_ not the document version. It is currently 5. It will in general not be read by consumers of the data, but allows for processing scripts to easily update from older to newer versions of canonical JSON.
* The `id` parameter must be unique across the corpus. If a DOI is available, prefer the ID form `"doi:10.1234/5678"`, but if not, anything unique can be used. Early versions of evoText often used an SHA1 hash of the article PDF file, for example.
* The `externalIds` value allows us to store an extensible list of IDs of other sorts, such as PubMed or Scopus identifiers. [A list of all currently known externalId types can be found here,](external-ids.md) though this should not be taken as exhaustive. All `externalIds` values must be of the form `prefix:identifier`, with everything before the first colon constituting the prefix, and everything after constituting the ID.
* The `dataSourceUrl` points to a URL to a particular data source description. [See more information about them here.](data-source-urls.md)
* The `dataSourceVersion` parameter is the _version of all files from this data source,_ and represents which generation of each set of data you are dealing with. It is a data-source-specific parameter, and its possible values will be defined on the page for each data source description. It will also be incremented when new articles are added to the corpus from the same data source, providing a way to indicate and document that article coverage has changed.
* The `type` field is currently always set to "article." This field is reserved for future dataset expansion. \(We have active plans to add preprints, which will be marked here.\)
* The `authors` are stored as an array of documents.
  * These _must include_ the `name` property, which is the full, unformatted name of the author as it appears in the original source.
  * They _may_ include the other, parsed properties as listed in the schema here.
  * The `affiliation` property is so diverse in the wild that we place no restrictions on how it may appear in final data.
  * The `externalIds` property stores various author global identifier values. Again, [see the list of externalId types here.](external-ids.md) All `externalIds` values must be of the form `prefix:identifier`, with everything before the first colon constituting the prefix, and everything after constituting the ID.
* All of the `date` parameters are stored as strings, although it is assumed that they will satisfy ISO 8601 format. Note that `"yyyy"`, `"yyyy-mm"`, and `"yyyy-mm-dd"` all satisfy ISO 8601. If a time is included, strongly prefer UTC time without timezone.
  * The `date` field corresponds to the "canonical publication date" of the document. If the document appeared in a print journal, this is a print publication date. Otherwise, this is an online, electronic publication date.
  * The `dateElectronic` field is the date at which the document appeared online. Note that this field need not be included if it is identical to `date`.
  * The `dateAccepted` and `dateReceived` contain the dates when the document was received and accepted by a journal during peer review. \(Note that if these fields are absent, this does _not_ automatically entail that the document was not peer reviewed.\)
* The `keywords` field includes only keywords, as intentionally selected by the authors \(no automatically or algorithmically generated keyword or area tags\).
* The `tags` field includes all other, possibly automatically generated, "area" or "domain" or "subject" categorizations that might have been available from journals. No data quality guarantee is possible for these, as they are wildly variable depending on publisher data. See the pages for each data source for more information about what tags have been included in that dataset.
* All other fields are reasonably self-explanatory, and all are strings. While it might be nice for volume or number to be integers, for example, each of these values has examples in the wild where rogue data entails that string representations are required \(for instance, electronic-only "page numbers" of the format "e123", or volume numbers of the form "1 Suppl."\). It's the responsibility of consumers to parse those fields into other representations if required.

## Changelog

* **Schema Version 5, 2020-08-02:** Rebrand to Sciveyor, changing the schema and dataSource URLs.
* **Schema Version 4, 2020-06-19:** Rename the "year" field to "date" and changed its format from a year to an ISO 8601 date. Add the "dateElectronic", "dateAccepted", and "dateReceived" fields.
* **Schema Version 3, 2019-12-17:** Add "type" field for documents, currently always set to "article". Convert "externalIds" to prefixed array rather than dictionary. Add "externalIds" array for authors. Add "keywords" and "tags".
* **Schema Version 2, 2019-06-25:** Add internal schema URL and version parameter, data source URLs, and data source versions. Reworked authors field to be an array of documents rather than strings, including parsed representations and affiliations. Added support for external IDs. Added abstract field.
* **Schema Version 1, 2019-04-12:** Initial version of at-rest JSON schema, developed for MongoDB usage with rletters-go.

