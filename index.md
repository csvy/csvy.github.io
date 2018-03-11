---
layout: index
---
# Welcome to CSVY.
This page describe the specs of yaml frontmatter for csv file format.
The main goals of the format are extreme simplicity and readability.

Because for data human's curators from no-data, CSV, metadata+CSV to Semi-structured data, the technological gap is too large. A simple file format to add metadata to the existing datasets is needed. [JSON](https://en.wikipedia.org/wiki/JSON) is very cryptic for humans, but [YAML](https://en.wikipedia.org/wiki/YAML) can do the job as it can be easily read both by humans and softwares.

## Based on Tabular Data Resource
There are important initiatives, like [Tabular Data Resource](http://frictionlessdata.io/specs/tabular-data-resource/) which it plans to use (json + csv), but most are meant to be published and read by machines.

_CSVY is a simple container of a Tabular Data Resource_, where the (Metadata+Schema) are translated from JSON to YAML and put in the YAML frontmatter part of the file, after the YAML frontmatter part is the Data part stored using the [CSV Dialect](http://frictionlessdata.io/specs/csv-dialect/) Description Format.

### YAML Header delimiter
A YAML metadata block is a valid YAML object, delimited by a line of three hyphens `---` at the top and a line of three hyphens `---` or three dots `...` at the bottom.

### Defining the Table Schema
Use the [Table Schema](https://specs.frictionlessdata.io/table-schema/), it's important to know that the CSVY format is designed to store only one dataset per file.
```yaml
---
profile: tabular-data-resource
name: my-dataset
path: https://raw.githubusercontent.com/csvy/csvy.github.io/master/examples/example.csvy
title: Example file of csvy 
description: Show a csvy sample file.
format: csvy
mediatype: text/vnd.yaml
encoding: utf-8
schema:
  fields:
  - name: var1
    type: string
  - name: var2
    type: integer
  - name: var3
    type: number
dialect:
  csvddfVersion: 1.0
  delimiter: ","
  doubleQuote: false
  lineTerminator: "\r\n"
  quoteChar: "\""
  skipInitialSpace: true
  header: true
sources:
- title: The csvy specifications
  path: http://csvy.org/
  email: ''
licenses:
- name: CC-BY-4.0
  title: Creative Commons Attribution 4.0
  path: https://creativecommons.org/licenses/by/4.0/
---
var1,var2,var3
A,1,2.0
B,3,4.3
```
### Libraries supporting CSVY

* R: [csvy](https://cran.r-project.org/package=csvy) using `read_csvy()` and `write_csvy()
* R: [rio](https://cran.r-project.org/package=rio) using `import()` and `export()` (supported provided by the csvy package)

### Backwards Compatibility

For backward compatibility you can always add to your [data.csv](https://raw.githubusercontent.com/csvy/csvy.github.io/master/examples/data.csv) a [data.yml](https://raw.githubusercontent.com/csvy/csvy.github.io/master/examples/data.yml) metadata file, the next step when there is proper implementation make a single file container, [data.csvy](https://raw.githubusercontent.com/csvy/csvy.github.io/master/examples/data.csvy) will not be a problem at all.

Parser support for skipping multiple lines in the header (which would contain the YAML), and for comment lines (lines starting with `#`). Based on [CSV Parser Notes](https://github.com/hubgit/csvw/wiki/CSV-Parser-Notes) by [@hubgit](https://github.com/hubgit).

Language  | Parser          | Skip lines | Comment lines | Comments
----------| --------------- | ---------- | ------------- | --------
Excel Mac |                 | yes        | no            |
Python    | pandas.read_csv | yes        | yes           |
R         | read.table      | yes        | yes           |
Ruby      | csv.read        | no         | yes           | skip lines via regex

### Related Projects

- [CSVW](http://www.w3.org/2013/csvw/wiki/Main_Page) (CSV on the Web)
- [Tabular Data Package](http://data.okfn.org/doc/tabular-data-package)
- [ARFF](https://weka.wikispaces.com/ARFF+(stable+version)) (Attribute-Relation File Format)

### Authors and Contributors

- [Javier Rovegno](https://github.com/jrovegno)
- [Martin Fenner](https://github.com/mfenner)

### Support or Contact

Use [Github Issues](https://github.com/csvy/csvy.github.io/issues).

### References

- [RFC documents the format used for Comma-Separated Values (CSV) RFC4180](https://tools.ietf.org/html/rfc4180)
- [Model for Tabular Data and Metadata on the Web](http://www.w3.org/TR/tabular-data-model/)
- [Front Matter](http://jekyllrb.com/docs/frontmatter/)
- [Data Package](http://frictionlessdata.io/data-packages/)
- [Tabular Data Packages](http://frictionlessdata.io/guides/tabular-data-package/)
- [Table Schema](https://specs.frictionlessdata.io/table-schema/)
- [Okfn Tools](http://frictionlessdata.io/tools/)
- [Json to Yaml converter](https://www.json2yaml.com/)
- [Codebeautify yaml  to (json/xml/csv)](http://codebeautify.org/yaml-to-json-xml-csv)
- [Is there a yaml front matter standard validator?](http://stackoverflow.com/questions/27838730/is-there-a-yaml-front-matter-standard-validator)
- [Add YAML front matter block support for pandas.io.parsers.read_csv](https://github.com/pydata/pandas/issues/9613)
- [Allow custom metadata to be attached to panel/df/series](https://github.com/pydata/pandas/issues/2485)
- [Using YAML frontmatter with CSV](http://blog.datacite.org/using-yaml-frontmatter-with-csv/)
- [Pandoc Yaml Metadata Block](http://pandoc.org/MANUAL.html#extension-yaml_metadata_block)
