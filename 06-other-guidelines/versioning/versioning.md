---
title: "Guidelines on the Versioning of SDMX Artefacts"
source_url: https://sdmx.org/wp-content/uploads/Guidelines_on_versioning_v1_0.pdf
source_file: Guidelines_on_versioning_v1_0.pdf
source_sha256: 8ce43013c533dd4b5e5edd74f3ea9fa016f9bbcf25b0244eb3c2fed920c08eaf
source_last_modified: "Tue, 11 May 2021 07:58:38 GMT"
retrieved: 2026-09-24
licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)
conversion: PDF -> Markdown (structure read from the page layout), wording and structure unchanged; see NOTICE.md for the list of changes
---
**<span style="color:#000080">SDMX GUIDELINES</span>**

<span style="color:#000080">GUIDELINES ON THE</span> <span style="color:#000080">VERSIONING OF SDMX ARTEFACTS</span>

<span style="color:#000080">V</span><span style="color:#000080">ERSION</span> <span style="color:#000080">1.0</span>

<span style="color:#000080">15/11/2015</span>

© SDMX 2015<br><span style="color:#0000FF">http://www.sdmx.org/</span>

# Contents

[1. Introduction](#1-introduction)

[2. Numbering system and syntax](#2-numbering-system-and-syntax)

[3. Criterion for incrementing the version number](#3-criterion-for-incrementing-the-version-number)

[a. Description of backward/forward compatibility](#a-description-of-backwardforward-compatibility)

[b. Cost-benefit analysis for a major version change](#b-cost-benefit-analysis-for-a-major-version-change)

[c. Synthesis based on the above syntax and criterion](#c-synthesis-based-on-the-above-syntax-and-criterion)

[4. Types of artefact changes and their versioning impact](#4-types-of-artefact-changes-and-their-versioning-impact)

[5. How versioning works for inter-dependent artefacts](#5-how-versioning-works-for-inter-dependent-artefacts)

[a. Impact on parent artefact when child artefact version changes](#a-impact-on-parent-artefact-when-child-artefact-version-changes)

[b. Addition or removal of referenced artefacts](#b-addition-or-removal-of-referenced-artefacts)

[6. Appendix - Examples](#6-appendix---examples)

# 1. Introduction

This document aims at providing guidelines on how to version SDMX artefacts inspired by "*semantic versioning*", i.e. a formal convention for specifying compatibility between the different versions of a “versionable” artefact (a SDMX artefact that has an associated version number). There are slight differences when compared to semantic versioning regarding the numbering and the definition of the criterion triggering the changes in numbering.

A three-component versioning system is proposed, with the third component being optional. The criterion for deciding which component is impacted is the severity of the change.

Versioning is central to SDMX because it guarantees the stability of references to SDMX artefacts. This is of the utmost importance given the sometimes strong dependencies between artefacts, especially in Data Structure Definitions (DSDs).

The document contains three main recommendations:

- numbering system and syntax;
- types of artefact changes and their versioning impact;
- how versioning works for inter-dependent artefacts.

The document’s appendix contains examples of several types of changes and their versioning impact.

# 2. Numbering system and syntax

The proposed versioning system is based on the Semantic Versioning 2.0 specification<sup><a href="#fn-1" id="fnref-1">1</a></sup>, namely:

`MAJOR.MINOR.PATCH`<sup><a href="#fn-2" id="fnref-2">2</a></sup>

However, as the "patch" component will generally not be used extensively in SDMX, it is proposed to limit the coding to `MAJOR.MINOR` as long as no patches are implemented. Concretely, this means that version number 2.1.0 will be abridged to 2.1 as long as no patch is implemented. When a patch is implemented, the version number then becomes 2.1.1. At subsequent `MAJOR` change in the versioning the `PATCH` component will disappear (2.4.7 → 3.0).

The most severe change has always precedence over other types of changes. For example, if the `MAJOR` and `MINOR` parts of the version number are impacted by changes, only the `MAJOR` component will be impacted. This means that version 3.2.1 will become 4.0.

When an artefact is published in production for the first time, the version number of the artefact should be 1.0.

# 3. Criterion for incrementing the version number

The criterion for deciding which component is impacted is the severity of the change, i.e. the possibility of maintaining backward and forward compatibility between the different versions of an artefact.

## a. Description of backward/forward compatibility

Backward compatibility is defined as: An item (e.g. a data message) that was produced and validated with the previous version of an artefact (e.g. a DSD) can still be successfully validated using the newest version of the same artefact. For example, a data message produced and validated with a DSD version 1.1 is still valid against the same DSD (same id and Agency) upgraded to version 1.2.

Forward compatibility is defined as: An item (e.g. a data message) that is produced and validated with the new version of an artefact (e.g. a DSD) can also be validated using the previous version of the same artefact.  For example, a data message produced and validated with a DSD version 1.1 is also valid against the same DSD (same id and Agency) having version 1.0 (an earlier version).

Given the syntax specified above, namely `MAJOR.MINOR.PATCH`, implementers should increment the:

- MAJOR version when changes are not backward compatible;
- MINOR version when changes are backward but not forward compatible;
- PATCH version when minor changes (e.g. text clarifications, correction of typos) are both backward and forward compatible.

## b. Cost-benefit analysis for a major version change

The cost of imposing a “major” change should be balanced against the benefit of retaining backward compatibility, for example by not deleting codes used in existing data exchanges or by deleting or replacing codes only through a concerted effort of all data exchange partners.

## c. Synthesis based on the above syntax and criterion

<table>
<tr><th><strong>Change Severity</strong></th><th><strong>Version Impact</strong></th><th><strong>Description</strong></th><th><strong>Example</strong></th></tr>
<tr><td><strong>Major</strong></td><td><strong><span style="color:#FF0000">+</span>.0</strong></td><td><strong>Neither</strong> backward <strong>nor</strong> forward compatibility</td><td><strong>1.2</strong> → <strong>2.0</strong></td></tr>
<tr><td><strong>Minor</strong></td><td><strong>N.<span style="color:#FF0000">+</span></strong></td><td>Backward <strong>but not</strong> forward compatibility</td><td><strong>1.0</strong> → <strong>1.1</strong></td></tr>
<tr><td><strong>Patch</strong></td><td><strong>N.M.<span style="color:#FF0000">+</span></strong></td><td>Backward <strong>and</strong> forward compatibility</td><td><strong>1.2</strong> → <strong>1.2.1</strong></td></tr>
</table>

# 4. Types of artefact changes and their versioning impact

As a general rule insignificant changes (e.g. textual clarifications or typos) will result in an increment of the patch component of the versioning system (i.e. N.M.**<span style="color:#C00000">+</span>**).

<table>
<tr><th colspan="3"><strong>CODE LIST (CL)</strong></th></tr>
<tr><th><strong>Type of Change</strong></th><th><strong>Impact</strong></th><th><strong>Comments</strong></th></tr>
<tr><td><strong>Addition into an existing CL of one or more new codes not having the CodeList:Code:ParentCode attribute</strong></td><td><strong>Minor</strong>: <strong>N.<span style="color:#C00000">+</span></strong><sup><a href="#fn-3" id="fnref-3">(3)</a></sup></td><td>Data exchanged/disseminated using the old CL can still be exchanged/disseminated using the new CL</td></tr>
<tr><td><strong>Addition of one or more new hierarchies represented using the CodeList:Code:ParentCode attribute (not using the Hierarchical Code List artefact)</strong></td><td><strong>Minor</strong>: <strong>N.<span style="color:#C00000">+</span>(</strong>3)</td><td>Data exchanged/disseminated using the old CL can still be exchanged/disseminated using the new CL as already existing hierarchies still represent the same aggregations</td></tr>
<tr><td><strong>Addition of one or more new codes into existing hierarchies represented using the CodeList:Code:ParentCode attribute (not using the Hierarchical Code List artefact)</strong></td><td><strong>Major</strong>: <strong><span style="color:#C00000">+</span>.0</strong></td><td>After the change, the parent code for the changed hierarchy does not represent the same aggregation any more, thus resulting in a break in backward compatibility</td></tr>
<tr><td><strong>Aggregation, disaggregation, reorganisation or removal of one or more codes</strong></td><td><strong>Major</strong>: <strong><span style="color:#C00000">+</span>.0</strong></td><td>Data exchanged/disseminated using an old version of the CL can no longer be exchanged/disseminated using the new version of the CL</td></tr>
</table>

<table>
<tr><th colspan="3"><strong>HIERARCHICAL CODE LIST (HCL)</strong></th></tr>
<tr><th><strong>Type of Change</strong></th><th><strong>Impact</strong></th><th><strong>Comments</strong></th></tr>
<tr><td><strong>Addition of new hierarchies in the HCL. Existing hierarchies are unaffected</strong></td><td><strong>Minor</strong>: <strong>N.<span style="color:#C00000">+</span></strong><sup><a href="#fn-3" id="fnref-3-2">(3)</a></sup></td><td>Data represented using the old HCL can still be represented using the new HCL</td></tr>
<tr><td><strong>Addition of codes into existing hierarchies in the HCL. Existing hierarchies are thus affected</strong></td><td><strong>Major</strong>: <strong><span style="color:#C00000">+</span>.0</strong></td><td>The HCL resulting from this change does not represent the same aggregation any more, thus breaking backward compatibility</td></tr>
<tr><td><strong>Removal of one or more codes in the HCL or removal of one or more codes in the referenced code lists</strong></td><td><strong>Major</strong>: <strong><span style="color:#C00000">+</span>.0</strong></td><td>Data represented using the old HCL can no longer be represented using the new HCL, thus resulting in a break in backward compatibility</td></tr>
<tr><td><strong>Addition, modification or removal of one or more hierarchical levels</strong></td><td><strong>Major: <span style="color:#C00000">+</span>.0</strong></td><td>The reorganisation of codes within hierarchies has a significant impact on the code aggregations</td></tr>
</table>

<table>
<tr><th colspan="3"><strong>CONCEPT SCHEME (CS)</strong></th></tr>
<tr><th><strong>Type of change</strong></th><th><strong>Impact</strong></th><th><strong>Comments</strong></th></tr>
<tr><td><strong>Addition of one or more new concepts in an existing CS</strong></td><td><strong>Minor</strong>: <strong>N.<span style="color:#C00000">+</span></strong></td><td>Data exchanged/disseminated using the old version of the CS can still be exchanged/disseminated using the new CS</td></tr>
<tr><td><strong>Removal of one or more existing concepts</strong></td><td><strong>Major: <span style="color:#C00000">+</span>.0</strong></td><td>Data exchanged/disseminated using the old version of the CS can no longer be exchanged/disseminated using the new version with less concepts</td></tr>
</table>

<table>
<tr><th colspan="3"><strong>DATA STRUCTURE DEFINITION (DSD)</strong></th></tr>
<tr><th><strong>Type of change</strong></th><th><strong>Impact</strong></th><th><strong>Comments</strong></th></tr>
<tr><td><strong>Addition of a dimension</strong></td><td><strong>Major</strong>: <strong><span style="color:#C00000">+</span>.0</strong></td><td>Adding a new dimension has a strong impact because a dimension represents the identifier of a dataset, thus requiring a remodelling of the data as existing structural validation will fail</td></tr>
<tr><td><strong>Addition of a mandatory attribute</strong></td><td><strong>Major</strong>: <strong><span style="color:#C00000">+</span>.0</strong></td><td>If the attribute is mandatory, the situation is the same as under point “Addition of a dimension”</td></tr>
<tr><td><strong>Addition of a conditional attribute</strong></td><td><strong>Minor</strong>: <strong>N.<span style="color:#C00000">+</span></strong></td><td>If the attribute is conditional backward compatibility is maintained</td></tr>
<tr><td><strong>Removal of a dimension or attribute</strong></td><td><strong>Major</strong>: <strong><span style="color:#C00000">+</span>.0</strong></td><td>Whatever the type of component, the change does not guarantee backward compatibility</td></tr>
</table>

For concrete examples, see the Appendix.

# 5. How versioning works for inter-dependent artefacts

This section describes how version changes to inter-dependent or parent/child artefacts affect each other. For example, how a Concept Scheme is affected when one of the Code Lists that it references changes version.

Some artefacts have references to other artefacts. For example:

- each of a Concept Scheme’s Concepts may reference a Code List;
- a DSD can reference one or more Concept Schemes;
- each of a DSD’s Concepts may reference a Code List. (Note that if a Concept-Code List reference exists both in a DSD and a Concept Scheme, the Concept-Code List reference in the DSD overrides the reference in the Concept Scheme);
- a Hierarchical Code List references one or more Code Lists whose codes are arranged in the hierarchical structure.

In the text below, the following concepts will be used:

- **Parent artefact**: an artefact that contains a reference to another artefact. For example, a Concept Scheme is a parent to a Code List that it references, and the Code List is the child;
- **Child artefact**: an artefact that is referenced by another artefact. For example, a Code List is a child of a Concept Scheme that contains a reference to it, and the Concept Scheme is the parent.

It is important to note that a new version of a child artefact does not automatically trigger a version update of the parent artefact. A version change to the parent artefact is made only if the new version of the child artefact is adopted by the parent artefact.

## a. Impact on parent artefact when child artefact version changes

The replacement of a reference with a different reference has the same impact for every artefact.

<table>
<tr><th colspan="3"><strong>ALL ARTEFACTS</strong></th></tr>
<tr><th><strong>Type of change</strong></th><th><strong>Impact</strong></th><th><strong>Comments</strong></th></tr>
<tr><td><strong>Replacement of a child artefact having a different version, but same id and Agency</strong></td><td><strong>The child artefact version change is replicated in the parent artefact</strong></td><td>If a child artefact (e.g. a Code List) has a minor version change, then the parent artefact (e.g. a Concept Scheme) should also have a minor version change.<br><br>If there are several child artefact version changes, the most severe impact is replicated in the parent artefact. For example, if two Code Lists have minor changes, and one Code List has a major change at the same time, the parent Concept Scheme has a major version change</td></tr>
<tr><td><strong>Replacement of a referenced child artefact having a different id or Agency</strong></td><td><strong>The parent artefact version impact depends on the backward/ forward compatibility as shown in the tables above</strong></td><td>Technically, the child artefact is not considered to be related to the previous child artefact. It needs to be checked whether exchange contracts can still be guaranteed (backward/forward compatibility principle)</td></tr>
</table>

## b. Addition or removal of referenced artefacts

<table>
<tr><th colspan="3"><strong>CONCEPT SCHEME (CS)</strong></th></tr>
<tr><th><strong>Type of change</strong></th><th><strong>Impact</strong></th><th><strong>Comments</strong></th></tr>
<tr><td><strong>Addition or removal of a child Code List</strong></td><td><strong>Minor: N.+</strong></td><td>The child Code Lists in a Data Structure Definition have priority over those referenced in a Concept Scheme. Child Code Lists added to or removed from a Concept Scheme do not have a direct impact on the data exchange. Backward/forward compatibility depends on the way Code Lists are referenced in Data Structure Definitions referencing the concept scheme. This needs to be taken into account when creating a new version of a DSD accordingly</td></tr>
</table>

<table>
<tr><th colspan="3"><strong>DATA STRUCTURE DEFINITION (DSD)</strong></th></tr>
<tr><th><strong>Type of change</strong></th><th><strong>Impact</strong></th><th><strong>Comments</strong></th></tr>
<tr><td><strong>Addition or removal of a child Code List</strong></td><td><strong>If same id and Agency, then the child artefact version change is replicated in the parent artefact.</strong><br><strong>If different id or Agency, impact wil depend on the backward/forward compatibility as shown in the tables above</strong></td><td>If a child Code List has a minor version change, then the DSD should also have a minor version change.<br><br>If there are several Code List version changes, the most severe impact is replicated in the DSD.  For example, if two Code Lists have minor changes, and one Code List has a major change at the same time, the parent DSD has a major version change</td></tr>
</table>

# 6. Appendix - Examples

**Example 1 – Change to a Code List name, for clarification purposes**. **Patch Impact: N.M.<span style="color:#FF0000">+</span>**

<table>
<tr><th><strong>Id</strong></th><th><strong>Old Name</strong></th><th><strong>New Name</strong></th></tr>
<tr><td><strong>CL_ADJUSTMENT</strong></td><td>Adjustment codes</td><td>Adjustment code list</td></tr>
</table>

**Example 2** – **Change to a Concept name, for clarification purposes. Patch impact: N.M.<span style="color:#FF0000">+</span>**

<table>
<tr><th><strong>Id</strong></th><th><strong>Old name</strong></th><th><strong>New name</strong></th></tr>
<tr><td><strong>PRODUCT_TO</strong></td><td>Product classification</td><td>Product classification (input-output product*product)</td></tr>
</table>

**Example 3** – **Change in the substance of codes. Major impact: <span style="color:#FF0000">+</span>.0**

<table>
<tr><th><strong>Id</strong></th><th><strong>Old name</strong></th><th><strong>New name</strong></th></tr>
<tr><td><strong>CP01115</strong></td><td>Other products</td><td>Pizza and quiche</td></tr>
</table>

**Example 4** - **Aggregation, disaggregation or reorganisation of codes. Major impact**: **<span style="color:#C00000">+</span>.0**

<table>
<tr><th colspan="2"><strong><span style="color:#17365D">AGGREGATION OF EXISTING CODES</span></strong></th></tr>
<tr><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td><strong>2011</strong> Heifers (female bovine that never calved), live<br><strong>2012</strong> Cows, live</td><td><strong>2010</strong> Heifers and cows, live</td></tr>
<tr><td colspan="2" rowspan="2">Codes <strong>2011</strong> and <strong>2012</strong> are fully<sup><a href="#fn-4" id="fnref-4">4</a></sup> <strong>removed</strong> and replaced with one <strong>brand new</strong> code. In this case there is a many to 1 correspondence between the codes.</td></tr>
</table>

<table>
<tr><th colspan="2"><strong><span style="color:#17365D">DISAGGREGATION OF EXISTING CODES</span></strong></th></tr>
<tr><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td><strong>1010</strong> Live horses</td><td><strong>1011</strong> Pure bred breeding horses, live<br><strong>1012</strong> Other horses, live</td></tr>
<tr><td colspan="2" rowspan="2">Code <strong>1010</strong> is fully <strong>removed</strong> and replaced with two <strong>brand new</strong> codes. In this case there is a 1 to m correspondence between the codes.</td></tr>
</table>

<table>
<tr><th colspan="2"><strong><span style="color:#17365D">REORGANISATION OF EXISTING CODES</span></strong></th></tr>
<tr><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td><strong>3010</strong> Fowls, weighing ≤ 185 g<br><strong>3020</strong> Ducks, , weighing ≤ 185 g<br><strong>3030</strong> Other poultry, weighing ≤ 185 g<br><strong>3040</strong> Fowls, weighing &gt; 185 g<br><strong>3050</strong> Ducks, , weighing &gt; 185 g<br><strong>3060</strong> Other poultry, weighing &gt; 185 g</td><td><strong>3025</strong> Poultry, weighing ≤ 175 g<br><strong>3045</strong> Poultry, weighing &gt; 175 g</td></tr>
<tr><td colspan="2">Codes <strong>3010</strong>, <strong>3020</strong>, <strong>3030</strong>, <strong>3040</strong>, <strong>3050</strong> and <strong>3060</strong> are fully removed and replaced with two brand new codes; furthermore the criterion for the classification used in the old version has been changed in the new version (185 g criterion versus 175 g criterion), so that it is not possible to exactly aggregate the codes from the old version to the codes of the new version (e.g. a part of <strong>3010</strong> goes to <strong>3025</strong>, another part to <strong>3045</strong>). In this case there is a m to n correspondence between the two sets of codes</td></tr>
</table>

**Example 5 – Changes to hierarchies in a Code List. Major impact: <span style="color:#FF0000">+</span>.0**

<table>
<tr><th colspan="2"><strong>ADDING A NEW CODE IN AN EXISTING HIERARCHY – CODE LIST</strong></th></tr>
<tr><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td>• 0213 - Beer<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o 02131 - Lager beer<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o 02132 - Other alcoholic beer</td><td>• 0213 - Beer<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o 02131 - Lager beer<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o 02132 - Other alcoholic beer<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o <strong>02133 - Low and non-alcoholic beer</strong></td></tr>
<tr><td colspan="2">Code 02133 has been added to hierarchy 0213</td></tr>
</table>

**Example 6 – Changes to hierarchies in a Hierarchical Code List. Major impact: <span style="color:#FF0000">+</span>.0**

<table>
<tr><th colspan="2"><strong>ADDING A NEW CODE IN AN EXISTING HIERARCHY – HIERARCHICAL CODE LIST</strong></th></tr>
<tr><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td>• A1 - World (codelist ref. ECB@CL_AREAS@1.0)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o E1  - Europe (ECB@CL_COUNTRIES@1.0)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ ES  - Spain<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ FR - France<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ GR - Greece<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ IT - Italy<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o E4 - Africa<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ etc.</td><td>• A1=World (codelist ref. ECB@CL_AREAS@1.0)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o E1 =   Europe (ECB@CL_COUNTRIES@1.0)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ ES = Spain<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ FR = France<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ GR = Greece<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ IT =  Italy<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>DE= Germany</strong><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o E4 =   Africa<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ etc.</td></tr>
<tr><td colspan="2">The id of the hierarchical codes are assumed to be equal to those of the code lists referenced. The code DE has been added to hierarchy E1</td></tr>
</table>

**Example 7.1 – Dependencies between artefacts: Concept Scheme and Code List. Minor impact: N.<span style="color:#FF0000">+</span>**

<table>
<tr><th><strong>Id:Artefact Type:Details</strong></th><th><strong>Change type</strong></th><th><strong>Version Impact</strong></th><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td><strong>CL_OBS_STATUS:Code List</strong></td><td>Addition of a new code X</td><td><strong>Minor: N.<span style="color:#FF0000">+</span></strong></td><td><strong>1.0</strong></td><td><strong>1.1</strong></td></tr>
<tr><td><strong>CS_TRADE:Concept Scheme: References CL_OBS_STATUS v1.0 above</strong></td><td>Adoption of new code X<br><strong><em>Change type</em></strong>: Replacement of a child artefact having a different version, but  the same id and Agency</td><td><strong>Minor: N.<span style="color:#FF0000">+</span></strong><br>The child version impact is replicated in the parent artefact</td><td><strong>2.0</strong></td><td><strong>2.1</strong></td></tr>
</table>

**Example 7.2 – Dependencies between artefacts: Concept Scheme and Code List. Major impact: <span style="color:#FF0000">+</span>.0**

<table>
<tr><th><strong>Id:Artefact Type:Details</strong></th><th><strong>Change type</strong></th><th><strong>Version Impact</strong></th><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td><strong>CL_OBS_STATUS:Code List</strong></td><td>Removal of code U</td><td><strong>Major: +.0</strong></td><td><strong>1.0</strong></td><td><strong>2.0</strong></td></tr>
<tr><td><strong>CS_TRADE:Concept Scheme:References CL_OBS_STATUS v1.0 above</strong></td><td>Adoption of new CL_OBS_STATUS without U.<br><br><strong><em>Change type</em></strong>: Replacement of a child artefact having a different version, but the same id and Agency</td><td><strong>Major: +.0</strong><br>The child version impact is replicated in the parent artefact.</td><td><strong>2.0</strong></td><td><strong>3.0</strong></td></tr>
</table>

**Example 7.3 – Dependencies between artefacts: Concept Scheme and Code List. Variable impact (see below)**

<table>
<tr><th><strong>Id:Artefact Type:Details</strong></th><th><strong>Change type</strong></th><th><strong>Version Impact</strong></th><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td rowspan="3"><strong>CL_XYZ: Code List</strong></td><td>a) Maintenance agency changes from A to B for governance reasons. Nothing else changes in the code list.</td><td rowspan="3"><strong>New artefact</strong></td><td rowspan="3"><strong>CL_XYZ (Agency A)</strong></td><td rowspan="3"><strong>CL_XYZ (Agency B) (new maintenance agency)</strong></td></tr>
<tr><td>b) Maintenance agency changes from A to B and at the same time new codes are added</td></tr>
<tr><td>c) Maintenance agency changes from A to B. Since B has different coding rules, the code list itself changes as well.</td></tr>
<tr><td rowspan="3"><strong>CS_TRADE: Concept Scheme: References CL_XYZ (Agency A)</strong></td><td rowspan="3">Replacement of a child artefact having a different Agency.<br><br>CL_XYZ (Agency A) changes to CL_XYZ (Agency B).</td><td><strong>Case a): Patch: N.M.<span style="color:#FF0000">+</span></strong> There is no impact on data exchange</td><td><strong>2.0</strong></td><td><strong>2.0.1</strong></td></tr>
<tr><td><strong>Case b): Minor: N. <span style="color:#FF0000">+</span></strong> The impact is the same as a new minor version of the code list</td><td><strong>2.0</strong></td><td><strong>2.1</strong></td></tr>
<tr><td><strong>Case c) Major: <span style="color:#FF0000">+</span>.0</strong> The impact is the same as a new major version of the code list.</td><td><strong>2.0</strong></td><td><strong>3.0</strong></td></tr>
</table>

**Example 7.4 – Dependencies between artefacts: Concept Scheme and DSD. Variable impact (see below)**

<table>
<tr><th><strong>Id:Artefact Type:Details</strong></th><th><strong>Change type</strong></th><th><strong>Version Impact</strong></th><th><strong>Old version</strong></th><th><strong>New version</strong></th></tr>
<tr><td><strong>CS_TRADE: Concept Scheme containing Concepts C1, C2, C3</strong></td><td>Addition of new Concept C4</td><td><strong>Minor: N.<span style="color:#FF0000">+</span></strong></td><td><strong>1.4</strong></td><td><strong>1.5</strong></td></tr>
<tr><td><strong>TRADE: Data Structure Definition: references Concepts C1 and C2</strong></td><td>None<br>Concept C3 is not used</td><td><strong>None</strong></td><td><strong>1.0</strong></td><td><strong>1.0</strong></td></tr>
<tr><td colspan="5"></td></tr>
<tr><td><strong>CS_TRADE: Concept Scheme containing Concepts C1, C2, C3</strong></td><td>Change of description in Concept C3 (typo)</td><td><strong>Patch: N.M.<span style="color:#FF0000">+</span></strong></td><td><strong>1.4</strong></td><td><strong>1.4.1</strong></td></tr>
<tr><td><strong>TRADE: Data Structure Definition: references Concepts C1 and C2</strong></td><td>None<br>Concept C3 is not used</td><td><strong>None</strong></td><td><strong>1.0</strong></td><td><strong>1.0</strong></td></tr>
<tr><td colspan="5"></td></tr>
<tr><td><strong>CS_TRADE: Concept Scheme containing Concepts C1, C2, C3</strong></td><td>Removal of Concept C3</td><td><strong>Major: +.0</strong></td><td><strong>1.4</strong></td><td><strong>2.0</strong></td></tr>
<tr><td><strong>TRADE: Data Structure Definition: references Concepts C1 and C2</strong></td><td>None<br>concept C3 is not used</td><td><strong>None</strong></td><td><strong>1.0</strong></td><td><strong>1.0</strong></td></tr>
<tr><td colspan="5"><strong>Remark:</strong> Once a new version of the DSD is needed for some other reasons (e.g. a change in a code list), it is recommended to update all concept references to the newest available concept scheme if possible: i.e. DSD version 1.1 would then update its concept scheme references from 1.4 to 2.0.</td></tr>
<tr><td colspan="5"></td></tr>
<tr><td><strong>CS_TRADE: Concept Scheme containing Concepts C1, C2, C3</strong></td><td>Change of description in Concept C2 (typo)</td><td><strong>Patch: N.M.+</strong></td><td><strong>1.4</strong></td><td><strong>1.4.1</strong></td></tr>
<tr><td><strong>TRADE: Data Structure Definition: references Concepts C1 and C2</strong></td><td>Correction should be taken into account, concept C2 is used</td><td><strong>Patch: N.M.+ <em>or</em></strong><br><strong>None</strong></td><td><strong>1.0</strong></td><td><strong>1.0.1</strong><br><strong><em>or</em></strong><br><strong>1.0</strong></td></tr>
<tr><td colspan="5"><strong>Remark:</strong> Since the change of a typo in a Concept of the Concept Scheme does not have a direct impact on the DSD itself (the link is by reference), there is strictly speaking no need to update the DSD. Both DSDs (1.0 and 1.0.1) will have exactly the same syntax. However, if maintainers want to highlight the correction for users of the DSD or for some other reason the DSD is updated anyway; it should reference the newer Concept Scheme.</td></tr>
</table>

<!-- footnotes -->

---

<a id="fn-1"></a><sup>1</sup> <span style="color:#0000FF">http://www.semver.org</span>

<a id="fn-2"></a><sup>2</sup> It should be noted that the SDMX standard specifies no limitation as to the number of components in the versioning system. The option proposed here is thus nothing but a recommended convention.

<a id="fn-3"></a><sup>3</sup> The overall impact on compatibility should be assessed when there are several “minor” version impact changes.  For example, it may be that the effect of adding several new Code List or HCL codes results in an implicit change in the meaning of existing Code List or HCL codes which may not be completely backward compatible, therefore (depending on the analysis) the overall version impact may be “Major +.0”.

<a id="fn-4"></a><sup>4</sup> i.e. without integration into or combination with another existing code.
