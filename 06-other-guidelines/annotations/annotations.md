---
title: "Guidelines on Using SDMX Annotations"
source_url: https://sdmx.org/wp-content/uploads/Guidelines-on-the-use-of-SDMx-Annotations-2.0.docx
source_file: Guidelines-on-the-use-of-SDMx-Annotations-2.0.docx
source_sha256: 173303bbf8fc1d6465fd46727d527ff9592304790709de709a567c37076e5584
source_last_modified: "Tue, 29 Apr 2025 09:29:40 GMT"
retrieved: 2026-09-24
licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)
conversion: DOCX -> Markdown, wording and structure unchanged; see NOTICE.md for the list of changes
page_furniture_not_reproduced:
  - "Restricted Use - À usage restreint"
---
<!-- figure: f01-logo -->
![SDMX logo](images/f01-logo.png)

**GUIDELINES ON USING SDMX ANNOTATIONS**

**Version 2.0 – April 2025**

# DOCUMENT HISTORY

| **Version** | **Date** | **Comment** |
|----|----|----|
| 1.0 | 01/03/2021 | Initial version. |
| 2.0 | 24/04/2025 | Adapted to SDMX 3.0. Extensions to controlled vocabulary. Clarified text. |

<a id="_Toc196741567"></a>

# Contents

[DOCUMENT HISTORY](#document-history)

[Contents](#_Toc196741567)

[Introduction](#introduction)

[SDMX Information Model for the Annotation construct](#sdmx-information-model-for-the-annotation-construct)

[SDMX 2.1](#sdmx-21)

[SDMX 3.0](#sdmx-30)

[Properties of the Annotation construct](#properties-of-the-annotation-construct)

[Introducing Standard Annotations](#introducing-standard-annotations)

[How to Identify Standard Annotations?](#how-to-identify-standard-annotations)

[Examples](#examples)

[The Business value of Standard Annotations](#the-business-value-of-standard-annotations)

[List of Standard Annotations](#list-of-standard-annotations)

[Relationships between Annotation properties](#relationships-between-annotation-properties)

[General and Display-related Annotation types](#general-and-display-related-annotation-types)

[Codelist and Statistical Classification-specific Annotations](#codelist-and-statistical-classification-specific-annotations)

[Concept Scheme SDMX:CS_ANNOT](#concept-scheme-sdmxcs_annot)

[Example of a Concept](#example-of-a-concept)

[SDMX-ML of the Example](#sdmx-ml-of-the-example)

[References](#references)

# Introduction

According to the SDMX documentation, the Annotation is a construct that contains user or organisation-specific metadata. The Annotation construct in SDMX is available to most of the SDMX structural metadata artefacts. This facility is essentially a flexible extension mechanism allowing metadata to be added to an SDMX structural artefact. Annotations are often used to store metadata in artefacts when there is no specific place for that information in the SDMX information model. Presentation metadata is a prime example, such as a default presentation for a dataflow.

Note that whilst the SDMX Annotation has a specific structure (Title, Type, URL, Text) individual organisations are free to use these in any way and any combination they wish. However, an Annotation can only be processed in a meaningful way (i.e. other than viewing it) by systems that understand its semantics.

The main advantage of the Annotation is its flexibility as all properties can be tailor-made and there is no limit to their number. This can prove very useful for specific applications, such as dissemination tools. The main drawback is poor interoperability as Annotations convey no semantics and are not standardised. This means that organisations that want to exchange Annotations and process them automatically must agree upon, at least, a common naming syntax.

The aim of this guideline is to improve machine interactions by proposing a controlled vocabulary for the Type property of the SDMX Annotation construct and a recommended usage for the other properties that will greatly improve the interoperability of Annotations between SDMX-compliant organisations.

The Controlled Vocabulary referred to above will be maintained as a SDMX Concept Scheme stored in the SDMX Global Repository.

# SDMX Information Model for the Annotation construct

### SDMX 2.1

<!-- figure: f02-uml-sdmx21 -->
```mermaid
classDiagram
    direction LR
    class AnnotableArtefact
    class Annotation {
        id : String
        title : String
        type : String
        url : String
    }
    class InternationalString
    class LocalisedString {
        label : String
        locale : String
    }
    AnnotableArtefact "0..1" o-- "0..*" Annotation
    Annotation "0..1" *-- "0..1" InternationalString : +text
    InternationalString "1" *-- "0..*" LocalisedString
    style AnnotableArtefact fill:#FFFFFF,stroke:#8B1A4B
    style Annotation fill:#FFFFCC,stroke:#8B1A4B
    style InternationalString fill:#FFFFCC,stroke:#8B1A4B
    style LocalisedString fill:#FFFFCC,stroke:#8B1A4B
```

<details>
<summary>Original figure</summary>

![SDMX 2.1 information model for the Annotation construct](images/f02-uml-sdmx21.png)

</details>

All classes derived from the abstract class AnnotableArtefact may have Annotations. The Annotation is used to convey extra information to describe SDMX constructs. This information may be in the form of a URL reference, a non-localised text, and/or multiple localised texts (represented by the one-to-many relationship to LocalisedString).

### SDMX 3.0

<!-- figure: f03-uml-sdmx30 -->
```mermaid
classDiagram
    class Annotation {
        - id: String
        - title: String
        - type: String
        - url: url
        - value: String
    }
    class InternationalUri
    class InternationalString
    class LocalisedUri {
        - url: url
        - locale: String
    }
    class LocalisedString {
        - label: String
        - locale: String
    }
    class Key
    Annotation "0..1" *-- "0..1" InternationalUri : +url
    Annotation "0..1" *-- "0..1" InternationalString : +text
    InternationalUri "1" *-- "1..*" LocalisedUri
    InternationalString "1" *-- "1..*" LocalisedString
    style Annotation fill:#FFF9A6,stroke:#404040
    style InternationalUri fill:#FFF9A6,stroke:#404040
    style InternationalString fill:#FFF9A6,stroke:#404040
    style LocalisedUri fill:#FFF9A6,stroke:#404040
    style LocalisedString fill:#FFF9A6,stroke:#404040
    style Key fill:#F2F2F2,stroke:#404040
```

<details>
<summary>Original figure</summary>

![SDMX 3.0 information model for the Annotation construct](images/f03-uml-sdmx30.png)

</details>

The URL can be localised which gives the advantage of linking to different resources depending on the language. It also removes the complexity of having to use AnnotationText in SDMX 2.1 to do this.

# Properties of the Annotation construct

The properties of the Annotation construct are listed below. This information is taken from the [SDMX official technical documentation](https://sdmx.org/?page_id=5008).

<table>
<colgroup>
<col style="width: 28%" />
<col style="width: 37%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;">Property</th>
<th style="text-align: center;">Description</th>
<th style="text-align: center;">Controlled vocabulary context</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;">id</td>
<td style="text-align: left;">Identifier for the Annotation. It can be used to disambiguate one Annotation from another where there are several Annotations for the same annotated object.</td>
<td style="text-align: left;">Id is set to @SDMX to identify it as part of the controlled vocabulary</td>
</tr>
<tr>
<td style="text-align: center;">title</td>
<td style="text-align: left;">A title used to identify an Annotation.</td>
<td style="text-align: left;">A non-localised value for the annotation. Used when localisation is irrelevant.</td>
</tr>
<tr>
<td style="text-align: center;">type</td>
<td style="text-align: left;"><p>Specifies how the Annotation is to be processed.</p>
<p>The <strong>type</strong> is often used as the usage context of the Annotation. The types are not enumerated<sup><a href="#fn-1" id="fnref-1">1</a></sup>, as these can be specified by the Annotation creator. The definitions and use of Annotation types should be documented by their creator.</p></td>
<td style="text-align: left;">Identifies the usage (e.g. images are type IMAGE) of the annotation. The type values are enumerated in the controlled vocabulary table.</td>
</tr>
<tr>
<td style="text-align: center;">url</td>
<td style="text-align: left;"><p>A link to external descriptive text.</p>
<p>The <strong>url</strong> is a URI - typically a URL - which points to a resource. If a specific behaviour is desired, an Annotation type should be defined which specifies the use of this field more exactly.</p></td>
<td style="text-align: left;">A non-localised URL reference to an external resource. Used when localisation is irrelevant.</td>
</tr>
<tr>
<td style="text-align: center;">+url</td>
<td style="text-align: left;"><strong>SDMX 3.0 and later</strong>. An annotation may have several localised URLs</td>
<td style="text-align: left;">A localised URL reference to an external resource.</td>
</tr>
<tr>
<td style="text-align: center;">+text</td>
<td style="text-align: left;"><p>An International String that provides the multilingual text content of the Annotation.</p>
<p><strong>Text</strong> holds a language-specific string containing the text of the Annotation.</p></td>
<td style="text-align: left;">A localised value for the annotation.</td>
</tr>
</tbody>
</table>

# Introducing Standard Annotations

As stated earlier, a major drawback of the Annotation construct is the fact that they are not standardised for reuse when exchanging structural metadata. Annotations are containers for additional information relating to the object to which they are attached. This means that for an Annotation to be interpreted in the same way by exchange partners, a reference is needed that defines some standard behaviour and implementation.

This guideline proposes an Annotation controlled vocabulary and guidelines on their (re)use for SDMX implementers.

A standard Annotation can be defined as an Annotation that has an agreed definition in the SDMX community. Some of them, especially the general and display-related annotations also have a described behaviour. They allow diverse systems to parse the information and perform a specific action in response.

# How to Identify Standard Annotations?

In order to be able to configure their applications to implement actions based upon standard Annotations, systems must know how to identify such Annotations. This is done by setting the Annotation **id** property to “@SDMX” which indicates that the Annotation is part of the controlled vocabulary described in the section List of Standard Annotations, and avoids using “@SDMX” for other usage contexts. For example, ORDER could be the order of codes (as described in this controlled vocabulary) or some kind of order number (a different usage).

The additional mandatory information to be provided is the **type** property that specifies the type of action to be implemented. There may be other mandatory property values depending on the type of the standard Annotation.

## Examples

The <span style="background-color:#E2EFD9">green columns in the table below</span> show example usages of standard Annotations. The <span style="background-color:#FBE4D5">orange “ORDER”</span> column is not a standard Annotation because the usage context is not the same as the standard Annotation “ORDER”, therefore the **id** should not be “@SDMX”.

<!-- figure: f05-standard-annotation-examples -->
```mermaid
block-beta
    columns 76
    r0c0["id*"]:8 r0c1["@SDMX"]:14 r0c2["@SDMX"]:12 r0c3["@SDMX"]:12 r0c4["Not @SDMX<br>This is a “customer order no.” which is a different use case than the ORDER standard Annotation which is a list order"]:30
    r1c0["title"]:8 r1c1[" "]:14 r1c2[" "]:12 r1c3[" "]:12 r1c4["1934245"]:30
    r2c0["type*"]:8 r2c1["NOT_DISPLAYED"]:14 r2c2["EXCLUDES"]:12 r2c3["ORDER"]:12 r2c4["ORDER"]:30
    r3c0["+text"]:8 r3c1[" "]:14 r3c2[" "]:12 r3c3["en :10"]:12 r3c4[" "]:30
    r4c0[" "]:8 r4c1[" "]:14 r4c2[" "]:12 r4c3["fr :20"]:12 r4c4[" "]:30
    classDef default fill:#FFFFFF,stroke:#D9D9D9,color:#000000
    style r0c0 fill:#D9D9D9,stroke:#BFBFBF
    style r0c1 fill:#E2EFD9,stroke:#BFBFBF
    style r0c2 fill:#E2EFD9,stroke:#BFBFBF
    style r0c3 fill:#E2EFD9,stroke:#BFBFBF
    style r0c4 fill:#FBE4D5,stroke:#BFBFBF
    style r1c0 fill:#D9D9D9,stroke:#BFBFBF
    style r1c1 fill:#E2EFD9,stroke:#BFBFBF
    style r1c2 fill:#E2EFD9,stroke:#BFBFBF
    style r1c3 fill:#E2EFD9,stroke:#BFBFBF
    style r1c4 fill:#FBE4D5,stroke:#BFBFBF
    style r2c0 fill:#D9D9D9,stroke:#BFBFBF
    style r2c1 fill:#E2EFD9,stroke:#BFBFBF
    style r2c2 fill:#E2EFD9,stroke:#BFBFBF
    style r2c3 fill:#E2EFD9,stroke:#BFBFBF
    style r2c4 fill:#FBE4D5,stroke:#BFBFBF
    style r3c0 fill:#D9D9D9,stroke:#BFBFBF
    style r3c1 fill:#E2EFD9,stroke:#BFBFBF
    style r3c2 fill:#E2EFD9,stroke:#BFBFBF
    style r3c3 fill:#E2EFD9,stroke:#BFBFBF
    style r3c4 fill:#FBE4D5,stroke:#BFBFBF
    style r4c0 fill:#D9D9D9,stroke:#BFBFBF
    style r4c1 fill:#E2EFD9,stroke:#BFBFBF
    style r4c2 fill:#E2EFD9,stroke:#BFBFBF
    style r4c3 fill:#E2EFD9,stroke:#BFBFBF
    style r4c4 fill:#FBE4D5,stroke:#BFBFBF
```

<details>
<summary>Original figure</summary>

![Example usages of standard annotations (green columns) and a non-standard ORDER annotation (orange column)](images/f05-standard-annotation-examples.png)

</details>

<span style="color:#FF0000">\*</span> denotes a mandatory information for standard Annotations

# The Business value of Standard Annotations

The following diagram explains the business value and decision process when deciding whether to use a standard Annotation. As can be seen, if they are used then a maximum reuse is made of the Annotation itself, tools and processes. If they are not used then bespoke Annotations, agreements, tools and processing are required to understand and make use of the information in the Annotation, and it (plus supporting tools, processes, etc.) is harder to reuse.

<!-- figure: f04-business-value -->
```mermaid
flowchart LR
    N{{"Need to use<br>an SDMX<br>Annotation"}}:::start
    Q1{"Is there a « Standard<br>Annotation » with the<br>same use case?"}:::q
    U["Use a « Standard<br>Annotation »<br>(as defined in this<br>guideline)"]:::green
    J1((" ")):::dot
    B1["Define a « bespoke »<br>Annotation"]:::gold
    B2["Define a « bespoke »<br>tool to process the<br>Annotation"]:::gold
    J2((" ")):::dot
    Q2{"Does the Annotation<br>need to be used<br>between exchange<br>parties?"}:::q
    I["The Annotation<br>is internal only"]:::red
    A["The Annotation requires a<br>usage and maintenance<br>agreement between<br>exchange parties"]:::gold
    N --> Q1
    Q1 -- "Yes" --> U
    Q1 -- "No" --- J1
    J1 --> B1
    J1 --> B2
    B1 --- J2
    B2 --- J2
    J2 --> Q2
    Q2 -- "No" --> I
    Q2 -- "Yes" --> A
    classDef start fill:#1FBF8F,stroke:#17A077,color:#FFFFFF
    classDef q fill:#003B7A,stroke:#003B7A,color:#FFFFFF
    classDef green fill:#0BA84A,stroke:#0BA84A,color:#FFFFFF
    classDef gold fill:#BF9000,stroke:#BF9000,color:#FFFFFF
    classDef red fill:#FF0000,stroke:#FF0000,color:#FFFFFF
    classDef dot fill:#1B7A8C,stroke:#1B7A8C
```

<details>
<summary>Original figure</summary>

![Business value of standard annotations: decision process](images/f04-business-value.png)

</details>

# List of Standard Annotations

This section lists the standard Annotations with their typical usage contexts. This list will be expanded over time as new implementations and needs arise. When references to external standards are made (e.g. skos or xkos specifications), the reader is invited to consult the “References” section for more information.

The list of standard Annotations will be available from the SDMX Registry as artefact: SDMX:CS_ANNOT(\*.\*.\*). Link: <https://registry.sdmx.org/ws/public/sdmxapi/rest/conceptscheme/SDMX/CS_ANNOT/latest/?format=sdmx-2.1&detail=full&references=none>

**Note:** There are several Annotations that are types of name or label, e.g. FULL_NAME, SHORT_LABEL, ORIGINAL_LABEL. These Annotations have specific use cases that are described in the tables below and should not be used to replace an artefact’s or item scheme item’s Name and Description property.

## Relationships between Annotation properties

#### Text value defaults and specific locale values

Some use cases may benefit from having a single, default value for all locales/languages but also to set the value for certain locales. An example is ORDER where there may be a default list order for all locales but two locales have a specific order which is different from the default. In order to avoid having to state an order for every locale, the Annotation Title property may be used to state the default value, whereas the text property is used for the localised values.

Consider this annotation *Example:* An ORDER annotation type that is attached to a code item ACME. If both the Annotation Text and Annotation Title have values, then the Annotation Text value (e.g. en:10,es:20) is used for the localized values instead of the Annotation Title (e.g. 30) which would only be taken if the locale in the context is not found among the specified ones.

#### URL value defaults and specific locale values

##### SDMX 2.1 and earlier

In SDMX 2.1, the Annotation’s URL property is a single, non-localised value. There may be cases where different URLs are required for certain locales. In this case, it is recommended to use the Annotation text property and state the language and URL in an HTML fragment, for example:

fr:\<a href=”https://someLink”\>

When both a URL and text property for the locale exists, the text property overrides (is used instead of) the URL property.

##### SDMX 3.0 and later

Multiple URL localised properties were introduced in SDMX 3.0. Therefore, the URL work-around in the above paragraph is not recommended. The URL property should be used as shown in the table.

## General and Display-related Annotation types

<table>
<colgroup>
<col style="width: 15%" />
<col style="width: 22%" />
<col style="width: 13%" />
<col style="width: 14%" />
<col style="width: 20%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr>
<th>Annotation Type</th>
<th>Use Case</th>
<th>Where to attach</th>
<th><p>+Text</p>
<p><span style="color:#5B9BD5">Blue is optional</span></p></th>
<th><p>Title</p>
<p><span style="color:#5B9BD5">Blue is optional</span></p></th>
<th><p>SDMX 2.1:URL</p>
<p>SDMX &gt;=3.0:+URL</p>
<p><span style="color:#5B9BD5">Blue is optional</span></p></th>
</tr>
</thead>
<tbody>
<tr>
<td>FULL_NAME</td>
<td>Alternative name to be displayed for items in Item Schemes (e.g. Codelists, Concept Schemes, Category Schemes) whenever the item is displayed without its parent. For example, if a code list that has a hierarchy is displayed as a flat list, then this annotation may be used to provide sufficient context for the code. Concatenation of code + heading in NACE Rev.2.1 <br />
en: A0123 Growing of citrus fruits</td>
<td>Item in an Item Scheme</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:Labour force (Employment)</span></p></td>
<td><span style="color:#5B9BD5">&lt;content&gt;</span></td>
<td></td>
</tr>
<tr>
<td>REPLACE_NAME</td>
<td>Replace each code name in a component by the value of another component in an observation or series</td>
<td>A Dataflow or DSD</td>
<td></td>
<td><p>&lt;component Id to replace name&gt;:&lt;component Id to use name&gt;</p>
<p><em>Example:</em></p>
<p>CUST_BREAKDOWN:CUST_BREAKDOWN_LB</p></td>
<td></td>
</tr>
<tr>
<td>REPLACE_CONTENT</td>
<td>Replace the content in a component by the value of another component in an observation or series</td>
<td>A Dataflow or DSD</td>
<td></td>
<td><p>&lt;component Id to replace content&gt;:&lt;component Id to use content&gt;</p>
<p><em>Example:</em></p>
<p>REF_AREA:M49_CODE</p></td>
<td></td>
</tr>
<tr>
<td>COMPLEMENT</td>
<td><p>Additional fixed text to be displayed in parenthesis after the code name.</p>
<p>E.g. Representation of Non-hazardous (NHAZW), hazardous waste (HAZW) in the European List of Wastes<br />
en: 01 03 04* acid-generating tailings from processing of sulphide ore (HAZW)<br />
en: 01 03 99 wastes not otherwise specified (NHAZW)</p></td>
<td>Item in an Item Scheme</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:See reference metadata </span></p></td>
<td><span style="color:#5B9BD5">&lt;content&gt;</span></td>
<td></td>
</tr>
<tr>
<td>ORDER</td>
<td>Explicit indication of a localised order of items in Items Schemes or artefacts (e.g. Codelist, Concept Scheme, Category Scheme, Dataflow, etc.)</td>
<td><p>Either:</p>
<ul>
<li><p>an artefact, or;</p></li>
<li><p>an item in an Item Scheme</p></li>
</ul></td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:10,es:20</span></p></td>
<td><span style="color:#5B9BD5">&lt;content&gt;</span></td>
<td></td>
</tr>
<tr>
<td>TOTAL</td>
<td><p>Code Item that represents a total value. If the attachment is:</p>
<ul>
<li><p>to a Code, the Annotation Text is optional and may contain an explanatory text;</p></li>
</ul>
<p>to a Codelist, the Annotation Title is mandatory and includes the code(s) that represent a total</p></td>
<td><p>Either:</p>
<ul>
<li><p>a Code Item that represents a total value, or;</p></li>
<li><p>a Codelist to specify the code(s) with the total</p></li>
</ul></td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;explanatory text&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;explanatory text&gt;,…</span></p></td>
<td><p><span style="color:#5B9BD5">Attached to Code Item: &lt;blank&gt;</span></p>
<p><span style="color:#5B9BD5">Attached to Codelist: &lt;code&gt;,&lt;code&gt;,…</span></p></td>
<td></td>
</tr>
<tr>
<td>DRILLDOWN</td>
<td>Denotes the concept that specifies whether observations are at the aggregate level or a drilldown.</td>
<td><p>Either:</p>
<ul>
<li><p>A Dataflow or DSD</p></li>
</ul></td>
<td></td>
<td><p>&lt;concept Id&gt;</p>
<p><em>Example:</em></p>
<p>DD_DIM (this concept should be hidden using the NOT_DISPLAYED Annotation below)</p></td>
<td></td>
</tr>
<tr>
<td>DEPRECATED</td>
<td><p>Indication that an Item in an Item Scheme or an artefact is deprecated.</p>
<p>For an item scheme item, the annotation value provides a replacement name for the code name.</p>
<p>For an artefact, the URL points to the replacement artefact. May be used in conjunction with SUPERSEED where the replacement artefact references the replaced artefact.</p>
<p>Suggestion to use a controlled vocabulary</p>
<p>url: &lt;<a href="http://publications.europa.eu/resource/authority/concept-status/CURRENT">http://publications.europa.eu/resource/authority/concept-status/CURRENT</a>&gt;<br />
url: &lt;<a href="http://publications.europa.eu/resource/authority/concept-status/DEPRECATED">http://publications.europa.eu/resource/authority/concept-status/DEPRECATED</a>&gt;</p>
<p>or </p>
<p>TITLE: true (false)</p></td>
<td><p>Either:</p>
<ul>
<li><p>an artefact, or;</p></li>
<li><p>an item in an Item Scheme</p></li>
</ul></td>
<td><p><span style="color:#5B9BD5">For item scheme item:</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:deprecated,fr:obsolète</span></p></td>
<td><span style="color:#5B9BD5">&lt;content&gt;</span></td>
<td><p><span style="color:#5B9BD5">For artefact:</span></p>
<p><span style="color:#5B9BD5">&lt;see section URL value defaults and specific locale values&gt;</span></p></td>
</tr>
<tr>
<td>DEFAULT</td>
<td><p>Indication that an item in an Item Scheme or artefacts is to be selected by default.</p>
<p>The Annotation defines a selection so that a pre-defined default subset of data can be processed (e.g. visualised, extracted) instead of the entire dataset</p></td>
<td><ul>
<li><p>Item in ItemScheme, or;</p></li>
<li><p>DSD, or;</p></li>
<li><p>a Dataflow</p></li>
</ul>
<p>Note: A DEFAULT Annotation attached to a later level in this list supersedes that attached to an earlier level. E.g., a DEFAULT Annotation attached to individual Codes in Codelists is only to be used when there is no DEFAULT Annotation attached to the Dataflow nor to the DSD, and those of DSDs are only to be used when there is no DEFAULT Annotation attached to the Dataflow.</p></td>
<td></td>
<td><p>Attached to:</p>
<p>- DSD or Dataflow:<br />
 <strong>&lt;concept&gt;=&lt;code&gt;+&lt;code&gt;+…,&lt;concept&gt;=&lt;code&gt;+&lt;code&gt;+…</strong></p>
<p><em>Example:</em> FREQ=A+Q,TIME_PERIOD_START=2013-01,TIME_PERIOD_END=2018-12</p></td>
<td></td>
</tr>
<tr>
<td>IMAGE</td>
<td>A visual identity to associate to Item Scheme Items or artefacts</td>
<td><p>Either:</p>
<ul>
<li><p>an artefact, or;</p></li>
<li><p>an item in an item scheme</p></li>
</ul></td>
<td style="text-align: left;"><p>For localised content in SDMX 2.1</p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;HTML containing URL to the resource&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;HTML containing URL to the resource&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:&lt;a href=”https://sdmx.org/wp-content/uploads/SDMX_map_small-220x220.jpg”&gt;</span></p></td>
<td></td>
<td><p><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">https://sdmx.org/wp-content/uploads/SDMX_map_small-220x220.jpg</span></p></td>
</tr>
<tr>
<td>DRILLDOWN_CONCEPTS</td>
<td>Concepts to be displayed in a drilldown operation</td>
<td>Dataflow or DSD</td>
<td></td>
<td style="text-align: left;"><p>&lt;concept Id&gt;,&lt;concept Id&gt;,…</p>
<p>Example :</p>
<p>DONOR,RECIPIENT,YEAR,PROJECT_ID,OBS_VALUE,DESCRIPTION,OWNER</p></td>
<td></td>
</tr>
<tr>
<td>NOT_DISPLAYED</td>
<td>Used to hide components or their values in the presentation</td>
<td style="text-align: left;"><p>Either:</p>
<ul>
<li><p>a Dataflow or DSD, or;</p></li>
<li><p>an Item in an Item Scheme</p></li>
</ul></td>
<td></td>
<td style="text-align: left;"><p>Attached to Item in Item Scheme: &lt;blank&gt;</p>
<p>Attached to Dataflow or DSD:</p>
<p>&lt;concept Id&gt;,&lt;concept Id&gt;,…</p>
<p>Example :</p>
<p>DD_DIM (to hide drilldown control concept)</p></td>
<td></td>
</tr>
<tr>
<td>LAYOUT_ROW</td>
<td>Dimensions to be presented in rows (concepts on y-axis)</td>
<td><p>Either:</p>
<ul>
<li><p>an artefact, or;</p></li>
<li><p>a Dimension</p></li>
</ul></td>
<td></td>
<td style="text-align: left;"><p>Attached to Dimension: &lt;blank&gt;</p>
<p>Attached to Dataflow or DSD: &lt;dimension Id&gt;,&lt;dimension Id &gt;,…</p>
<p><em>Example:</em></p>
<p>REF_AREA,MEASURE</p></td>
<td></td>
</tr>
<tr>
<td>LAYOUT_COLUMN</td>
<td>Dimensions to be presented in columns (concepts on x-axis)</td>
<td><p>Either:</p>
<ul>
<li><p>an artefact, or;</p></li>
<li><p>a Dimension</p></li>
</ul></td>
<td></td>
<td style="text-align: left;"><p>Attached to Dimension: &lt;blank&gt;</p>
<p>Attached to Dataflow or DSD: &lt;dimension Id&gt;,&lt;dimension Id&gt;,…</p>
<p><em>Example:</em></p>
<p>TIME_PERIOD</p></td>
<td></td>
</tr>
<tr>
<td>LAYOUT_FLAG</td>
<td>Indication that an attribute and its attribute value should be presented as a flag</td>
<td>Dataflow</td>
<td></td>
<td style="text-align: left;"><p>&lt;concept Id&gt;,&lt;concept Id&gt;,...</p>
<p><em>Example:</em></p>
<p>OBS_STATUS,CONF_STATUS</p></td>
<td></td>
</tr>
<tr>
<td>LAYOUT_NOTE</td>
<td>Indication that an attribute and its attribute value should be presented as a note</td>
<td>Dataflow</td>
<td></td>
<td style="text-align: left;"><p>&lt;concept Id&gt;,&lt;concept Id&gt;,...</p>
<p><em>Example:</em></p>
<p>OBS_STATUS,CONF_STATUS</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: left;">METADATA</td>
<td>Links an MSD directly to a DSD. Can be used to overcome the complexities of reference metadata linkage</td>
<td>DSD</td>
<td></td>
<td>MSD URI, e.g. urn:sdmx:org.sdmx.infomodel.metadatastructure.MetadataStructure=OECD:MSD_REF_METADATA(1.0)</td>
<td></td>
</tr>
<tr>
<td style="text-align: left;">LAYOUT_ROW_SECTION</td>
<td>Dimension to be presented as a break-down concept at a third hierarchical level above columns and rows.</td>
<td><p>Either:</p>
<ul>
<li><p>an artefact, or;</p>
<p>a Dimension</p></li>
</ul></td>
<td></td>
<td><p>Attached to Dimension: &lt;blank&gt;</p>
<p>Attached to Dataflow or DSD: &lt;dimension Id&gt;,&lt;dimension Id&gt;,…</p>
<p><em>Example:</em></p>
<p>SEX</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: left;">EXT_RESOURCE</td>
<td><p>A localised link to an external resource associated to the annotated artefact. For example, an ontology item</p>
<p><em>a methodology</em> en:&lt;a href:"<a href="https://ec.europa.eu/eurostat/web/waste/methodology">https://ec.europa.eu/eurostat/web/waste/methodology</a>"&gt;</p></td>
<td>Any SDMX object</td>
<td style="text-align: left;"><p><span style="color:#5B9BD5">For localised content in SDMX 2.1</span></p>
<p><span style="color:#5B9BD5"> &lt;language&gt;:&lt;HTML containing URL to the resource&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;HTML containing URL to the resource&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:&lt;a href=”</span><a href="http://rdf-vocabulary.ddialliance.org/xkos#depth">http://rdf-vocabulary.ddialliance.org/xkos#depth</a><span style="color:#5B9BD5">”&gt;</span></p></td>
<td style="text-align: left;"></td>
<td><p><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">http://rdf-vocabulary.ddialliance.org/xkos#depth</span></p></td>
</tr>
<tr>
<td style="text-align: left;">COMBINED_CONCEPTS</td>
<td><p>Comma-separated list of concept IDs to show as a concatenated label.</p>
<p>The listed concepts’ item contents may be concatenated to generate the target concept.</p>
<p>Multiple target concept combinations can be defined by separating the target concepts by ;</p></td>
<td>Dataflow or DSD</td>
<td><p>&lt;language&gt;:&lt;display name&gt;,</p>
<p>&lt;language&gt;:&lt;display name&gt;</p>
<p>e.g. COMBINED_UNIT_MEASURE:PRICE_BASE,UNIT_MEASURE;COMBINED_MEASURE:MEASURE,REF_SECTOR{(en):Combined unit of measure;Combined measure}{(fr):Unité de mesure combinée;Mesure combinée}</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: left;">(deprecated) UNIT_MEASURE_CONCEPTS</td>
<td><p>Comma-separated list of concept IDs that is used to define the full unit of measure. The concepts must be in the DSD.</p>
<p>The listed concepts’ item contents may be concatenated to generate the unit of measure label (unless the UNIT_MEASURE_LABEL annotation is present).</p></td>
<td>Dataflow or DSD</td>
<td></td>
<td><p>&lt;concept Id&gt;,&lt;concept Id&gt;,…</p>
<p><em>Example:</em> UNIT_MEASURE,UNIT_MULT,TRANSFORMATION [could generate a value of Australian Dollar, Thousands, Non-transformed]</p></td>
<td></td>
</tr>
<tr>
<td>(deprecated) UNIT_MEASURE_LABEL</td>
<td><p>Indicates the concept that enumerates the full unit of measure labels.</p>
<p>The concept must be in the DSD. UNIT_MEASURE_LABEL overrides the UNIT_MEASURE_CONCEPTS if both are provided.</p>
<p>Also can be attached to items in item scheme, e.g.</p>
<p>Text     en:Gram<br />
           fr: Gramme<br />
url:<strong> <a href="http://data.europa.eu/gzn/su/G">http://data.europa.eu/gzn/su/G</a></strong></p></td>
<td>Dataflow or DSD, Item in an Item Scheme</td>
<td><p><span style="color:#5B9BD5">This is optional, used if a freetext label is required.</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:USD, thousands</span></p>
<p><span style="color:#5B9BD5">fr:USD, milliers</span></p></td>
<td><p><span style="color:#5B9BD5">This is optional, used if an enumerated list is required.</span></p>
<p><span style="color:#5B9BD5">&lt;concept Id&gt;</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">UOM_ATTRIBUTE [This concept may contain the following items as units of measure:</span></p>
<ul>
<li><p><span style="color:#5B9BD5">National Currency, thousands</span></p></li>
<li><p><span style="color:#5B9BD5">USD, thousands</span></p></li>
</ul>
<p><span style="color:#5B9BD5">Index, based on National Currency]</span></p></td>
<td></td>
</tr>
<tr>
<td>LAYOUT_TIME_PERIOD_DESC</td>
<td>Indication that the display of the TIME_PERIOD dimension for a dataflow, or all dataflows of the same DSD, is to be done in descending sort order.</td>
<td>Dataflow, DSD</td>
<td></td>
<td><p><em>Example:</em></p>
<p>LAYOUT_TIME_PERIOD_DESC</p></td>
<td></td>
</tr>
<tr>
<td>LAYOUT_CELL_ALIGN</td>
<td>Indication to force the data cell alignment to the left or to the right. This can be defined generically for all locales or per locale.</td>
<td>Dataflow, DSD, Dimension</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><span style="color:#5B9BD5">&lt;content&gt; values:RIGHT or LEFT</span></p></td>
<td><span style="color:#5B9BD5">Content values:RIGHT or LEFT</span></td>
<td></td>
</tr>
<tr>
<td>MAX_TABLE_DATA</td>
<td>Increase the maximum preview table size above default maximum limits for the number of observations retrieved from the SDMX web service and for the number of table cells</td>
<td>Dataflow</td>
<td></td>
<td><p>&lt;integer&gt;</p>
<p><em>Example:</em></p>
<p>15000</p></td>
<td></td>
</tr>
<tr>
<td>MAXTEXTATTRIBUTELENGTH</td>
<td>Increase the maximum length for textual attribute values</td>
<td>DSD</td>
<td></td>
<td><p>&lt;integer&gt;</p>
<p><em>Example:</em></p>
<p>500</p></td>
<td></td>
</tr>
<tr>
<td>SEARCH_WEIGHT</td>
<td>Indication of localised boosted dataflows in the search results when ordered by relevance</td>
<td>Dataflow</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;integer&gt;,...</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">"en":"3","es":"4","fr":"5"</span></p></td>
<td><p><span style="color:#5B9BD5">&lt;integer&gt;</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">10</span></p></td>
<td></td>
</tr>
</tbody>
</table>

## Codelist and Statistical Classification-specific Annotations 

The categories below are used widely, for example by the European Statistical System (ESS), and the United Nations Statistics Division for its central framework classifications ISIC4<sup><a href="#fn-2" id="fnref-2">2</a></sup> and CPC<sup><a href="#fn-3" id="fnref-3">3</a></sup>.

<table>
<colgroup>
<col style="width: 15%" />
<col style="width: 22%" />
<col style="width: 13%" />
<col style="width: 14%" />
<col style="width: 20%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr>
<th>Annotation Type</th>
<th>Use Case</th>
<th>Where to attach</th>
<th><p>+Text</p>
<p><span style="color:#5B9BD5">Blue is optional</span></p></th>
<th><p>Title</p>
<p><span style="color:#5B9BD5">Blue is optional</span></p></th>
<th><p>SDMX 2.1:URL</p>
<p>SDMX &gt;=3.0:+URL</p>
<p><span style="color:#5B9BD5">Blue is optional</span></p></th>
</tr>
</thead>
<tbody>
<tr>
<td>ORIGINAL_CODE</td>
<td>Code as displayed in other representations, such as official or original documentation (i.e. possibly containing dots, spaces, etc.). Reference to external standard: skos:notation</td>
<td>Item in an Item Scheme</td>
<td></td>
<td><p>&lt;original code&gt;</p>
<p><em>Examples:</em></p>
<ul>
<li><p>0105.13 [Harmonized System]</p></li>
<li><p>11.2.0.9 [COICOP classification]</p></li>
</ul></td>
<td></td>
</tr>
<tr>
<td>HIER_CONTEXT</td>
<td><p>In SDMX 2.1, a reference between a usage context and a hierarchy (that may be contained in a Hierarchical Codelist (HCL)).</p>
<p>In SDMX 3.0, use the HierarchyAssociation artefact</p></td>
<td>DSD or Dataflow</td>
<td></td>
<td><p><span style="color:#1F497D">&lt;component Id&gt;:&lt;HCL Id&gt;.&lt;hierarchy Id&gt; </span></p>
<p><em>Example:</em></p>
<p><span style="color:#1F497D">REF_AREA:OECD.EDU:HCL_REF_AREA(1.0).REF_AREA </span>provides the link to the reference area hierarchy for OECD education data</p></td>
<td></td>
</tr>
<tr>
<td>HIER_LEVEL</td>
<td><p>Explicit specification of the hierarchical level of a code item</p>
<p>Reference to external standard: xkos:ClassificationLevel - property: xkos:xdepth url: <a href="http://data.europa.eu/ux2/nace2.1/sections">http://data.europa.eu/ux2/nace2.1/sections</a></p>
<p>text en:sections</p></td>
<td>Code item</td>
<td></td>
<td><p>&lt;hierarchical level&gt;</p>
<p><em>Example:</em></p>
<p>1</p></td>
<td></td>
</tr>
<tr>
<td>SHORT_LABEL</td>
<td>A short label, typically for dissemination purposes where long labels are sometimes not appropriate for presentation in tables where space is an important parameter (generally less than 40 or 50 characters)</td>
<td>Artefact, or Concept, or Item in an Item Scheme</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p></td>
<td><p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">[Official French label “Transformation et conservation de la viande de boucherie” is shortened to] fr:Transf. &amp; conserv. viande de boucherie</span></p>
<p><span style="color:#5B9BD5">In Codelist=IMF:CL_AREA(1.13) </span><br />
<span style="color:#5B9BD5">Code 4J837 European Union Intellectual Property Office has a Short_Label</span></p>
<p><span style="color:#5B9BD5">EN:EUIPO</span></p></td>
<td></td>
</tr>
<tr>
<td>EXPLAN_LABEL</td>
<td>An explanatory text that specifies “other” and similar categories. An example is the Combined Nomenclature classification where the many codes labelled “other” are complemented by a verbose text describing in detail the content of the code item</td>
<td>Item in an Item Scheme, mapping to Representation Maps</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p></td>
<td><p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">[EU Combined Nomenclature official label for code 3824 99 57 reads “Other”, which is not very informative for the user; instead the EXPLAN_LABEL reads] en:Cartridges and refills, filled, for electronic cigarettes, and preparations for use in the cartridges and refills, not containing nicotine or its salts, ethers, esters or other derivatives thereof</span></p></td>
<td></td>
</tr>
<tr>
<td>EXPLAN_CONSOL</td>
<td>Explanatory notes. An explanatory text to be used when objects included in and excluded from a classification position are consolidated, i.e. are presented together. Reference to external standard: skos:scopeNote</td>
<td>Item in an Item Scheme, mapping to Representation Maps</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p></td>
<td><p><span style="color:#5B9BD5">Example (from the US NAICS classification):</span></p>
<p><span style="color:#5B9BD5">en:Industries in the Food Manufacturing subsector transform livestock and agricultural products into products for intermediate or final consumption. […] The food products manufactured in these establishments are typically sold to wholesalers or retailers for distribution to consumers, but establishments primarily engaged in retailing bakery and candy products made on the premises not for immediate consumption are included. Establishments primarily engaged in manufacturing beverages are classified in Subsector 312, Beverage and Tobacco Product Manufacturing.</span></p></td>
<td></td>
</tr>
<tr>
<td>EXPLAN_INCLUDES</td>
<td>Explanatory notes. Description of those things known specifically to be included in the concept. Synonyms Typical labels for such explanatory notes: "This class includes", "This category includes", "This position includes", "Includes", etc. Reference to external standard: xkos:inclusionNote or xkos:coreContentNote (if  EXPLAN_INCLUDES_ALSO available)</td>
<td>Item in an Item Scheme, mapping to Representation Maps</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p></td>
<td><p><span style="color:#5B9BD5">Example (from ISIC Rev. 4 explanatory notes to code 2520 - Manufacture of weapons and ammunition):</span></p>
<p><span style="color:#5B9BD5">en: This class includes:</span></p>
<ul>
<li><p><span style="color:#5B9BD5">manufacture of heavy weapons (artillery, mobile guns, rocket launchers, torpedo tubes, heavy machine guns)</span></p></li>
<li><p><span style="color:#5B9BD5">manufacture of small arms (revolvers, shotguns, light machine guns)</span></p></li>
<li><p><span style="color:#5B9BD5">manufacture of air or gas guns and pistols</span></p></li>
<li><p><span style="color:#5B9BD5">manufacture of war ammunition</span></p></li>
</ul></td>
<td></td>
</tr>
<tr>
<td>EXPLAN_CASELAW</td>
<td>Explanatory notes. Indication that a decision on the classification has been made by the ad hoc Committee (concept generally described as “ruling”, “classification opinion”, classification decision; caselaw). : Reference to external standardxkos:caseLaw. The difference between caselaws and traditional explanatory notes is that caselaws are adopted during the time period between two official versions of a specific classification and have thus a slightly different status (e.g. from a legal viewpoint)</td>
<td>Item in an Item Scheme</td>
<td><p>&lt;language&gt;:&lt;content&gt;,</p>
<p>&lt;language&gt;:&lt;content&gt;,…</p>
<p>Example (from NACE Rev. 2 caselaw to code 01.62):</p>
<p>en:Automated egg hatching for poultry - Operation of livestock management systems]</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td>EXPLAN_INCLUDES_ALSO</td>
<td>Explanatory notes. Description of those things which can be considered as borderline cases and are generally based on consensus rather than strict methodological principles (e.g. classifying wooden shoes as handicraft rather than shoes). Typical labels for such explanatory notes: "This class includes also", "This category includes also", "This position includes also ", "Includes also", etc. Reference to external standard: xkos:additionalContentNote</td>
<td>Item in an Item Scheme</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p></td>
<td><p><span style="color:#5B9BD5">Example (from ISIC Rev. 4 explanatory notes to code 2520 - Manufacture of weapons and ammunition):</span></p>
<p><span style="color:#5B9BD5">en:This class also includes:</span></p>
<ul>
<li><p><span style="color:#5B9BD5">manufacture of hunting, sporting or protective firearms and ammunition</span></p></li>
<li><p><span style="color:#5B9BD5">manufacture of explosive devices such as bombs, mines and torpedoes</span></p></li>
</ul></td>
<td></td>
</tr>
<tr>
<td>EXPLAN_EXCLUDES</td>
<td>Explanatory notes. Description of those things which are explicitly excluded from a category. Typical labels for such explanatory notes: "This class excludes", "This category excludes", "This position excludes", "Excludes", etc. Reference to external standards: xkos:exclusionNote</td>
<td>Item in an Item Scheme</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p></td>
<td><p><span style="color:#5B9BD5">Example (from ISIC Rev. 4 explanatory notes to code 2520 - Manufacture of weapons and ammunition):</span></p>
<p><span style="color:#5B9BD5">en:This class excludes:</span></p>
<ul>
<li><p><span style="color:#5B9BD5">manufacture of percussion caps, detonators or signalling flares, see 2029</span></p></li>
<li><p><span style="color:#5B9BD5">manufacture of cutlasses, swords, bayonets etc., see 2593</span></p></li>
</ul></td>
<td></td>
</tr>
<tr>
<td>MAP_REFER</td>
<td>A reference to a classification mapping or transformation, e.g. an SDMX Structure Map. Reference to external standard: skos:mappingRelation (skos:broadMatch, skos:narrowMatch, skos:closeMatch, skos:exactMatch or skos:relatedMatch)</td>
<td>Codelist, Concept Scheme, or another Item Scheme</td>
<td></td>
<td><span style="color:#5B9BD5">Id of an ItemSchemeMap returned by the Annotation URL</span></td>
<td><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></td>
</tr>
<tr>
<td>COMP_RULE</td>
<td>Code item composition rule. For example, for code A the composition rule may be “A1+A2” where A1 and A2 are other codes in the same Codelist</td>
<td>An Item in an Item Scheme</td>
<td></td>
<td><p>&lt;content&gt;</p>
<p><em>Example:</em></p>
<p>A1+A2</p></td>
<td></td>
</tr>
<tr>
<td>FOLLOWS</td>
<td><p>A reference used to express the succession in time of Item Schemes.</p>
<p>For example, NACE Rev. 2 is the successor of NACE Rev. 1.1</p>
<p>Reference to external standard: skos:ConceptScheme - property: xkos:follows </p></td>
<td>Codelist or Item Scheme</td>
<td></td>
<td></td>
<td><p><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></p>
<p><em>Example:</em></p>
<p>(CL_REGIONAL 3.1.1 follows CL_REGIONAL 3.1):</p>
<p><a href="https://registry.sdmx.org/ws/public/sdmxapi/rest/codelist/ESTAT/CL_REGIONAL/3.1">https://registry.sdmx.org/ws/public/sdmxapi/rest/codelist/ESTAT/CL_REGIONAL/3.1</a></p></td>
</tr>
<tr>
<td>HAS_VARIANT</td>
<td><p>A reference used to express the relation between an Item Scheme and its variant(s).</p>
<p>Reference to external standard: skos:ConceptScheme - property: xkos:variant</p>
<p>For <em>Example:</em> CL_AREA has a variant CL_GEO</p></td>
<td>Codelist or Item Scheme</td>
<td></td>
<td></td>
<td><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></td>
</tr>
<tr>
<td>SUPERSEED</td>
<td><p>A reference to a previous version, if the current version obsoleted the previous one.</p>
<p>May be used in conjunction with DEPRECATED.</p>
<p>Reference to external standard: skos:ConceptScheme - property: xkos:supersedes</p></td>
<td>Codelist or Item Scheme, or an artefact</td>
<td></td>
<td></td>
<td><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></td>
</tr>
<tr>
<td>FAMILY_LABEL</td>
<td><p>Label of the Classification Family (e.g. NACE, ISIC)</p>
<p>Reference to external standard: skos:ConceptScheme - property: xkos:belongsTo</p>
<p>label of the classification</p></td>
<td>Codelist or Item Scheme</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">en:NACE</span></p></td>
<td></td>
<td><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></td>
</tr>
<tr>
<td>COVERAGE_LABEL</td>
<td><p>Label(s) of the item scheme’s coverage (e.g. National Accounts, Products, Activities, Occupations)</p>
<p>Reference to external standard: skos:ConceptScheme - property: xkos:covers</p>
<p><em>Examples:</em></p>
<p>URL &lt;http://eurovoc.europa.eu/56&gt; (National accounts)</p>
<p>URL &lt;http://publications.europa.eu/resource/authority/data-theme/REGI&gt; (Regions and Cities)</p></td>
<td>Codelist or Item Scheme</td>
<td><p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,</span></p>
<p><span style="color:#5B9BD5">&lt;language&gt;:&lt;content&gt;,…</span></p>
<p><em><span style="color:#5B9BD5">Example:</span></em></p>
<p><span style="color:#5B9BD5">En:national accounts</span></p></td>
<td></td>
<td><span style="color:#5B9BD5">See section URL value defaults and specific locale values.</span></td>
</tr>
<tr>
<td>GEO_FEATURE_SET</td>
<td><p>In Codelists, transmits GeoFeature values.</p>
<p>Example for  NUTS ID BE23<br />
url:<a href="http://data.europa.eu/nuts/geometry/2xr1qiv9">http://data.europa.eu/nuts/geometry/2xr1qiv9</a></p></td>
<td>Code in a Codelist. The Codelist must have an annotation attached with AnnotationType=GEO_TYPE_GEOGRAPHIC</td>
<td></td>
<td>A set of points defining a feature following the 1363 ISO/IEC 13249-3:2016 standard to conform Well-known Text (WKT) for the 1364 representation of geometries. See SDMX STANDARDS: SECTION 6 for further information on the format.</td>
<td></td>
</tr>
<tr>
<td>GEO_TYPE_GEOGRAPHIC</td>
<td>Indicates that a codelist contains GeoFeature values via the GEO_FEATURE_SET annotation.</td>
<td>Codelist</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>LEGAL_BASIS</td>
<td><p>Indicates that the Legislation on which the codelist/nomenclature is based.</p>
<p>Example for NACE Rev.2.1</p>
<p>url: <a href="http://data.europa.eu/eli/reg_del/2023/137/oj">http://data.europa.eu/eli/reg_del/2023/137/oj</a></p></td>
<td>Codelist</td>
<td></td>
<td></td>
<td><span style="color:#5B9BD5">http://data.europa.eu/eli/reg_del/2023/137/oj</span></td>
</tr>
</tbody>
</table>

# Concept Scheme SDMX:CS_ANNOT

The Concept Scheme for standard Annotations will have the Maintenance Agency SDMX and will describe the following properties for each Annotation. For the information represented by Annotations, the value is in AnnotationTitle apart from the URL property where it is in AnnotationURL.

| Property | Representation in Concept | Description |
|----|:---|----|
| Code | Concept Id | The Annotation Type column, e.g. NOT_DISPLAYED, EXCLUDES |
| Name | Concept Name | Short description of the standard Annotation derived from the “Use case” column |
| Representation | Concept Core Representation | Allowable type or format for the Annotation |
| Description | Concept Description | The information in the “Use case” column. Possible to add more contextual information. Specific details can be described here, such as if the value should be in AnnotationText or AnnotationTitle |
| Artefact(s) | Annotation Type: Artefact(s) | The information in the “Where to attach” column |
| URL | Annotation Type: URL | The Annotation URL column. The value is in URL |

## Example of a Concept

| **Concept Id** | NOT_DISPLAYED |
|:--:|----|
| **Concept Name** | Used to hide components or their values in the presentation |
| **Concept Core Representation** | /TextFormat@textType="String" |
| **Concept Description** | To hide dimensions and attributes in a display (e.g. a table). For example, if they have only one allowed, available or selected value |
| **Concept: Annotation: Type: Artefact(s)** | Either a Dataflow or DSD, or an item in an item scheme |

### SDMX-ML of the Example

<span style="color:#000096">\<str:Concept</span><span style="color:#F5844C"> id</span><span style="color:#FF8040">=</span><span style="color:#993300">"NOT_DISPLAYED"</span><span style="color:#000096">\></span>  
<span style="color:#000096">\<com:Annotations\></span>  
<span style="color:#000096">\<com:Annotation\></span>  
<span style="color:#000096">\<com:AnnotationTitle\></span>Either a Dataflow or DSD, or an item in an item scheme<span style="color:#000096">\</com:AnnotationTitle\></span>  
<span style="color:#000096">\<com:AnnotationType\></span>Artefact(s)<span style="color:#000096">\</com:AnnotationType\></span>  
<span style="color:#000096">\</com:Annotation\></span>  
<span style="color:#000096">\</com:Annotations\></span>  
<span style="color:#000096">\<com:Name</span><span style="color:#F5844C"> xml:lang</span><span style="color:#FF8040">=</span><span style="color:#993300">"en"</span><span style="color:#000096">\></span>Used to hide components or their values in the presentation<span style="color:#000096">\</com:Name\></span>  
<span style="color:#000096">\<com:Description</span><span style="color:#F5844C"> xml:lang</span><span style="color:#FF8040">=</span><span style="color:#993300">"en"</span><span style="color:#000096">\></span>To hide dimensions and attributes in a display (e.g. a table). For example, if they have only one allowed, available or selected value<span style="color:#000096">\</com:Description\></span>  
<span style="color:#000096">\<str:CoreRepresentation\></span>  
<span style="color:#000096">\<str:TextFormat</span><span style="color:#F5844C"> textType</span><span style="color:#FF8040">=</span><span style="color:#993300">"String"</span><span style="color:#000096">/\></span>  
<span style="color:#000096">\</str:CoreRepresentation\></span>  
<span style="color:#000096">\</str:Concept\></span>

# References

- [Formalization of the Structure and Content of Statistical Classifications](https://urldefense.com/v3/__https:/eur02.safelinks.protection.outlook.com/?url=https*3A*2F*2Furldefense.com*2Fv3*2F__https*3A*2Feur02.safelinks.protection.outlook.com*2F*3Furl*3Dhttps*3A*2F*2Fec.europa.eu*2Feurostat*2Framon*2Fmiscellaneous*2Fgen_intro_classif_files*2FStructure_and_content_of_classifications_version_1_0_October_2019.docx*26data*3D02*7C01*7CDavid.BARRACLOUGH*40oecd.org*7Cf9cb429291334e5170cb08d80c883aeb*7Cac41c7d41f61460db0f4fc925a2b471c*7C0*7C1*7C637273126543303645*26sdata*3Dl01*2BEX3SNWREH*2FElV3r9Ld*2BG49l7ouvFi7pqAGYg2Ss*3D*26reserved*3D0__*3BJSUlJSUlJSUlJSUlJSUlJSUlJSU!!DOxrgLBm!Q_cL04DGMBYhHfuPQVRMMCKao1C3QuaoJxBTxO4_mSKNMGfLjmV2UTCtAhTDvbMAZtNzrTZ3*24&data=02*7C01*7CDavid.BARRACLOUGH*40oecd.org*7Ca70a73c696814b06406408d80d1d9336*7Cac41c7d41f61460db0f4fc925a2b471c*7C0*7C1*7C637273768055440921&sdata=r4CVvCdYBIU39XMN0qNmt*2FC9FIS7AnXrzYcjuzDe0Dc*3D&reserved=0__;JSUlJSUlJSUlJSoqKioqKioqJSUqKioqKioqKiUlKioqKiUlJSUlJSUlJSUlJSUl!!DOxrgLBm!RCGOp-FMBfmiP7CvEwdSAhL4XCil-vey-z32n6uxoCDXVTN7rXWXG442IZgqwpmM4wKQq908$)

- [SDMX Global Registry](https://registry.sdmx.org/overview.html)

- 

- [SDMX Glossary 2.1](https://sdmx.org/wp-content/uploads/SDMX_Glossary_version_2_1-Final-2.docx)SDMX Standards, “[Information Model: UML Conceptual Design](https://sdmx.org/wp-content/uploads/SDMX_2_0_SECTION_02_InformationModel.pdf)”, version 2.1

- [SKOS Specification](https://www.w3.org/TR/2009/REC-skos-reference-20090818/)

- [XKOS Specification](https://ddialliance.org/Specification/XKOS/1.2/OWL/xkos.html)

<!-- footnotes -->

------------------------------------------------------------------------

<a id="fn-1"></a><sup>1</sup> The technical standard does not enumerate the annotation types, however this guideline provides a recommended enumeration or controlled vocabulary

<a id="fn-2"></a><sup>2</sup> International Standard Industrial Classification of All Economic Activities

<a id="fn-3"></a><sup>3</sup> Central Product Classification
