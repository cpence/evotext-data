---
description: The format for our canonical JSON data storage
---

# Canonical JSON Schema

This is a canonical schema description, `https://data.evotext.org/schema`.  
The current `version` described by this documentation is 2.

All of our data at rest are transformed into a canonical JSON format that we use to normalize them and make them easier to process at scale into other kinds of required formats.

## Current Schema

```javascript
{
    "schema": "https://data.evotext.org/schema",
    "version": 2,

    "id": "any string ID, must be unique across the entire corpus",
    "doi": "10.1234/5678 (should include if available)",
    "externalIds": {
        "type": "value",
        "scopus": "1234",
        "pmid": "1234",
        "...": "..."
    },
    
    "license": "short, human-readable form of the document license",
    "licenseUrl": "URL to further information about licensing terms",
    
    "dataSource": "short, human-readable explanation of the source of this data",
    "dataSourceUrl": "url of the form https://data.evotext.org/source/asdf",
    "dataSourceVersion": 1,
    
    "title": "title of article",
    "authors": [
        { "name": "array of authors" },
        {
            "name": "each name in natural First Last order",
            "first": "if available",
            "middle": "a parsed version",
            "last": "of the name",
            "prefix": "Dr. Prof.",
            "suffix": "IV",
            "affiliation": "free-form data"
        }
    ],
    "journal": "journal in which article is published",
    "year": "year of publication",
    "volume": "volume number",
    "number": "issue number",
    "pages": "page range of article (prefer format xxx-yyy)",
    
    "abstract": "abstract of article, if available",
    
    "fullText": "full text of article"
}
```

A few notes on this format:

* The `schema` parameter is the URL for this page, containing the schema definition.
* The `version` parameter is the _schema version,_ not the document version. It is currently 2. It will in general not be read by consumers of the data, but allows for processing scripts to easily update from older to newer versions of canonical JSON.
* The `id` parameter must be unique across the corpus. If a DOI is available, prefer the ID form `"doi:10.1234/5678"`, but if not, anything unique can be used. Early versions of evoText often used an SHA1 hash of the article PDF file, for example.
* The `externalIds` value allows us to store an extensible list of IDs of other sorts, such as PubMed or Scopus identifiers. [A list of all currently known externalId types can be found here,](external-ids.md) though this should not be taken as exhaustive.
* The `dataSourceUrl` points to a URL to a particular data source description. [See more information about them here.](data-source-urls.md)
* The `dataSourceVersion` parameter is the _version of all files from this data source,_ and represents which generation of each set of data you are dealing with. It is a data-source-specific parameter, and its possible values will be defined on the page for each data source description. It will also be incremented when new articles are added to the corpus from the same data source, providing a way to indicate and document that article coverage has changed.
* The `authors` are stored as an array of documents. These _must include_ the `name` property, which is the full, unformatted name of the author as it appears in the original source. They _may_ include the other, parsed properties as listed in the schema here. The `affiliation` property is so diverse in the wild that we place no restrictions on how it may appear in final data.
* All other fields are reasonably self-explanatory, and all are strings. While it might be nice for years to be of date format, or for volume or number to be integers, each of these values has examples in the wild where rogue data entails that string representations are required \(for instance, electronic-only "page numbers" of the format "e123", or volume numbers of the form "1 Suppl."\). It's the responsibility of consumers to parse those fields into other representations if required.

## Changelog

* **Schema Version 2, 2019-06-25:** Add internal schema URL and version parameter, data source URLs, and data source versions. Reworked authors field to be an array of documents rather than strings, including parsed representations and affiliations. Added support for external IDs. Added abstract field.
* **Schema Version 1, 2019-04-12:** Initial version of at-rest JSON schema, developed for MongoDB usage with rletters-go.

