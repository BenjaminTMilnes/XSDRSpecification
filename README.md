# XSDR Specification

## Copyright

All rights reserved. No part of this repository, or the information contained within it - including all past and future revisions and branches - may be copied or reproduced, be it physically, electronically - including by forking or cloning this repository - or by any other means, without written permission from the copyright owner - B. T. Milnes.



## Contents

+ [Copyright](#copyright)
+ [Version](#version)
+ [Introduction](#introduction)
+ [Document Metadata Elements](#document-metadata-elements)
+ [Text Flow Elements](#text-flow-elements)
+ [Lists](#lists)



## Version

Version 0.1

The master branch of this repository is used for writing the next edition of the XSDR specification. Thus the repository as viewed on the master branch is not the latest finalised version. For finalised versions, see the release branches and tags.



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

+ [&lt;document&gt;](#document)
+ [&lt;style&gt;](#style)
+ [&lt;title&gt;](#title)
+ [&lt;subtitle&gt;](#subtitle)
+ [&lt;abstract&gt;](#abstract)
+ [&lt;keywords&gt;](#keywords)
+ [&lt;authors&gt;](#authors)
+ [&lt;author&gt;](#author)
+ [&lt;first-name&gt;](#first-name)
+ [&lt;last-name&gt;](#last-name)
+ [&lt;name&gt;](#name)
+ [&lt;email-address&gt;](#email-address)



### &lt;document&gt;

The &lt;document&gt; element is the root element for XSDR. There must be exactly one &lt;document&gt; element in an XSDR file, and all other elements must be contained within it.

#### Attributes

|Name       |Synonyms    |Allowed Values |
|-----------|------------|---------------|
|version    |-           |the version of the XSDR specification to which your file conforms, e.g. 0.1 |

#### Example

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
  <abstract>Something, something, something ... dark side.</abstract>
</document>
```



### &lt;style&gt;

Analogous to the HTML &lt;style&gt; element.

The &lt;style&gt; element contains style information for the document. There can be multiple &lt;style&gt; elements in a document. The &lt;style&gt; element must be directly contained by the &lt;document&gt; element.

Styling information for XSDR documents is given in DSS - an analogue of CSS used for paged documents.

#### Attributes

|Name       |Synonyms    |Allowed Values |
|-----------|------------|---------------|
|type       |-           |the styling language that this information is written in; case-insensitive; e.g. "DSS" |

#### Example

```xml
<document version="0.1">
  <style type="DSS">
    h1 {
	  font-height: 20pt;
	  font-weight: bold;
	}
  </style>
</document>
```



### &lt;title&gt;

The &lt;title&gt; element defines the title of the document. Text placed here is not automatically printed anywhere on any of the pages of the document.

The &lt;title&gt; element should be directly contained by the &lt;document&gt; element, and it may not contain any formatting tags such as bold or italic font tags.

#### Example

```xml
<document version="0.1">
  <title>XSDR Specification</title>
</document>
```



### &lt;subtitle&gt;

The &lt;subtitle&gt; element defines the subtitle of the document. Text placed here is not automatically printed anywhere on any of the pages of the document.

The &lt;subtitle&gt; element should be directly contained by the &lt;document&gt; element, and it may not contain any formatting tags such as bold or italic font tags.

The subtitle element is optional, and whether and how you choose to split text between the title and subtitle elements is up to you.

#### Example

```xml
<document version="0.1">
  <title>XSDR Specification</title>
  <subtitle>Version 0.1</subtitle>
</document>
```



### &lt;abstract&gt;

The &lt;abstract&gt; element defines the abstract for the document. Text placed in here is not automatically printed anywhere on any of the pages of the document.

#### Example

```xml
<document version="0.1">
  <abstract>Something, something, something ... dark side.</abstract>
</document>
```



### &lt;keywords&gt;

The &lt;keywords&gt; element is used to give a set of keywords relevant to the document. Text placed here is not automatically printed anywhere on any of the pages of the document.

The keywords should be a list of comma-separated text strings.

#### Example

```xml
<document version="0.1">
  <keywords>delta baryon, pion, Tokai-Kamioka, photon</keywords>
</document>
```



### &lt;authors&gt;

The &lt;authors&gt; is a container element for &lt;author&gt; elements. It should be contained within the main &lt;document&gt; element. There should only be one &lt;authors&gt; element per document.

#### Example

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

#### Example

```xml
<authors>
  <author>
    <first-name>Benjamin</first-name>
    <last-name>Milnes</last-name>
    <email-address>b.t.milnes@example.com</email-address>
  </author>
</authors>
```



### &lt;first-name&gt;

Synonyms: &lt;fn&gt;

The &lt;first-name&gt; element defines the first name of an author. It must be contained by an &lt;author&gt; element. It should not include any font-styling elements, such as italic or bold font elements.



### &lt;last-name&gt;

Synonyms: &lt;ln&gt;

The &lt;last-name&gt; element defines the last name of an author. It must be contained by an &lt;author&gt; element. It should not include any font-styling elements, such as italic or bold font elements.



### &lt;name&gt;

The &lt;name&gt; element defines the name of an author. It can be used as an alternative to specifying the first and last name of an author separately. If the &lt;name&gt; element is given, any information in the &lt;first-name&gt; and &lt;last-name&gt; elements for that author is ignored.



### &lt;email-address&gt;

Synonyms: &lt;ea&gt;

The &lt;email-address&gt; element defines the email address of an author. It must be contained within an &lt;author&gt; element.



## Text Flow Elements

+ [&lt;paragraph&gt;](#paragraph)
+ [&lt;line-break&gt;](#line-break)



### &lt;paragraph&gt;

Synonyms: &lt;p&gt;

Analogous to the HTML &lt;p&gt; element.

The &lt;paragraph&gt; element defines a textual paragraph within the document.

#### Example

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

#### Example

```xml
<p>
  Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
  <lb />
  Grumpy Wizards make toxic brew for the Evil Queen and Jack.
</p>
```



## Lists

+ [&lt;ordered-list&gt;](#ordered-list)
+ [&lt;unordered-list&gt;](#unordered-list)
+ [&lt;list-item&gt;](#list-item)



### &lt;ordered-list&gt;

Synonyms: &lt;ol&gt;

Analogous to the HTML &lt;ol&gt; element. It works in the same way

The &lt;ordered-list&gt; element defines a numbered list of items.

#### Example

```xml
<ol>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ol>
```



### &lt;unordered-list&gt;

Synonyms: &lt;ul&gt;

Analogous to the HTML &lt;ul&gt; element. It works in the same way.

The &lt;unordered-list&gt; element defines a bulleted list of items.

#### Example

```xml
<ul>
  <li>Item</li>
  <li>Item</li>
  <li>Item</li>
</ul>
```



### &lt;list-item&gt;

Synonyms: &lt;li&gt;

Analogous to the HTML &lt;li&gt; element. It works in the same way.

The &lt;list-item&gt; element defines an item in an ordered or unordered list.

#### Example

```xml
<ol>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ol>

<ul>
  <li>Item</li>
  <li>Item</li>
  <li>Item</li>
</ul>
```
