# XSDR Specification

## Copyright

All rights reserved. No part of this repository, or the information contained within it - including all past and future revisions and branches - may be copied or reproduced, be it physically, electronically - including by forking or cloning this repository - or by any other means, without written permission from the copyright owner - B. T. Milnes.



## Contents

+ [Copyright](#copyright)
+ [Version](#version)
+ [Introduction](#introduction)
+ [Document Metadata Elements](#document-metadata-elements)
+ [Templating](#templating)
+ [Sectioning](#sectioning)
+ [Text Flow Elements](#text-flow-elements)
+ [Lists](#lists)
+ [Images](#images)
+ [Indices and Citations] (#indices-and-citations)
+ [Formatting Elements] (#formatting-elements)
+ [Variables] (#variables)
+ [Other Elements] (#other-elements)



## Version

**Version 0.2**

The master branch of this repository is used for writing the next edition of the XSDR specification. Thus the repository as viewed on the master branch is not the latest finalised version. For finalised versions, see the release branches and tags.



## Introduction

One of the most popular tools for writing and formatting scientific papers is LaTeX - an extension of the TeX typesetting system. LaTeX makes it easy to format scientific documents, by deciding on many aspects of the style and layout itself. LaTeX can also elegantly typeset mathematics, which is essential for a number of fields of study.

However, LaTeX has a number of issues. As a syntax, it has a number of inconsistencies that make it unpredictable, which gives it a steep learning curve. And while the style that LaTeX uses by default is good for certain types of document, for others it isn't, and the workarounds for this are lengthy and clumsy.

XSDR is intended to be an alternative to LaTeX as a document layout and formatting syntax. It is an XML specification. It uses very clear, regular, predictable syntax to describe the contents of a printable, paged document. It has a number of superficial similarities to HTML.

This repository just holds the specification for XSDR - **it does not contain an XSDR compiler**.



### Why not just use HTML?

XSDR has a number of similarities to HTML - paragraph and heading tags, line break tags - and HTML is already used by a number of people to write scientific documents, so why not just use HTML, and compile HTML into PDF files?

HTML is designed for the web, where there is no concept of a document comprised of multiple pages, with each page a specific, physical size. HTML has no concept of page breaks, page headers and footers, contents tables, and in-line citations. There are easy ways to work around this in HTML (for example, a page break could be defined by &lt;div class="page-break"&gt;&lt;/div&gt;, and then simply interpreted by the compiler), but they would be no simpler than just having a dedicated XML specification for printed documents (in XSDR, a page break is defined by &lt;page-break /&gt; or even just &lt;pb /&gt;).



### Synonyms

XSDR allows a large number of **synonyms** - element names, attribute names, and attribute values that are **semantically identical, and processed in the same way by the compiler**. For example, a paragraph can be defined by &lt;paragraph&gt;&lt;/paragraph&gt; tags, but you can also define it using just &lt;p&gt;&lt;/p&gt; tags.

Allowing for synonyms makes XSDR much easier to learn. For example, someone unfamiliar with XSDR, upon seeing a &lt;paragraph&gt; element, would immediately know that it defines a paragraph. But it does not do this at the expense of making it easy to use - having to type &lt;paragraph&gt; for every paragraph would be annoying, thus &lt;p&gt; is allowed.

Synonyms also make XSDR more predictable, and faster to use. It's easier to guess what the name for an element or attribute might be, so you don't have to look it up as often.

#### 'colour' vs. 'color'

As part of the synonyms in XSDR, XSDR compilers will interpret British and American spellings of words identically. For example, you can specify the colour that text should be either with 'font-colour: blue;' or 'font-color: blue;'.

The purpose of this is to reduce the amount of thought that has to go into menial tasks such as altering the colour of text. If you're used to typing 'colour', then you can just type it and it will work, and similarly if you're used to typing 'color'.

This specification document, however, will be written using British standard spellings.



## Document Metadata Elements

+ [&lt;document&gt;](#document)
+ [&lt;style&gt;](#style)
+ [&lt;title&gt;](#title)
+ [&lt;subtitle&gt;](#subtitle)
+ [&lt;abstract&gt;](#abstract)
+ [&lt;keywords&gt;](#keywords)
+ [&lt;publication-date&gt;](#publication-date)
+ [&lt;authors&gt;](#authors)
+ [&lt;author&gt;](#author)
+ [&lt;name&gt;](#name)
+ [&lt;email-address&gt;](#email-address)
+ [&lt;address&gt;](#address)
+ [&lt;website&gt;](#website)



### &lt;document&gt;

The &lt;document&gt; element is the **root element for XSDR**. There must be exactly one &lt;document&gt; element in an XSDR file, and all other elements must be contained within it.

#### Attributes

|Name       |Synonyms    |Allowed Values |
|-----------|------------|---------------|
|version    |-           |the version of the XSDR specification to which your file conforms, e.g. 0.1 |

#### Example

```xml
<document version="0.1">
  <authors>
    <author>
      <name>B. T. Milnes</name>
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

**Styling information for XSDR documents is given in DSS - an analogue of CSS used for paged documents.**

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

The &lt;title&gt; element defines the title of the document. **Text placed here is not automatically printed anywhere on any of the pages of the document.**

The &lt;title&gt; element should be directly contained by the &lt;document&gt; element, and it may not contain any formatting tags such as bold or italic font tags.

#### Example

```xml
<document version="0.1">
  <title>XSDR Specification</title>
</document>
```



### &lt;subtitle&gt;

The &lt;subtitle&gt; element defines the subtitle of the document. **Text placed here is not automatically printed anywhere on any of the pages of the document.**

The &lt;subtitle&gt; element should be directly contained by the &lt;document&gt; element, and it may not contain any formatting tags such as bold or italic font tags.

**The subtitle element is optional**, and whether and how you choose to split text between the title and subtitle elements is up to you.

#### Example

```xml
<document version="0.1">
  <title>XSDR Specification</title>
  <subtitle>Version 0.1</subtitle>
</document>
```



### &lt;abstract&gt;

The &lt;abstract&gt; element defines the abstract for the document. **Text placed in here is not automatically printed anywhere on any of the pages of the document.**

#### Example

```xml
<document version="0.1">
  <abstract>Something, something, something ... dark side.</abstract>
</document>
```



### &lt;keywords&gt;

The &lt;keywords&gt; element is used to give a set of keywords relevant to the document. **Text placed here is not automatically printed anywhere on any of the pages of the document.**

The keywords should be a list of comma-separated text strings.

#### Example

```xml
<document version="0.1">
  <keywords>delta baryon, pion, Tokai-Kamioka, photon</keywords>
</document>
```



### &lt;publication-date&gt;

The &lt;publication-date&gt; element defines the date on which the document was published. If the document is a paper being submitted to a journal, the journal publishing the paper should set this field.

The date should be in the format 'YYYY.MM.DD' - i.e. '2017.10.07'. Hours, minutes, and seconds should not be included.



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
    <name>B. T. Milnes</name>
    <email-address>b.t.milnes@example.com</email-address>
  </author>
</authors>
```



### &lt;name&gt;

The &lt;name&gt; element defines the name of an author.

+ It must be directly contained by an &lt;author&gt; element.
+ It should not include any font-styling elements, such as italic or bold font elements.



### &lt;email-address&gt;

Synonyms: &lt;ea&gt;

The &lt;email-address&gt; element defines the email address of an author.

+ It must be contained within an &lt;author&gt; element.
+ It is optional.



### &lt;address&gt;

The &lt;address&gt; element defines the address of an author or organisation.

+ It must be contained within an &lt;author&gt; element.
+ It is optional.



### &lt;website&gt;

The &lt;website&gt; element defines the website of an author or organisation.

+ It must be contained within an &lt;author&gt; element.
+ There can be multiple &lt;website&gt; elements for each author or organisation.
+ It is optional.



## Templating

Templating is an essential part of XSDR. It allows you to easily apply formatting to a range of pages within your document. It also allows you to place elements on every page within a range of pages, while only defining their content and position once. For example, if you want the page number to appear at the bottom of every page, you would define a page template with the page number variable in the page footer, and then apply that page template to the relevant section of the document.

+ [&lt;templates&gt;](#templates)
+ [&lt;page-template&gt;](#page-template)



### &lt;templates&gt;

All of the templates used within the document are contained within the &lt;templates&gt; element, of which there should only be one in the document, and which usually appears after the metadata, but before the &lt;sections&gt; element.



### &lt;page-template&gt;

The &lt;page-template&gt; element is a special class of template for defining the format of each page within a section of the document. **Use this to define the size and orientation of the page, as well as its margins, and any header and footer content.**

#### Example

```xml
<document>
  <templates>
    <page-template reference="main" style="page-size: a4; inner-margin: 3.0cm;">
      <header>
        <d style="text-alignment: centre;">Book Title</d>
      </header>
      <footer>
        <d style="text-alignment: centre;"><page-number /></d>
      </footer>
    </page-template>
  </templates>
  <sections>
    <section page-template-reference="main">
      <h1>Introduction</h1>
      <p>Grumpy wizards make toxic brew for the Evil Queen and Jack.</p>
    </section>
  </sections>
</document>
```



### &lt;header&gt;

The &lt;header&gt; element is used to define content that should go in the header of each page of a section. The header element can only appear within a page template element - not within the sections directly. The content contained in the header element is copied onto every page of the sections that the page template is applied to, appearing at the top of the page.

#### Example

```xml
<page-template>
  <header>
    <d style="text-alignment: centre;">Book Title</d>
  </header>
</page-template>
```



### &lt;footer&gt;

The &lt;footer&gt; element is similar to the &lt;header&gt; element. It is used to define content that should go in the footer of each page of a section. The footer element can only appear within a page template element - not within the sections directly. The content contained in the footer element is copied onto every page of the sections that the page template is applied to, appearing at the bottom of the page.

#### Example

```xml
<page-template>
  <footer>
    <d style="text-alignment: centre;"><page-number /></d>
  </footer>
</page-template>
```



## Sectioning

An XSDR document is divided into sections. These sections can have meaning within your document - you can define one section for the introduction, another perhaps for experimental results, another for the conclusion. They are also a way of applying different page templates throughout the document. For example, for a book, page numbers are generally not printed on the first few pages - thus this section of the book would have a different page template to the rest.

+ [&lt;sections&gt;](#sections)
+ [&lt;section&gt;](#section)
+ [&lt;page-break&gt;](#page-break)



### &lt;sections&gt;

The &lt;sections&gt; element defines the content of your document. All of the content of your document should be contained within the &lt;sections&gt; element. There may be only one &lt;sections&gt; element per document, and it must be directly contained by the &lt;document&gt; element.

#### Example

```xml
<document>
  <sections>
    <section style="page-size: a4; inner-margin: 3.0cm;">
      <h1>Introduction</h1>
      <p>Grumpy wizards make toxic brew for the Evil Queen and Jack.</p>
    </section>
  </sections>
</document>
```



### &lt;section&gt;

The &lt;section&gt; element defines a section within your document. This might be a title page, the introduction, the index - no constraints are placed on how long or short a section can be, or what is put in it. If your entire document uses one page template, you can make the document have just one section.

**A &lt;section&gt; element cannot contain other &lt;section&gt; elements.**

#### Example

```xml
<document>
  <sections>
    <section style="page-size: a4; inner-margin: 3.0cm;">
	  <h1>Introduction</h1>
	  <p>Grumpy wizards make toxic brew for the Evil Queen and Jack.</p>
	</section>
  </sections>
</document>
```



### &lt;page-break&gt;

Synonyms: &lt;pb&gt;

The &lt;page-break&gt; element indicates that content following it should begin flowing onto the next page, and that the remainder of the current page should be left blank.

If the type attribute is set to 'next-page', then content following the page break element will flow onto the next page. If the type is set to 'even-page', then content following the page break element will flow onto the next even-numbered page, and if the type is set to 'odd-page', then content following the page break element will flow onto the next odd-numbered page.

#### Attributes

|Name       |Synonyms    |Allowed Values |
|-----------|------------|---------------|
|type       |-           |one of: 'next-page', 'even-page', 'odd-page'; the default is 'next-page' |

#### Example

```xml
<section>
  <h1>Grumpy Wizards and their Brews</h1>
  <p>
    Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
  </p>
  <pb />
  <!-- The following text will appear on the next page. -->
  <h1>Grumpy Wizards and their Brews</h1>
  <p>
    Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
  </p>
</section>
```



## Text Flow Elements

+ [&lt;heading1&gt; to &lt;heading10&gt;](#heading1-to-heading10)
+ [&lt;paragraph&gt;](#paragraph)
+ [&lt;line-break&gt;](#line-break)
+ [&lt;division&gt;](#division)



### &lt;heading1&gt; to &lt;heading10&gt;

+ &lt;heading1&gt;
+ &lt;heading2&gt;
+ &lt;heading3&gt;
+ &lt;heading4&gt;
+ &lt;heading5&gt;
+ &lt;heading6&gt;
+ &lt;heading7&gt;
+ &lt;heading8&gt;
+ &lt;heading9&gt;
+ &lt;heading10&gt;

Synonyms: &lt;h1&gt;, &lt;h2&gt;, &lt;h3&gt;, &lt;h4&gt;, &lt;h5&gt;, &lt;h6&gt;, &lt;h7&gt;, &lt;h8&gt;, &lt;h9&gt;, &lt;h10&gt;

Analogous to the HTML elements &lt;h1&gt; to &lt;h6&gt;

The elements &lt;heading1&gt; to &lt;heading10&gt; are used to define headings in your document. &lt;heading1&gt; should be the highest-level heading in your document. If you are writing a book, this is perhaps the part or chapter heading. &lt;heading10&gt; should be the lowest-level heading in your document. The precise meaning of each heading element is not defined in this specification, and is dependent on the type of document you are writing.

#### Example

```xml
<h1>Grumpy Wizards and their Brews</h1>
<p>
  Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
</p>
```



### &lt;paragraph&gt;

Synonyms: &lt;p&gt;

**Analogous to the HTML &lt;p&gt; element.**

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

**Analogous to the HTML &lt;br&gt; element.**

The &lt;line-break&gt; defines a point at which in-line elements should begin flowing onto the next line.

#### Example

```xml
<p>
  Grumpy Wizards make toxic brew for the Evil Queen and Jack. Grumpy Wizards make toxic brew for the Evil Queen and Jack. 
  <lb />
  Grumpy Wizards make toxic brew for the Evil Queen and Jack.
</p>
```



### &lt;division&gt;

Synonyms: &lt;d&gt;

**Analogous to the HTML &lt;div&gt; element.**

The &lt;division&gt; element is a generic block element. It has no semantic meaning within the document. It's main use is for applying formatting to sections that otherwise aren't contained by a particular element. For example, if you wanted to place a textbox on the page with a blue background, and that textbox contained headings, paragraphs, and images, you would put all of the contents of the textbox within a &lt;division&gt; element, and then apply the blue background to the style of the &lt;division&gt; element.

#### Example

```xml
<d style="background-colour: blue; inner-margin: 5mm;">
  <h4>Grumpy Wizards and their Brews</h4>
  <p>Grumpy Wizards make toxic brew for the Evil Queen and Jack.</p>
</d>
```



## Lists

+ [&lt;ordered-list&gt;](#ordered-list)
+ [&lt;unordered-list&gt;](#unordered-list)
+ [&lt;list-item&gt;](#list-item)



### &lt;ordered-list&gt;

Synonyms: &lt;ol&gt;

**Analogous to the HTML &lt;ol&gt; element.**

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

**Analogous to the HTML &lt;ul&gt; element.**

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

**Analogous to the HTML &lt;li&gt; element.**

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



## Images



### &lt;image&gt;

**Analogous to the HTML &lt;img&gt; tag.**

The &lt;image&gt; element includes an external image file in the document at the given location. The image file can be a raster image, such as a PNG or a JPEG, or a vector image, such as an SVG.

It is not essential for an image element to be contained by a figure element, but if you're making a document such as an academic paper or book, then it's a good idea.

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|file||the path to the image file|

#### Example

```xml
<image file="funnycat.png" />
```



### &lt;figure&gt;

**Analogous to the HTML &lt;figure&gt; tag.**

The &lt;figure&gt; element defines a figure in the document. A figure normally contains an image and a caption.

When the XSDR compiler processes the XSDR document, it will give each figure a number, thus there is no need to manually number the figures.

#### Example

```xml
<figure>
	<image file="funnycat.png" />
	<caption>A funny cat</caption>
</figure>
```


### &lt;caption&gt;

The &lt;caption&gt; element defines a caption for a figure or a table. A &lt;caption&gt; element must appear inside a &lt;figure&gt; or &lt;table&gt; element.



## Indices and Citations



### &lt;citation&gt;

Synonyms: &lt;c&gt;

**Analogous to the HTML &lt;cite&gt; element.**

The &lt;citation&gt; element defines an in-line citation.

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|reference|r|any valid bibliographic reference - normally a text string consisting of just letters and numbers|

#### Example

```xml
<p>Winter is coming.<c reference="JonSnow" /></p>
```



### &lt;table-of-contents&gt;

Synonyms: &lt;contents&gt;



### &lt;index-entry&gt;

Synonyms: &lt;ie&gt;

The &lt;index-entry&gt; element defines text that should be referenced in the index of the document.

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|text|the text that will be printed in the index for this entry||
|cross-reference|other items in the index to see||

Example

```xml
<p><index-entry text="Albert Einstein">Einstein</index-entry> said, <q>Imagination is more important than knowledge.</q></p>
```



&lt;index&gt;

The &lt;index&gt; element defines where the index of the document should appear. The index is normally automatically generated from the &lt;index-entry&gt; elements that are throughout the document.



&lt;bibliography&gt;

The &lt;bibliography&gt; element defines where the bibliography should appear in the document. The format attribute can be used to indicate what format the bibliography is in. The bibliography can be written in the BibTeX syntax, or it can be written in XBR - a companion of XSDR for bibliographic data.

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|format||one of 'bibtex', 'xbr'; the format that the bibliography has been written in; the default is 'xbr'|
|order-by||one of 'title', 'author', 'date', 'usage-in-document'; 'usage-in-document' is the default, and orders the items in the bibliography by the order that they are reference in the document|
|reverse-order||either 'true' or 'false'; reverses the order that the items appear in|



## Formatting Elements



### &lt;italic&gt;

Synonyms: &lt;i&gt;

The &lt;italic&gt; element defines italic text.

While for the most part, XSDR follows the principle that the XML should define what the document contains, and the CSS / DSS should define how it looks, the &lt;i&gt;, &lt;b&gt;, &lt;u&gt;, and &lt;s&gt; tags are an exception to this. These tags define italic, bold, underlined, and strikethrough text. These formatting tags are allowed because of how often they need to be used.

For languages that don't use italic or bold fonts, the way that text within these tags is rendered should be in such a way that the implied meaning is the same as the implied meaning of italic or bold text.

#### Example

```xml
<p>This is a <i>really</i> bad example of using italic text.</p>
```


### &lt;bold&gt;

Synonyms: &lt;b&gt;

The &lt;bold&gt; element defines a section of bold text.



### &lt;underline&gt;

Synonyms: &lt;u&gt;

The &lt;underline&gt; element defines a section of underlined text.



### &lt;strikethrough&gt;

Synonyms: &lt;s&gt;



## Variables

A variable in XSDR is an element that inserts text or a template at a given position which may be different depending on the context of the document at that point. For example, the &lt;page-number&gt; element is a variable - it inserts the page number as a text string into the document at that point. Whatever page that page number element ends up being on in the final rendered document is what the page number will show.

There are lots of different variables. They can be used in the main sections of the document, as well as in templates. In the future it may also be possible to define your own variables.



### &lt;variable&gt;

Synonyms: &lt;v&gt;

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|name||anything; defines the name of the variable that will be used to reference it in other parts of the document|






### &lt;page-number&gt;

Synonyms: &lt;pn&gt;



### &lt;section-number&gt;

Synonyms: &lt;sn&gt;



### &lt;page-count&gt;

Synonyms: &lt;pc&gt;



### &lt;section-count&gt;

Synonyms: &lt;sc&gt;



### &lt;word-count&gt;

Synonyms: &lt;wc&gt;

The &lt;word-count&gt; tag prints the total number of words in the document. This number ignores anything contained in &lt;mathematics&gt;, &lt;code&gt;, or &lt;annotation&gt; tags, as well as element names, attribute names, and attribute values.


## Other Elements


### &lt;quotation&gt;

Synonyms: &lt;quote&gt;, &lt;q&gt;

**Analogous to the HTML &lt;blockquote&gt; and &lt;q&gt; elements.**

The &lt;quotation&gt; element defines a quotation. If a &lt;quotation&gt; element is contained by a &lt;paragraph&gt; element, then it will be rendered as an in-line quotation, but if not, it will be rendered as a block quotation.

#### Example

```xml
<p>
  Einstein said, <q>Imagination is more important than knowledge.</q>
</p>
```



### &lt;code&gt;

**Analogous to the HTML &lt;code&gt; element.**

The &lt;code&gt; element defines a section of text that is computer code. Such text is normally rendered using a monospace font.

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|language|-|the name of the programming language or syntax that the code is in|



### &lt;mathematics&gt;

Synonyms: &lt;maths&gt;, &lt;m&gt;

The &lt;mathematics&gt; element defines a section of mathematics - either in-line mathematics or display-style mathematics. If a &lt;mathematics&gt; element is contained by a &lt;paragraph&gt; element, then it will be rendered as in-line mathematics, but if not, it will be rendered as display-style mathematics.

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|format|-|one of 'latex', 'mathml'; the default is 'latex'|

#### Example

```xml
<p>
  A straight line is described by <m>y = mx + c</m>.
</p>
```



### &lt;annotation&gt;

Synonyms: &lt;a&gt;

The &lt;annotation&gt; element defines an annotation. Annotations are not rendered when the document is printed, and are a way of adding comments to the digital form of the document.



### &lt;footnote&gt;

Synonyms: &lt;fn&gt;

The &lt;footnote&gt; element defines a footnote. The footnote can be added into the document at the point where it is relevant - when the final document is rendered, it will be moved to the bottom of the page.



### &lt;hyperlink&gt;

Synonyms: &lt;hl&gt;

**Analogous to the HTML &lt;a&gt; element.**

The &lt;hyperlink&gt; element defines a hyperlink.

#### Attributes

|Name|Synonyms|Allowed Values|
|---|---|---|
|url|-|analogous to the HTML href attribute on &lt;a&gt; tags|

#### Example

```xml
<p>
  The GitHub repository for this XSDR Specification can be found <hl url="https://github.com/BenjaminTMilnes/XSDRSpecification/">here</hl>.
</p>
```



### &lt;horizontal-rule&gt;

Synonyms: &lt;hr&gt;

**Analogous to the HTML &lt;hr&gt; element.**


