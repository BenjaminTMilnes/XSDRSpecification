# XSDR Specification

## Copyright

All rights reserved. No part of this repository, or the information contained within it - including all past and future revisions and branches - may be copied or reproduced, be it physically, electronically - including by forking or cloning this repository - or by any other means, without written permission from the copyright owner - B. T. Milnes.

## Version

Version 0.1

## Introduction

One of the most popular tools for writing and formatting scientific papers is LaTeX - an extension of the TeX typesetting system. LaTeX makes it easy to format scientific documents, by deciding on many aspects of the format, style, and layout itself. LaTeX can also elegantly typeset mathematics, which is essential for a number of fields of study.

However, LaTeX has a number of issues. As a syntax, it has a number of inconsistencies that make it unpredictable, which gives it a steep learning curve. And while the style and format that LaTeX uses by default is good for certain types of document, for others it isn't, and the workarounds for this are lengthy and clumsy.

XSDR is intended to be an alternative to LaTeX as a document layout and formatting syntax. It is an XML specification. It uses very clear, regular, predictable syntax to describe the contents of a printable, paged document. It has a number of superficial similarities to HTML.

This repository just holds the specification for XSDR - it does not contain an XSDR compiler.

### Why not just use HTML?

XSDR has a number of similarities to HTML - paragraph and heading tags, line break tags - and HTML is already used by a number of people to write scientific documents, so why not just use HTML, and compile HTML into PDF files?

HTML is designed for the web, where there is no concept of a document comprised of multiple pages, with each page a specific, physical size. HTML has no concept of page breaks, page headers and footers, contents tables, and in-line citations. There are easy ways to work around this in HTML (for example, a page break could be defined by &lt;div class="page-break"&gt;&lt;/div&gt;, and then simply interpreted by the compiler), but they would be no simpler than just having a dedicated XML specification for printed documents (in XSDR, a page break is defined by &lt;page-break /&gt; or even just &lt;pb /&gt;).

### Synonyms

XSDR allows a large number of synonyms - element names, attribute names, and attribute values that are semantically identical, and processed in the same way by the compiler. For example, a paragraph can be defined by &lt;paragraph&gt;&lt;/paragraph&gt; tags, but you can also define it using just &lt;p&gt;&lt;/p&gt; tags.

Allowing for synonyms makes XSDR much easier to learn. For example, someone unfamiliar with XSDR, upon seeing a &lt;paragraph&gt; element, would immediately know that it defines a paragraph. But it does not do this at the expense of making it easy to use - having to type &lt;paragraph&gt; for every paragraph would be annoying, thus &lt;p&gt; is allowed.

Synonyms also make XSDR more predictable, and faster to use. It's easier to guess what the name for an element or attribute might be, so you don't have to look it up as often.

## Document Metadata Elements

### &lt;document&gt;

The &lt;document&gt; element is the root element for XSDR. There must be exactly one &lt;document&gt; element in an XSDR file, and all other elements must be contained within it.

```xml
<document version="0.1">
  <authors>
    <author>
      <first-name>Benjamin</first-name>
      <last-name>Milnes</last-name>
      <email-address>b.t.milnes@example.com</email-address>
    </author>
  </authors>
  <title>XSDR Specification</title>
</document>
```

#### Attributes

|Name       |Synonyms    |Allowed Values |
|-----------|------------|---------------|
|version    |-           |the version of the XSDR specification to which your file conforms, e.g. 0.1 |

### &lt;authors&gt;

The &lt;authors&gt; is a container element for &lt;author&gt; elements. It should be contained within the main &lt;document&gt; element. There should only be one &lt;authors&gt; element per document.

```xml
<document>
  <authors>
    <author></author>
    <author></author>
    <author></author>
  </authors>
</document>
```

### &lt;author&gt;

The &lt;author&gt; element is used to define an author of the document. It should be contained within the &lt;authors&gt; element. There can be any number of &lt;author&gt; elements within the &lt;authors&gt; element.

The &lt;author&gt; element can contain a variety of information about the author, including their name, their email address, the institution that they're associated with, the address of their academic department, and so on. Templates and style sheets determine how this information is included in the final printed document or PDF. Additional information about the author can be included here so that if one has the XSDR file for the document, one can identify and contact the author more easily.

```xml
<authors>
  <author>
    <first-name>Benjamin</first-name>
    <last-name>Milnes</last-name>
    <email-address>b.t.milnes@example.com</email-address>
  </author>
</authors>
```


## Text Flow Elements

### &lt;paragraph&gt;

Synonyms: &lt;p&gt;

Analogous to the HTML &lt;p&gt; element.

The &lt;paragraph&gt; element defines a textual paragraph within the document.

```xml
<paragraph>
  Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
</paragraph>
```

Or alternatively:

```xml
<p>
  Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
</p>
```

The &lt;paragraph&gt; element should not be used for sections of text that are not strictly paragraphs. For example, if, in the page template, you want to put the title of the document at the top of every page, you should not contain it within &lt;paragraph&gt; tags, as it is not paragraph text. Instead, use a generic text container element.

### &lt;line-break&gt;

Synonyms: &lt;lb&gt;

Analogous to the HTML &lt;br&gt; element.

The &lt;line-break&gt; defines a point at which in-line elements should begin flowing onto the next line.

```xml
<paragraph>
  Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
  <line-break />
  Grumpy Wizards make toxic brew for the Evil Queen and Jack.
</paragraph>
```

Or alternatively:

```xml
<p>
  Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
  <lb />
  Grumpy Wizards make toxic brew for the Evil Queen and Jack.
</p>
```
