# PLoS

This is a canonical data source description, `https://data.evotext.org/source/plos`.  
The current `dataSourceVersion` described by this documentation is 1.

**Coverage:** All PLoS-published journals, regularly updated; currently to January 22, 2020  
**Copyright:** Reserved by individual authors; see each article record  
**License:** [CC-BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## How we got it

This data is downloaded directly from PLoS, via their open-source [allofplos Python scraper.](https://github.com/PLOS/allofplos) This scraper not only allows us to download a complete copy of all PLoS journals, it also permits incremental updates, so we regularly refresh our corpus of PLoS content.

## Processing

* **JATS XML to Canonical JSON:** direct parsing from XML
* **PMIDs, PMCIDs, and PubMed Manuscript IDs:** [PubMed scraping](../technical-details/pubmed-scraping.md)
* **Keywords and Tags:** PLoS does not use author-provided keywords. The "subject categories" visible on each article page are saved as tags.

## Changelog

* **Data Source Version 1:** complete rework of our prior PLoS data \(none of which was kept\), from the new 'allofplos' data source in JATS XML

