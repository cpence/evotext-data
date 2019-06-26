---
description: The format for our canonical JSON data storage
---

# Canonical JSON Schema

This is a canonical schema description, `https://data.evotext.org/schema`.  
The current `version` described by this documentation is 2.

All of our data at rest are transformed into a canonical JSON schema that we can use in order to normalize them and make them easier to process at scale into other kinds of required formats.

## Current Schema

```javascript
{
    "schema": "https://data.evotext.org/schema",
    "version": 2,

    "id": "any string ID, must be unique across the entire corpus",
    "doi": "10.1234/5678 (should include if available)",
    
    "license": "short, human-readable form of the document license",
    "licenseUrl": "URL to further information about licensing terms",
    
    "dataSource": "short, human-readable explanation of the source of this data",
    "dataSourceUrl": "url of the form https://data.evotext.org/source/asdf",
    "dataSourceVersion": 1,
    
    "title": "title of article",
    "authors": [
        "array of authors",
        "each name stored in natural First Last order"
    ],
    "journal": "journal in which article is published",
    "year": "year of publication",
    "volume": "volume number",
    "number": "issue number",
    "pages": "page range of article (prefer format xxx-yyy)",
    
    "fullText": "full text of article"
}
```

A few notes on this format:

* The `schema` parameter is the URL for this page, containing the schema definition.
* The `version` parameter is the _schema version,_ not the document version. It is currently 2. It will in general not be read by consumers of the data, but allows for processing scripts to easily update from older to newer versions of canonical JSON.
* The `id` parameter must be unique across the corpus. If a DOI is available, prefer the ID form `"doi:10.1234/5678"`, but if not, anything unique can be used. Data coming from early versions of evoText often used an SHA1 hash of the article PDF file.
* The `dataSourceUrl` points to a URL to a particular data source description. [See more information about them here.](data-source-urls.md)
* The `dataSourceVersion` parameter is the _version of all files from this data source,_ and represents which generation of each set of data you are dealing with. It is a data-source-specific parameter, and its possible values will be defined on the page for each data source description.
* All other fields are reasonably self-explanatory, and all are strings. While it might be nice for years to be of date format, or for volume or number to be integers, each of these values has examples in the wild where rogue data entails that string representations are required \(for instance, electronic-only "page numbers" of the format "e123", or volume numbers of the form "1 Suppl."\). It's the responsibility of consumers to parse those fields into other representations if required.

## Changelog

* **Schema Version 2, 2019-06-25:** Add internal schema URL and version parameter, data source URLs, and data source versions.
* **Schema Version 1, 2019-04-12:** Initial version of at-rest JSON schema, developed for MongoDB usage with rletters-go.

