---
description: How we fetch metadata from DOIs
---

# Crossref DOI Scraping

Many of our datasets come with DOI information that we must later turn into machine-readable bibliographic data. This can be accomplished using Crossref, the central repository for DOI information \(which is found at [https://doi.org/](https://doi.org/)\). The support on their servers for this access is documented [here](https://support.crossref.org/hc/en-us/articles/213673586-Content-negotiation) and [here](https://crosscite.org/docs.html).

In short, if you query the Crossref server URL for a particular DOI \(e.g., [https://dx.doi.org/10.1038/165387a0](https://dx.doi.org/10.1038/165387a0)\), but set the "Accept" HTTP header to a non-HTML content type, then instead of being served a redirect to the canonical URL for that article, you will get a file representing Crossref's bibliographic information about that article.

For our purposes, we use the content type `application/vnd.citationstyles.csl+json`, which returns data in the form of Citation Style Language JSON. All of the CSL file formats are clearly documented [in their Github repository](https://github.com/citation-style-language/schema), and the CSL JSON reference format in particular is documented [here](https://github.com/citation-style-language/schema/blob/master/csl-data.json). This format can be easily parsed into our canonical JSON.

