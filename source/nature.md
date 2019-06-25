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
* _Intermediate file formats for_ Nature _have since been lost due to poor data management practices. The following are best-guess reconstructive hypotheses._
* **Bibliographic data:** CrossRef DOI scraping
* The files transitioned through, at least, an early version of our Solr XML schema, and then the final version of our Solr XML schema. Because the intermediate plain-text files were lost, this final Solr XML was the source of the plain-text used to construct our canonical JSON data.

## Changelog

* **Data Source Version 1:** first parsing of the _Nature_ data into canonical JSON format from our original XML source.

