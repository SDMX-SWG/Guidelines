---
title: "Guidelines for SDMX Concept Roles"
source_url: https://sdmx.org/wp-content/uploads/Guidelines_for_SDMx_Concept_Roles_v1.1.docx
source_file: Guidelines_for_SDMx_Concept_Roles_v1.1.docx
source_sha256: 80abd2eb0425bdc799e5585fdc4a8d5e6f957326b4baf97d2dd500187d94d0ca
source_last_modified: "Thu, 21 Jul 2022 23:29:12 GMT"
retrieved: 2026-09-24
licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)
conversion: DOCX -> Markdown, wording and structure unchanged; see NOTICE.md for the list of changes
---
SDMX GUIDELINES

GUIDELINES FOR  
SDMX CONCEPT ROLES

VERSION 1.1

# Contents

[Document History](#_Toc2084466)

[Introduction](#introduction)

[Cross-domain Concept Scheme for Concept Roles in SDMX 2.1](#cross-domain-concept-scheme-for-concept-roles-in-sdmx-21)

[Concept roles in SDMX 2.0](#concept-roles-in-sdmx-20)

[Appendix on implementation examples](#appendix-on-implementation-examples)

[SDMX 2.0: Implementation example](#sdmx-20-implementation-example)

[SDMX 2.1: Implementation example](#sdmx-21-implementation-example)

<a id="_Toc2084466"></a>

# Document History

| **Version** | **Date** | **Comment** |
|:---|:---|:---|
| 1.0 | 26/2/2019 | Initial version |
| 1.1 | 2/2/2021 | Added COUNT concept role; SDMX 2.1 concept roles apply to SDMX 3.0 |

# Introduction

This document describes SDMX Concept Roles and their use, proposes a cross-domain Concept scheme that defines the set of concept roles (for SDMX 2.1), and gives examples on concept role implementation in both SDMX 2.0 and SDMX 2.1.

A concept role gives a particular context to a concept for easy and systematic interpretation by machine processing and visualization tools. For example, the concepts REPORTING_AREA and COUNTERPART_AREA are different concepts but they are both geographical characteristics, therefore they can be associated with the same concept role ID: “GEO”. This allows visualization systems to interpret these concepts as geographical data in order to generate maps.

A concept can have more than one role; for example, a concept may have both a geographical and entity role (see the table 1 for a description of these roles). Also, concept roles can be defined and referenced outside of the cross-domain concept role set.

The implementation of concept roles is different in versions 2.0 and 2.1 of the SDMX technical standard. The SDMX 2.1 concept roles also apply to SDMX 3.0.

Examples for both versions are included in the Appendix.

# Cross-domain Concept Scheme for Concept Roles in SDMX 2.1

The concept roles are themselves concepts, and a cross-domain concept scheme for concept roles is described in Table 1 below. A concept (in a DSD) can acquire one or more concept roles.

Note: The roles marked with “\*” have been included for compatibility with SDMX 2.0. Some of the SDMX 2.0 concept roles have been excluded from this 2.1 list for these reasons:

- Other mechanisms exist in SDMX 2.1 to distinguish the concepts, for example for time period and measure;

- No use cases could be found for the concept roles. For example for identity and nonObsTime.

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 16%" />
<col style="width: 22%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><strong>Id</strong></th>
<th style="text-align: center;"><strong>Name</strong></th>
<th style="text-align: center;"><strong>Definition</strong></th>
<th style="text-align: center;"><strong>Context</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><strong>COMMENT</strong></td>
<td>Comment</td>
<td>Descriptive text which can be attached to data or metadata.</td>
<td style="text-align: left;"><p>Used for concepts that contain descriptive information about the data.</p>
<p>Examples include footnotes, notes, reference metadata within the data message.</p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>ENTITY*</strong></td>
<td>Entity</td>
<td>Describes the subject of the data set (e.g. a country).</td>
<td style="text-align: left;">Identifies the subject to whom the data refers (e.g. the reporting agent for primary reporting, the country for secondary reporting)</td>
</tr>
<tr>
<td style="text-align: center;"><strong>FLAG</strong></td>
<td>Flag</td>
<td>Coded attribute in a data set that represents qualitative information for the cell or partial key (e.g. series) value.</td>
<td style="text-align: left;"><p>Allows to display flags close to the observation value or partial key in statistical tables.</p>
<p>Examples of qualitative information that can be exchanged via a flag are "estimated value", "break in series", “confidential”.</p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>FREQ*</strong></td>
<td>Frequency</td>
<td>Time interval at which the source data are collected.</td>
<td style="text-align: left;"><p>Identifies the observation’s time interval for processing and/or presenting on a graph’s time axis.</p>
<p>For example, if a data series has a constant time interval between its observations, this interval determines the frequency of the series (e.g. monthly, quarterly, yearly). “Frequency” - also called “periodicity” - may refer to several stages in the production process, e.g. in data collection or in data dissemination. (e.g., a time series could be available at annual frequency but the underlying data are compiled monthly). Therefore, “Frequency” can be broken down into “Frequency - data collection” and “Frequency - data dissemination”.</p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>GEO</strong></td>
<td>Geographical</td>
<td>Geographic area to which the measured statistical phenomenon relates.</td>
<td style="text-align: left;">Used for concepts which refer to geographical or political groups of countries or regions within a country. It can allow for the representation of geographical information on maps or graphs.</td>
</tr>
<tr>
<td style="text-align: center;"><strong>OPERATION</strong></td>
<td>Statistical operation</td>
<td>Signifies statistical operations have been done on the observations.</td>
<td style="text-align: left;"><p>Allows systems to distinguish operation concepts from other concepts (entities, variables) which may be prioritised differently in navigation, presentation and processing.</p>
<p>An example is to indicate that this concept codes information such as seasonal adjustment or time transformations.</p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>VARIABLE</strong></td>
<td>Variable<sup><a href="#fn-1" id="fnref-1">1</a></sup></td>
<td>Characteristic of a unit being observed that may assume more than one of a set of values to which a numerical measure or a category from a classification can be assigned.</td>
<td style="text-align: left;"><p>Used to distinguish concepts that represent statistical variables (e.g. sex, age) from concepts that are strictly related to the operation performed over data (e.g. Adjustment).</p>
<p>This identification of this concept(s) is crucial for statisticians as it is very important in survey data to identify variables. For example, in a DSD representing the GDP of a country we will have the reference area, the unit of measure of the GDP and the value of the GDP. The unit of measure is a concept used to understand or interpret data but it is not a statistical variable, which are reference area and the GDP observed value. The concept of variable is emphasized strongly in GSIM but not in SDMX, and the inclusion of this information as a Concept role, incorporates this information into SDMX.</p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>COUNT</strong></td>
<td>Count</td>
<td>Indicates a counter for unique items in a dataset</td>
<td style="text-align: left;"><p>Used when a unique (or unique in conjunction with other other series key fields) artificial key is required in datasets. An example usage is for generating and processing a reporting template and there is no guarantee that the key field values for each observation will be unique. Each observation would have a different COUNT concept value to guarantee that the observation key values are unique.</p>
<p>A concept with this role would usually be typed as Integer and the observation values would increment (1,2,3,…). However, other data types could be used as long as the concept serves the purpose of making the dataset’s observation key values unique.</p></td>
</tr>
</tbody>
</table>

*Table 1. Cross-domain concept scheme for concept roles*

If other cross-domain roles are required, the SDMX SWG should be contacted to update the concept scheme with new role proposals. Alternatively, domain or implementation-specific concept roles may be created. However, these would be difficult to use for inter-agency exchange and are therefore not recommended.

For technical implementation details please see the appendix below.

# Concept roles in SDMX 2.0

In SDMX 2.0, the list of concept roles is specified in the technical standard itself. In SDMX messages, a role is allocated to a concept by setting its role-specific xml attribute to **true.** Table 2 lists all of the xml attributes that can be specified as roles in SDMX 2.0.

| **Role type** | **Description** |
|:---|:---|
| **Frequency** | Identifies the Concept that plays the role of frequency: *time interval at which observations occur over a given time period*<sup><a href="#fn-2" id="fnref-2">2</a></sup> |
| **Count** | Identifies the Concept that plays the role of an identifier where the identifier is taken from a known system of counts |
| **measureType** | Identifies the Concept that plays the role of identifying a type of measure |
| **Entity** | Identifies the Concept that plays the role of the subject to whom the data refers (e.g. the reporting agent for primary reporting, the country for secondary reporting) |
| **Time** | Identifies the Concept that specifies the time of the observation of the primaryMeasure |
| **nonObsTime** | Identifies the Concept that plays the role of a date/time identifier in the KeyFamily which is not related to the time of the observation |
| **primaryMeasure** | Identifies the Concept that plays the role of the observation in a time series |
| **Identity** | Identifies the Concept that plays the role of an identifier which is taken from a known scheme of identifiers |

*Table 2. List of roles in SDMX 2.0*

For example, if a dimension represents the frequency, the attribute *IsFrequencyDimension* should be set to ’true’ in the data structure definition.

<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 40%" />
<col style="width: 1%" />
<col style="width: 40%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><strong>Role type</strong></th>
<th colspan="2" style="text-align: center;"><strong>xml attribute<br />
associated to a Dimension</strong></th>
<th style="text-align: center;"><strong>xml attribute<br />
associated to an Attribute</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Frequency</strong></td>
<td colspan="2" style="text-align: center;">isFrequencyDimension</td>
<td style="text-align: center;">isFrequencyAttribute</td>
</tr>
<tr>
<td><strong>Count</strong></td>
<td colspan="2" style="text-align: center;">isCountDimension</td>
<td style="text-align: center;">isCountAttribute</td>
</tr>
<tr>
<td><strong>measureType</strong></td>
<td colspan="2" style="text-align: center;">isMeasureDimension</td>
<td style="text-align: center;">isMeasureAttribute</td>
</tr>
<tr>
<td><strong>Entity</strong></td>
<td colspan="2" style="text-align: center;">isEntityDimension</td>
<td style="text-align: center;">isEntityAttribute</td>
</tr>
<tr>
<td><strong>Time</strong></td>
<td colspan="3"
style="text-align: center;"><strong><span style="color:#FF0000">Specified
by the standard with the xml element “TimeDimension”</span></strong></td>
</tr>
<tr>
<td><strong>nonObsTime</strong></td>
<td style="text-align: center;">isNonObsTimeDimension</td>
<td colspan="2" style="text-align: center;">isNonObsTimeAttribute</td>
</tr>
<tr>
<td><strong>primaryMeasure</strong></td>
<td colspan="3"
style="text-align: center;"><strong><span style="color:#FF0000">Specified
by the standard with the xml element “PrimaryMeasure”</span></strong></td>
</tr>
<tr>
<td><strong>Identity</strong></td>
<td style="text-align: center;">isIdentityDimension</td>
<td colspan="2" style="text-align: center;">isIdentityAttribute</td>
</tr>
</tbody>
</table>

*Table 3. SDMX 2.0 xml attributes to be specified for a role*

In SDMX 2.0 there are some restrictions in the use of roles:

- only one concept among all dimensions and attributes can have the frequency role;

- only one concept among all dimensions and attributes can have the entity role;

- Frequency, Count, Entity, nonObsTime and Identity roles, are mutually exclusive when applied to dimensions;

- Frequency and Entity roles are mutually exclusive when applied to attributes.

# Appendix on implementation examples

This appendix shows how concept roles can be represented in SDMX messages in SDMX 2.0 and SDMX 2.1.

## SDMX 2.0: Implementation example

Note that SDMX 2.0 Concept roles are fixed according to the technical standards; they are also described in this guideline.

In the Demography DSD example shown below, dimensions: “FREQ”, “COUNTRY” and “DEMO” have been assigned the “frequency dimension”, “entity dimension”, and “measure dimension” roles. This is expressed by setting the “isFrequencyDimension”, “isEntityDimension” and “isMeasureDimension” XML attributes equal to “true” to the corresponding dimensions.

<span style="color:#244061">\<structure:KeyFamily </span><span style="color:#FF0000">id</span>="DEMOGRAPHY" <span style="color:#FF0000">agencyID</span>="ESTAT" <span style="color:#FF0000">version</span>="2.1" <span style="color:#FF0000">isFinal</span>="true" <span style="color:#FF0000">validFrom</span>="2008-05-14"<span style="color:#244061">\></span>

<span style="color:#244061">\<structure:Name </span><span style="color:#FF0000">xml:lang</span>="en"\>Demography Rapid Questionnaire Data Structure Definition<span style="color:#244061">\</structure:Name\></span>

<span style="color:#244061">\<structure:Components\></span>

<span style="color:#244061"> \<structure:Dimension </span><span style="color:#FF0000">conceptRef</span>="FREQ" <span style="color:#FF0000">codelist</span>="CL_FREQ" <span style="color:#FF0000">codelistAgency</span>="ESTAT" <span style="color:#FF0000">codelistVersion</span>="1.0" <span style="color:#FF0000">conceptSchemeRef</span>="DEMO_CONCEPTS" <span style="color:#FF0000">conceptSchemeAgency</span>="ESTAT" <span style="color:#FF0000">conceptSchemeVersion</span>="2.0" <span style="color:#FF0000">crossSectionalAttachGroup</span>="true" **<span style="color:#FF0000">isFrequencyDimension</span>="true<span style="color:#244061">"</span>**<span style="color:#244061">/\></span>

<span style="color:#244061"> \<structure:Dimension </span><span style="color:#FF0000">conceptRef</span>="COUNTRY" <span style="color:#FF0000">codelist</span>="CL_COUNTRY" <span style="color:#FF0000">codelistAgency</span>="ESTAT" <span style="color:#FF0000">codelistVersion</span>="1.1" <span style="color:#FF0000">conceptSchemeRef</span>="DEMO_CONCEPTS" <span style="color:#FF0000">conceptSchemeAgency</span>="ESTAT" <span style="color:#FF0000">conceptSchemeVersion</span>="2.0" <span style="color:#FF0000">crossSectionalAttachGroup</span>="true" **<span style="color:#FF0000">isEntityDimension</span>="true"**<span style="color:#244061">/\></span>

<span style="color:#244061">\<structure:Dimension </span><span style="color:#FF0000">conceptRef</span>="SEX" <span style="color:#FF0000">codelist</span>="CL_SEX" <span style="color:#FF0000">codelistAgency</span>="ESTAT" <span style="color:#FF0000">codelistVersion</span>="1.0" <span style="color:#FF0000">conceptSchemeRef</span>="DEMO_CONCEPTS" <span style="color:#FF0000">conceptSchemeAgency</span>="ESTAT" <span style="color:#FF0000">conceptSchemeVersion</span>="2.0" <span style="color:#FF0000">crossSectionalAttachObservation</span>="true"<span style="color:#244061">/\></span>

<span style="color:#244061">\<structure:Dimension </span><span style="color:#FF0000">conceptRef</span>="DEMO" <span style="color:#FF0000">codelist</span>="CL_DEMO" <span style="color:#FF0000">codelistAgency</span>="ESTAT" <span style="color:#FF0000">codelistVersion</span>="1.0" <span style="color:#FF0000">conceptSchemeRef</span>="DEMO_CONCEPTS" <span style="color:#FF0000">conceptSchemeAgency</span>="ESTAT" <span style="color:#FF0000">conceptSchemeVersion</span>="2.0" **<span style="color:#FF0000">isMeasureDimension</span>="true"**<span style="color:#244061">/\></span>

<span style="color:#244061">………………</span>

<!-- figure: f01-roles-sdmx20 -->
<details>
<summary>Original figure</summary>

![Figure 1. XML excerpt of roles definition in SDMX 2.0 (original rendering, with the role attributes outlined)](images/f01-roles-sdmx20.png)

</details>

*Figure 1. XML excerpt of roles definition in SDMX 2.0*

## SDMX 2.1: Implementation example

Note that SDMX 2.0 Concept roles are flexible according to the technical standards; they are also described in this guideline.

The example below shows a role of “Variable” assigned to the dimension “ACCOUNTING_ENTRY” in the Balance of Payments DSD. The concept role is defined using the xml element: *ConceptRole* and the “VARIABLE” role is referenced in the cross-domain concept scheme “CONCEPT_ROLES”.

\<str:DataStructureComponents\>

\<str:DimensionList <span style="color:#FF0000">id</span>="DimensionDescriptor" <span style="color:#FF0000">urn</span>="urn:sdmx:org.sdmx.infomodel.datastructure.DimensionDescriptor=IMF:BOP(1.6).DimensionDescriptor"\>

......

\<str:Dimension <span style="color:#FF0000">id</span>="ACCOUNTING_ENTRY" <span style="color:#FF0000">urn</span>="urn:sdmx:org.sdmx.infomodel.datastructure.Dimension=IMF:BOP(1.6). ACCOUNTING_ENTRY"\>

\<str:ConceptIdentity\>

\<Ref id="ACCOUNTING_ENTRY" <span style="color:#FF0000">maintainableParentID</span>="CS_BOP" <span style="color:#FF0000">package</span>="conceptscheme" <span style="color:#FF0000">class</span>="Concept" agencyID="IMF" <span style="color:#FF0000">maintainableParentVersion</span>="1.6" /\>

\</str:ConceptIdentity\>

\<str:LocalRepresentation\>

…..

\</str:LocalRepresentation\>

**\<str:ConceptRole\>**

\<Ref <span style="color:#FF0000">id</span>="VARIABLE" <span style="color:#FF0000">maintainableParentID</span>="CONCEPT_ROLES" <span style="color:#FF0000">maintainableParentVersion</span>="1.0" <span style="color:#FF0000">agencyID</span>="SDMX" /\>

**\</str:ConceptRole\>**

\</str:Dimension\>

....

\</str:DimensionList\>

....

\<str:DataStructureComponents\>

<!-- figure: f02-variable-role-sdmx21 -->
<details>
<summary>Original figure</summary>

![Figure 2. XML example of “variable” concept role in SDMX 2.1 (original rendering, with outlines)](images/f02-variable-role-sdmx21.png)

</details>

*Figure 2. XML example of “variable” concept role in SDMX 2.1*

\<str:DataStructure <span style="color:#FF0000">id</span>="NA_MAIN" <span style="color:#FF0000">urn</span>="urn:sdmx:org.sdmx.infomodel.datastructure.DataStructure=ESTAT:NA_MAIN(1.1)" <span style="color:#FF0000">agencyID</span>="ESTAT" <span style="color:#FF0000">version</span>="1.1" <span style="color:#FF0000">isFinal</span>="true"\>

\<com:Name <span style="color:#FF0000">xml:lang</span>="en"\>NA Main Aggregates\</com:Name\>

\<str:DataStructureComponents\>

\<str:DimensionList\>

\<str:Dimension id="REF_AREA" <span style="color:#FF0000">urn</span>="urn:sdmx:org.sdmx.infomodel.datastructure.Dimension=ESTAT:NA_MAIN(1.5).REF_AREA" <span style="color:#FF0000">position</span>="3"\>

\<str:ConceptIdentity\>

\<Ref <span style="color:#FF0000">id</span>="REF_AREA" <span style="color:#FF0000">agencyID</span>="ESTAT" <span style="color:#FF0000">class</span>="Concept" <span style="color:#FF0000">package</span>="conceptscheme" maintainableParentVersion="1.5" <span style="color:#FF0000">maintainableParentID</span>="CS_NA"/\>

\</str:ConceptIdentity\>

\<str:LocalRepresentation\>

\<str:Enumeration\>

\<Ref <span style="color:#FF0000">id</span>="CL_AREA" <span style="color:#FF0000">version</span>="1.5" <span style="color:#FF0000">agencyID</span>="IMF" <span style="color:#FF0000">class</span>="Codelist" <span style="color:#FF0000">package</span>="codelist"/\>

\</str:Enumeration\>

\<str:EnumerationFormat <span style="color:#FF0000">textType</span>="String" <span style="color:#FF0000">maxLength</span>="5" <span style="color:#FF0000">minLength</span>="2"/\>

\</str:LocalRepresentation\>

**\<str:ConceptRole\>**

\<Ref <span style="color:#FF0000">id</span>="GEO" <span style="color:#FF0000">maintainableParentID</span>="CONCEPT_ROLES"<span style="color:#FF0000"> maintainableParentVersion</span>="1.0" <span style="color:#FF0000">agencyID</span>="SDMX" /\>

**\</str:ConceptRole\>**

**\<str:ConceptRole\>**

\<Ref <span style="color:#FF0000">id</span>="VARIABLE" <span style="color:#FF0000">maintainableParentID</span>="CONCEPT_ROLES"<span style="color:#FF0000"> maintainableParentVersion</span>="1.0" <span style="color:#FF0000">agencyID</span>="SDMX"/\>

**\</str:ConceptRole\>**

\</str:Dimension\>

....

\</str:DimensionList\>

....

\<str:DataStructureComponents\>

<!-- figure: f03-geo-role-sdmx21 -->
<details>
<summary>Original figure</summary>

![Figure 3. XML example of “geo” concept role in SDMX 2.1 (original rendering, with outlines)](images/f03-geo-role-sdmx21.png)

</details>

*Figure 3. XML example of “geo” concept role in SDMX 2.1*

<!-- footnotes -->

------------------------------------------------------------------------

<a id="fn-1"></a><sup>1</sup> <http://www1.unece.org/stat/platform/display/GSIMclick/Variable>

<a id="fn-2"></a><sup>2</sup> Source: "[SDMX Glossary](https://sdmx.org/wp-content/uploads/SDMX_Glossary_Version_2_0_October_2018.docx)", Version 2.0
