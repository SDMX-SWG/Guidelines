# NOTICE

This directory is an adaptation of the **SDMX statistical guidelines** published by the SDMX Statistical Working Group (SWG) at <https://sdmx.org/guidelines/>, retrieved on 2026-09-24.

The guidelines are licensed under the Creative Commons Attribution-ShareAlike 4.0 International licence ([CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)). This adaptation is distributed under the same licence. © SDMX; the original documents remain available at the source URLs below.

## What was changed

The documents were converted from Word (DOCX) and PDF to Markdown. The wording and the structure were kept as they are; the conversion made only the changes listed here.

**In every document**

- **Format.** Word and PDF layout was expressed in Markdown: headings, lists, tables (HTML where cells are merged), footnotes (kept with the source's own numbers), equations (TeX between `$`).
- **Page furniture removed.** Running headers and footers, page numbers, margin line numbers and the page numbers of tables of contents do not exist in a Markdown page. Header and footer texts are listed in each document's front matter (`page_furniture_not_reproduced`). Table-of-contents entries link to the headings.
- **Figures.** Diagrams and charts are redrawn in Mermaid; the original figure follows each one in a collapsed "Original figure" block. The Mermaid carries the content (boxes, labels, connections, colours); its layout is Mermaid's own. Where a diagram differs from its original, the difference is recorded in `figures/<document>.json` (field `review`) in the conversion workspace. Screenshots, logos and pictures of text are included as images.
- **Charts drawn as tables** (a Word table whose shaded cells are the bars) are redrawn in Mermaid from the table itself, with the original rendering below.
- **Colour.** Text colour that can carry meaning is kept as HTML colour; black, greys and near-white are not reproduced. Some Markdown renderers (GitHub among them) show such text uncoloured.
- **Source errors kept.** Typos, broken links and other defects of the originals are kept as published.

**In particular documents**

- [SDMX Content-Oriented Guidelines — Introduction](01-introduction/cog-introduction/cog-introduction.md)
  - published as PDF only: headings, lists and tables were read from the page layout
- [Guidelines for the Creation and Management of SDMX Code Lists](02-code-lists/code-lists-guidelines/code-lists-guidelines.md)
  - a drawing was left out: cover-page frame: an empty bordered rectangle around the title block (no text, no meaning)
- [Classification of Statistical Subject-Matter Domains](03-subject-matter-domains/subject-matter-domains/subject-matter-domains.md)
  - published as PDF only: headings, lists and tables were read from the page layout
- [Governance of commonly used SDMX metadata artefacts](05-governance/governance-commonly-used-artefacts/governance-commonly-used-artefacts.md)
  - a drawing was left out: cover-page frame: an empty bordered rectangle around the title block (no text, no meaning)
  - drawings laid over text (f03-change-steps) are kept as the original rendering after the text
- [Standardising Reference Metadata Reporting in SDMX](06-other-guidelines/reference-metadata-reporting/reference-metadata-reporting.md)
  - published as PDF only: headings, lists and tables were read from the page layout
  - a glyph that the PDF's font exports as the code U+F0B7 is written as "•", as it is printed
- [Modelling Statistical Domains in SDMX](06-other-guidelines/modelling-statistical-domains/modelling-statistical-domains.md)
  - a cross-reference (REF) showed a stale stored value "2.3"; the value Word displays, "2.2.2", is used
  - a cross-reference (REF) showed a stale stored value "2.3"; the value Word displays, "2.2.2", is used
  - a cross-reference (NOTEREF) showed a stale stored value "7"; the value Word displays, "4", is used
- [Guidelines for SDMX Data Structure Definitions](06-other-guidelines/dsd-guidelines/dsd-guidelines.md)
  - published as PDF only: headings, lists and tables were read from the page layout
  - an illegible clipped fragment on page 27 is left out
- [Guidelines on the Versioning of SDMX Artefacts](06-other-guidelines/versioning/versioning.md)
  - published as PDF only: headings, lists and tables were read from the page layout
  - a glyph that the PDF's font exports as the code U+0001 is written as "→", as it is printed
  - a glyph that the PDF's font exports as the code U+0002 is written as "▪", as it is printed
- [Guidelines for SDMX Concept Roles](06-other-guidelines/concept-roles/concept-roles.md)
  - a drawing was left out: cover-page frame: an empty bordered rectangle around the title block (no text, no meaning)
  - drawings laid over text (f01-roles-sdmx20) are kept as the original rendering after the text
  - drawings laid over text (f02-variable-role-sdmx21) are kept as the original rendering after the text
  - drawings laid over text (f03-geo-role-sdmx21) are kept as the original rendering after the text
- [SDMX Global Registry Content Policy](06-other-guidelines/global-registry-content-policy/global-registry-content-policy.md)
  - published as PDF only: headings, lists and tables were read from the page layout
- [Guidelines for Modelling Vintages in SDMX](06-other-guidelines/vintages/vintages.md)
  - a text box (t01-ecb-query-url) is given as its text
  - a text box (t02-dataflows-xml) is given as its text in a code block, line for line
  - a text box (t03-dsd-xml) is given as its text in a code block, line for line
  - a text box (t04-codelist-xml) is given as its text in a code block, line for line
  - a text box (t05-attribute-xml) is given as its text in a code block, line for line
  - a text box (t06-attribute-usage-xml) is given as its text in a code block, line for line
  - a text box (t07-codelist-xml) is given as its text in a code block, line for line

**The index page** ([README.md](README.md)) is the page <https://sdmx.org/guidelines/>. Its links to the guideline files point to the converted Markdown instead; all other links are as published.

## Sources

| Document | Source | SHA-256 (first 16) | Last modified |
|---|---|---|---|
| [SDMX Content-Oriented Guidelines — Introduction](01-introduction/cog-introduction/cog-introduction.md) | [SDMx_COG_2016_Introduction.pdf](https://sdmx.org/wp-content/uploads/SDMx_COG_2016_Introduction.pdf) | `155248da46e41d47` | Tue, 11 May 2021 07:58:44 GMT |
| [Guidelines for the Creation and Management of SDMX Code Lists](02-code-lists/code-lists-guidelines/code-lists-guidelines.md) | [SDMx_Guidelines_for_CDCL-1.docx](https://sdmx.org/wp-content/uploads/SDMx_Guidelines_for_CDCL-1.docx) | `6e7265af082ce5bd` | Tue, 25 Feb 2025 09:34:49 GMT |
| [Classification of Statistical Subject-Matter Domains](03-subject-matter-domains/subject-matter-domains/subject-matter-domains.md) | [03_sdmx_cog_annex_3_smd_2009.pdf](https://sdmx.org/wp-content/uploads/03_sdmx_cog_annex_3_smd_2009.pdf) | `1e8cb8d17f756b33` | Tue, 11 May 2021 07:57:58 GMT |
| [SDMX Glossary Version 2.1](04-glossary/glossary/glossary.md) | [SDMx_Glossary_version_2_1-Final-2.docx](https://sdmx.org/wp-content/uploads/SDMx_Glossary_version_2_1-Final-2.docx) | `f999a02dd71f7711` | Tue, 11 May 2021 07:58:46 GMT |
| [Reference Framework for SDMX Structural Metadata Governance](05-governance/structural-metadata-governance/structural-metadata-governance.md) | [SDMx-Structural-Metadata-Governance.docx](https://sdmx.org/wp-content/uploads/SDMx-Structural-Metadata-Governance.docx) | `6d8a3bcb9e0495cf` | Wed, 29 Mar 2023 13:26:23 GMT |
| [Governance of commonly used SDMX metadata artefacts](05-governance/governance-commonly-used-artefacts/governance-commonly-used-artefacts.md) | [Governance_of_commonly_used_SDMx_metadata_artefacts_v1.3.docx](https://sdmx.org/wp-content/uploads/Governance_of_commonly_used_SDMx_metadata_artefacts_v1.3.docx) | `b3c8adbe341b48a7` | Tue, 11 May 2021 07:58:38 GMT |
| [Guidelines on Using SDMX Annotations](06-other-guidelines/annotations/annotations.md) | [Guidelines-on-the-use-of-SDMx-Annotations-2.0.docx](https://sdmx.org/wp-content/uploads/Guidelines-on-the-use-of-SDMx-Annotations-2.0.docx) | `173303bbf8fc1d64` | Tue, 29 Apr 2025 09:29:40 GMT |
| [Standardising Reference Metadata Reporting in SDMX](06-other-guidelines/reference-metadata-reporting/reference-metadata-reporting.md) | [Standardising-Reference-Metadata-Reporting-in-SDMx-v1-0.pdf](https://sdmx.org/wp-content/uploads/Standardising-Reference-Metadata-Reporting-in-SDMx-v1-0.pdf) | `8e24962d0d3e927d` | Tue, 11 May 2021 07:58:48 GMT |
| [Modelling Statistical Domains in SDMX](06-other-guidelines/modelling-statistical-domains/modelling-statistical-domains.md) | [Modelling-statistical-domains-in-SDMx-v2-201806.docx](https://sdmx.org/wp-content/uploads/Modelling-statistical-domains-in-SDMx-v2-201806.docx) | `16ffb73eaa08cc76` | Tue, 11 May 2021 07:58:40 GMT |
| [Guidelines for Representing Methodological Changes in Data Structure Definitions](06-other-guidelines/methodological-changes-in-dsds/methodological-changes-in-dsds.md) | [GUIDELINES_FOR_REPRESENTING_METHODOLOGICAL_CHANGES_IN_DSDs_version_1_0.docx](https://sdmx.org/wp-content/uploads/GUIDELINES_FOR_REPRESENTING_METHODOLOGICAL_CHANGES_IN_DSDs_version_1_0.docx) | `4858f35906d38c83` | Tue, 11 May 2021 07:58:38 GMT |
| [Guidelines for SDMX Data Structure Definitions](06-other-guidelines/dsd-guidelines/dsd-guidelines.md) | [SDMx_Guidelines_for_DSDs_1.0.pdf](https://sdmx.org/wp-content/uploads/SDMx_Guidelines_for_DSDs_1.0.pdf) | `b435fcd9e94e524d` | Tue, 11 May 2021 07:58:46 GMT |
| [Guidelines on the Versioning of SDMX Artefacts](06-other-guidelines/versioning/versioning.md) | [Guidelines_on_versioning_v1_0.pdf](https://sdmx.org/wp-content/uploads/Guidelines_on_versioning_v1_0.pdf) | `8ce43013c533dd4b` | Tue, 11 May 2021 07:58:38 GMT |
| [Guidelines on Non-Calendar Year Reporting of Data](06-other-guidelines/non-calendar-year-reporting/non-calendar-year-reporting.md) | [Guidelines_Non-Calendar_Year_Reporting_V1-0.docx](https://sdmx.org/wp-content/uploads/Guidelines_Non-Calendar_Year_Reporting_V1-0.docx) | `095b4c40349b5d38` | Tue, 11 May 2021 07:58:38 GMT |
| [Possible Ways of Implementing the Observation Status Concept](06-other-guidelines/observation-status/observation-status.md) | [OBS_STATUS_Implementation_2_0.docx](https://sdmx.org/wp-content/uploads/OBS_STATUS_Implementation_2_0.docx) | `0dd5874965225ec3` | Tue, 11 May 2021 07:58:40 GMT |
| [Guidelines for Confidentiality and Embargo in SDMX](06-other-guidelines/confidentiality-and-embargo/confidentiality-and-embargo.md) | [Guidelines_on_Confidentiality_and_Embargo.docx](https://sdmx.org/wp-content/uploads/Guidelines_on_Confidentiality_and_Embargo.docx) | `dd2ceb5223e9fff0` | Tue, 11 May 2021 07:58:38 GMT |
| [Guidelines on Coding Time Transformations in SDMX](06-other-guidelines/time-transformations/time-transformations.md) | [SWG_TimeTransformation_V1.0.docx](https://sdmx.org/wp-content/uploads/SWG_TimeTransformation_V1.0.docx) | `cc159e5a5eba7caf` | Tue, 11 May 2021 07:58:48 GMT |
| [Guidelines for SDMX Concept Roles](06-other-guidelines/concept-roles/concept-roles.md) | [Guidelines_for_SDMx_Concept_Roles_v1.1.docx](https://sdmx.org/wp-content/uploads/Guidelines_for_SDMx_Concept_Roles_v1.1.docx) | `80abd2eb0425bdc7` | Thu, 21 Jul 2022 23:29:12 GMT |
| [Checklist for SDMX Data Providers — data provider story](06-other-guidelines/data-provider-checklist-story/data-provider-checklist-story.md) | [checklist_for_data_provider_story.docx](https://sdmx.org/wp-content/uploads/checklist_for_data_provider_story.docx) | `956eda421a4254c7` | Tue, 11 May 2021 07:58:04 GMT |
| [SDMX Global Registry Content Policy](06-other-guidelines/global-registry-content-policy/global-registry-content-policy.md) | [SDMx_Global_Registry_Content_Policy_5-3-2015.pdf](https://sdmx.org/wp-content/uploads/SDMx_Global_Registry_Content_Policy_5-3-2015.pdf) | `54a7e4f6749d1edd` | Tue, 11 May 2021 07:58:46 GMT |
| [Guidelines for SDMX Hierarchies](06-other-guidelines/hierarchies/hierarchies.md) | [GUIDELINES_FOR_SDMx_HIERARCHIES_version_1_0.docx](https://sdmx.org/wp-content/uploads/GUIDELINES_FOR_SDMx_HIERARCHIES_version_1_0.docx) | `4c5735489fbe8b94` | Tue, 02 Sep 2025 06:54:52 GMT |
| [Guidelines for Modelling Vintages in SDMX](06-other-guidelines/vintages/vintages.md) | [GUIDELINES_FOR_WORKING_WITH_VINTAGES_IN_SDMx_version_1_0.docx](https://sdmx.org/wp-content/uploads/GUIDELINES_FOR_WORKING_WITH_VINTAGES_IN_SDMx_version_1_0.docx) | `47fa7c2dc023f34a` | Wed, 15 Oct 2025 14:14:14 GMT |
| [Guidelines for Modelling Units of Measure in SDMX](06-other-guidelines/units-of-measure/units-of-measure.md) | [Guidelines-for-modelling-Units-of-measure-in-SDMx.docx](https://sdmx.org/wp-content/uploads/Guidelines-for-modelling-Units-of-measure-in-SDMx.docx) | `17e9a3751f157d36` | Mon, 12 Jan 2026 13:17:09 GMT |
