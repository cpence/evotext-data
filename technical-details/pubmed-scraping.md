---
description: How we fetch metadata from PubMed
---

# PubMed Scraping

In order to have a more complete collection of article abstracts, as well as unique PMID values for every article in the corpus for which they are known, we query [PubMed](https://www.ncbi.nlm.nih.gov/pubmed/), the central bibliographic database in the biological sciences operated by the US National Institutes of Health, for every article in the corpus.

To do this, we use PubMed's [ESearch and EFetch APIs](https://www.ncbi.nlm.nih.gov/books/NBK25501/). The ESearch API takes a DOI \(which we have for almost every item in our database\), and converts it to a PubMed PMID. We then pass this PMID to the EFetch API, which returns a variety of useful data:

* Standard bibliographic data, including PMID, PMCID, and PubMed Manuscript ID
* Abstract
* Manual article categorization, including lists of chemicals and proteins, as well as [NLM MeSH subject headings](https://www.nlm.nih.gov/mesh/)

This data is highly variable in coverage – very often, in fact, PubMed lacks information for older articles \(the back-catalog of articles published before the database went fully online in 1996 is not very extensive\), and PubMed has absolutely no coverage whatsoever outside of the sciences. We cannot therefore rely on any of the data present here \(this is, for example, why MeSH headings are not present in our [schema](../schema/)\), but they can help to round out our collection for otherwise difficult datasets.

