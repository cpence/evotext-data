# Nature

This is a canonical data source description, `https://data.evotext.org/source/nature`.  
The current `dataSourceVersion` described by this documentation is 4. The `dataSource` name for this data is either `Nature Publishing Group` \(for our initial PDFs obtained under license with NPG, publication dates prior to 2011-07-04\), or `Springer Nature` \(for all others\).

**Coverage:** all to vol. 475, no. 7355 \(2011-07-14\)  
**Copyright:** Springer Nature  
**License:** [Springer Nature TDM Policy](https://www.springernature.com/gp/researchers/text-and-data-mining)

## How we got it

This data was downloaded directly, using a custom-built Python scraper for the Nature Publishing Group family of journals. \(Scrapers age quickly; I believe that ours is no longer functional as of around 2018.\)

As our data is now covered by the Springer Nature TDM Policy \(since 2015\), we can now update this corpus from 2011 to the present. We have yet to do so, but hope to implement a workflow for this very soon.

## Processing

* **PDF OCR to plain text:** ABBYY FineReader 11
  * The older portions of _Nature_ \(from 1869–mid-2011\) are some of the first files we obtained for the project. They transitioned through, at least, an early version of our Solr XML schema and then the final version of our Solr XML schema. Because the intermediate plain-text files were lost, this final Solr XML was the source of the plain-text used to construct our canonical JSON data. We are not aware of any further errors \(beyond OCR error\) introduced by this process.
* **Basic bibliographic data:** [CrossRef scraping](../technical-details/crossref-scraping.md) \(for articles before mid-2011\)
  * Author affiliations as well as publication dates were added from [PubMed data](../technical-details/pubmed-scraping.md) when available.
* **Abstracts:** Scraped from two data sources. If the lengths of the two abstracts are less than 20 characters apart from one another \(i.e., they are roughly the same text\), the PubMed abstract was used, as these have fewer formatting errors. Otherwise, the longer abstract was used.
  * Direct web page scraping \(the Dublin Core `dc.description` field, taken from the `<meta>` tag on each canonical article page at [nature.com](https://www.nature.com)\)
  * [PubMed scraping](../technical-details/pubmed-scraping.md)
* **PMIDs, PMCIDs, and PubMed Manuscript IDs:** [PubMed scraping](../technical-details/pubmed-scraping.md)
* **Keywords and Tags:** No keywords are currently used by _Nature,_ and no tags were extracted from the _Nature_ bibliographic data.

## Changelog

* **Data Source Version 4 \(2020-07-21\):** Upgraded to JSON schema v4, adding `date`, `dateElectronic`, `dateReceived`, and `dateAccepted`.
* **Data Source Version 3 \(2020-02-05\):** Empty`externalIds` and occasional empty `authors` values were detected. These have been removed.
* **Data Source Version 2 \(2020-01-23\):** A bug was detected in the parsing of our PMCID, PMMID, and PMID values. The bug was fixed, and we've re-run the PubMed extraction against the entire corpus to provide correct values for this metadata.
* **Data Source Version 1:** First parsing of the _Nature_ data into canonical JSON format from our original XML source, adding abstracts, PMIDs, formatted names, etc.

