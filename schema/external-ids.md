---
description: A list of known external ID types that currently appear in evoText
---

# External IDs

This page will list all known external ID types that might appear in the `externalIds` value for a document. These are intended to capture the ones we know about, but should _not_ be taken as an exhaustive list. It's better for data integration to keep an ID we don't know that we need, even if it winds up going unused in the long run.

* `pmid`: A PMID value, which is simply a large integer.
* `pmcid`: A PMCID value, which is simply a large integer prefixed by "PMC."
  * Every paper indexed by PubMed should in principle have a PMID value, while only papers that are deposited in PubMed Central \(the full-text open access repository\) have PMCID values.
* `pmmid`: A PubMed Manuscript ID value, which indicates the way in which that manuscript was deposited into PubMed Central.
  * For more on these first three types of values and a tool to manually convert between them \(when possible\), [see this page at PubMed Central](https://www.ncbi.nlm.nih.gov/pmc/pmctopmid/).
* `pii`: A publisher-specific identifier that may or may not follow the [standard PII format](https://en.wikipedia.org/wiki/Publisher_Item_Identifier).
* `scopus`: A Scopus ID value, which is simply a large integer.
* `semanticScholar`: a Semantic Scholar identifier, which is a 40-character hex string.

