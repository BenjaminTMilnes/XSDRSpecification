# XSDR Specification

## Copyright

All rights reserved. No part of this repository, or the information contained within it - including all past and future revisions and branches - may be copied or reproduced, be it physically, electronically - including by forking or cloning this repository - or by any other means, without written permission from the copyright owner - B. T. Milnes.

## Introduction

One of the most popular tools for writing and formatting scientific papers is LaTeX - an extension of the TeX typesetting system. LaTeX makes it easy to format scientific documents, by deciding on many aspects of the format, style, and layout itself. LaTeX can also elegantly typeset mathematics, which is essential for a number of fields of study.

However, LaTeX has a number of issues. As a syntax, it has a number of inconsistencies that make it unpredictable, which gives it a steep learning curve. And while the style and format that LaTeX uses by default is good for certain types of document, for others it isn't, and the workarounds for this are lengthy and clumsy.

XSDR is intended to be an alternative to LaTeX as a document layout and formatting syntax. It is an XML specification. It uses very clear, regular, predictable syntax to describe the contents of a printable, paged document. It has a number of superficial similarities to HTML.

This repository just holds the specification for XSDR - it does not contain an XSDR compiler.

### Why not just use HTML?

XSDR has a number of similarities to HTML - paragraph and heading tags, line break tags - and HTML is already used by a number of people to write scientific documents, so why not just use HTML, and compile HTML into PDF files?

HTML is designed for the web, where there is no concept of a document comprised of multiple pages, with each page a specific, physical size. HTML has no concept of page breaks, page headers and footers, contents tables, and in-line citations. There are easy ways to work around this in HTML (for example, a page break could be defined by <div class="page-break"></div>, and then simply interpreted by the compiler), but they would be no simpler than just having a dedicated XML specification for printed documents (in XSDR, a page break is defined by <page-break /> or even just <pb />).


