# Nature

This is a canonical data source description, `https://data.evotext.org/source/nature`.  
The current `dataSourceVersion` described by this documentation is 1.

**Coverage:** all to vol. 475, no. 7355 \(2011-07-14\)  
**Copyright:** Nature Publishing Group  
**License:** Obtained via direct scrape of NPG website, under contract between NPG and the evoText Project

## How we got it

This data was downloaded directly, using a custom-built Python scraper for the Nature Publishing Group family of journals. \(Scrapers age quickly; I believe that ours is no longer functional as of around 2018.\)

It is not easily possible to update this corpus, or to extend its scope closer to the present.

## Processing

* **PDF OCR to plain text:** ABBYY FineReader 11
  * These are some of the oldest files that we have. They transitioned through, at least, an early version of our Solr XML schema and then the final version of our Solr XML schema. Because the intermediate plain-text files were lost, this final Solr XML was the source of the plain-text used to construct our canonical JSON data. We are not aware of any further errors \(beyond OCR error\) introduced by this process.
* **Basic bibliographic data:** [CrossRef scraping](../technical-details/crossref-scraping.md)
  * Author affiliations were added from [PubMed data](../technical-details/pubmed-scraping.md) when available.
* **Abstracts:** Scraped from two data sources. If the lengths of the two abstracts are less than 20 characters apart from one another \(i.e., they are roughly the same text\), the PubMed abstract was used, as these have fewer formatting errors. Otherwise, the longer abstract was used.
  * Direct web page scraping \(the Dublin Core `dc.description` field, taken from the `<meta>` tag on each canonical article page at [nature.com](https://www.nature.com)\)
  * [PubMed scraping](../technical-details/pubmed-scraping.md)
* **PMIDs, PMCIDs, and PubMed Manuscript IDs:** [PubMed scraping](../technical-details/pubmed-scraping.md)

## Changelog

* **Data Source Version 1:** first parsing of the _Nature_ data into canonical JSON format from our original XML source, adding abstracts, PMIDs, formatted names, etc.

