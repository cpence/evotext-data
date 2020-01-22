# NLM XML Parsing

_Note: We do not currently have any text which is incoming in NLM-XML format, but this workflow is extremely useful to extract full text from, for example, the PubMed Open Access Subset corpus. We are archiving this workflow here in case it becomes useful in the future._

Lots of Open Access content is provided in the [National Library of Medicine Journal Publishing DTD XML format.](http://dtd.nlm.nih.gov/publishing/) Here is a collection of standardized documentation about how to get NLM XML format articles into the evoText database.

Note that when `$EVOTEXT_SCRIPTS` is mentioned in the below, this refers to a checked-out copy of the [evoText parsing script repository](https://github.com/cpence/evotext).

### Quick Workflow

```text
. $EVOTEXT_SCRIPTS/xslt/dtd/add_catalog

# If the source is a version of the NLM DTD less than 3:
mkdir v3
xsltproc --output v3/<file>.xml \\
    $EVOTEXT_SCRIPTS/xslt/nlm_to_v3/2publishing3.xsl <file>.xml
rm *.xml
mv v3/*.xml .
rmdir v3
# Archive these v3 XML files

xsltproc --output <file>.html \\
  $EVOTEXT_SCRIPTS/xslt/nlm_html_modified.xsl <file>_v3.xml
$EVOTEXT_SCRIPTS/parse_html_to_txt $file.html > $file.txt
# no script currently available for NLM XML to JSON!
```

### Set Path to Local DTDs

We have a copy of the NLM publishing DTDs included in the evotext scripts repository, and you need to enable its included XML catalog for that copy to work. \(If you don't, you'll go out over the network and fetch a DTD for **every** document you process.\) To add the catalog to your source path \(which actually sets an environment variable\), source the following bash script:

```text
. $EVOTEXT_SCRIPTS/xslt/dtd/add_catalog
```

### Convert to NLM DTD v3

The first step is to convert to a uniform baseline of the current \(3.0\) version of the NLM DTD. There's a set of XSLT stylesheets available to do this at the [NLM Tools website,](http://dtd.nlm.nih.gov/tools/tools.html) and we've put a copy of those XSLT files in the scripts repository. To transform with these XSLT files and `xsltproc`, you also need the DTD files for the versions of the publishing tag set that are in use. The 2.0 and 3.0 versions \(and possibly more\) are also available in the repo.

To make this conversion, apply the XSLT file using `xsltproc`:

```text
xsltproc --output <file>_v3.xml \\
    $EVOTEXT_SCRIPTS/xslt/nlm_to_v3/2publishing3.xsl <file>.xml
```

### Convert to HTML

The next step is to convert the XML files to HTML. For this, we begin with the [NLM's provided XSLT file for converting to publication-quality HTML](http://dtd.nlm.nih.gov/tools/tools.html). We've created a modified version of this stylesheet that outputs no metadata or citation references into the output file.

Similar to the above, we convert with:

```text
xsltproc --output <file>.html \\
    $EVOTEXT_SCRIPTS/xslt/nlm_html_modified.xsl <file>_v3.xml
```

### Convert to Plain Text

Next, we convert the article to plain text, using a modified version of [Aaron Swartz's html2text Python script](https://github.com/aaronsw/html2text). This conversion is:

```text
$EVOTEXT_SCRIPTS/parse_html_to_txt $file.html > $file.txt
```

### Extract Metadata

For the moment, because we have no documents incoming in this format, we have not created an updated parsing script that extracts metadata from this file format. This document will be updated if we write one.

