About This Documentation
=========================
This documentation was generated using Widoco and customized for the **CFC Ontology (Circular Future Cities Material Passport Ontology)** project. Widoco integrates existing tools to produce enriched, modular ontology documentation.

Features used for CFC Ontology include:
* Modular separation of HTML sections, making updates and maintenance easier.
* Automatic RDFa annotation for semantic enrichment.
* Provenance documentation in W3C PROV-O format, recording vocabulary evolution.
* Extraction of metadata from the ontology and enhancement through `widoco.conf`.
* Guidelines and templates for structured documentation of ontology structure, usage, and references.

Directory structure:
|
|- `provenance/` — Contains metadata on how the documentation was generated (HTML and RDF).
|- `resources/` — Icons, style sheets, and related visualization files.
|- `sections/` — Independently editable HTML fragments for each documentation block (e.g., abstract, introduction, cross-reference).

Customizing Ontology Metadata
=============================
The `widoco.conf` file enhances the generated HTML with citation metadata, licensing icons, and versioning. It is populated using the ontology’s RDF metadata and can be manually refined for accuracy and completeness.

Local Viewing Considerations
============================
Widoco output is an HTML file set. For proper local viewing, Firefox or Internet Explorer are recommended. Chrome blocks local `XMLHttpRequest` by default; to view locally in Chrome, use one of the following:

* Serve via a local server or Dropbox public URL
* Or launch Chrome with file access enabled:

  - (Windows) `chrome.exe --allow-file-access-from-files`
  - (macOS) `open /Applications/Google\ Chrome.app/ --args --allow-file-access-from-files`
  - (Linux) `/usr/bin/google-chrome --allow-file-access-from-files`

For issues with Widoco, visit: https://github.com/dgarijo/Widoco