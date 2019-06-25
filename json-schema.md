---
description: The format for our canonical JSON data storage
---

# JSON Schema

All of our data at rest are transformed into a canonical JSON schema that we can use in order to normalize them and make them easier to process at scale into other kinds of required formats.

## Current Schema

```javascript
{
    "id": "any string ID, must be unique across the entire corpus",
    "version": 2,
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

* The `id` parameter must be unique across the corpus. If a DOI is available, prefer the ID form `"doi:10.1234/5678"`, but if not, anything unique can be used. Data coming from early versions of evoText often used an SHA1 hash of the article PDF file.
* The `version` parameter is the _schema version,_ not the document version, and is the only non-string value in the entire schema. It is currently 2. It will in general not be read by consumers of the data, but allows for processing scripts to easily update from older to newer versions of canonical JSON.
* All other fields are reasonably self-explanatory, and all are strings. \(While it might be nice for years to be of date format, or for volume or number to be integers, each of these values has examples in the wild where rogue data entails that string representations are required. It's the responsibility of data consumers to parse those fields into numbers if required.\)

## Changelog

* **Schema Version 2, 2019-06-25:** Add internal schema version parameter
* **Schema Version 1, 2019-04-12:** Initial version of at-rest JSON schema, developed for MongoDB usage with rletters-go.

