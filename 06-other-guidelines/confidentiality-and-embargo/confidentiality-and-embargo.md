---
title: "Guidelines for Confidentiality and Embargo in SDMX"
source_url: https://sdmx.org/wp-content/uploads/Guidelines_on_Confidentiality_and_Embargo.docx
source_file: Guidelines_on_Confidentiality_and_Embargo.docx
source_sha256: dd2ceb5223e9fff0fbc50b31d5c299f9d55c0558fca2c4fb6ef01ec0e876fc3e
source_last_modified: "Tue, 11 May 2021 07:58:38 GMT"
retrieved: 2026-09-24
licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)
conversion: DOCX -> Markdown, wording and structure unchanged; see NOTICE.md for the list of changes
---
<!-- figure: f01-logo -->
![SDMX logo](images/f01-logo.png)

**SDMX STATISTICAL GUIDELINES**

GUIDELINES FOR  
CONFIDENTIALITY AND EMBARGO IN SDMX

Version 2.0 - 19 January 2018

# Document History

<table>
<colgroup>
<col style="width: 11%" />
<col style="width: 17%" />
<col style="width: 70%" />
</colgroup>
<thead>
<tr>
<th>Version</th>
<th>Date</th>
<th>Comment</th>
</tr>
</thead>
<tbody>
<tr>
<td>1.0</td>
<td>21/8/2015</td>
<td>Initial version.</td>
</tr>
<tr>
<td>2.0</td>
<td>7/3/2018</td>
<td><p>Replaced the “Embargo: Privileged access” use case confidentiality status to use CONF_STATUS:E instead of CONF_STATUS:N. When this guideline is implemented, the CONF_STATUS:N can no longer be used for this use case (the embargo time is ignored if the CONF_STATUS is N).</p>
<p>Clarified the document text, removed superfluous text.</p>
<p>Added use of time zone is recommended.</p></td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

# Introduction

This paper presents use case scenarios related to confidentiality and embargo in SDMX data exchanges, and provides recommendations on how to represent these elements in the SDMX model. The aim is to provide a consistent and practical way to represent these aspects in SDMX artefacts in order to promote cross-domain consistency, and harmonise methodology and processes.

Confidentiality aims at protecting data from unauthorised disclosure that could be prejudicial or harmful to the interest of the source or other relevant parties.

Embargo means that data may become public only after expiry of a pre-defined date and time.

Embargo establishes a relationship between a set of data (e.g. an observation), a date/time and a group of privileged data recipients.

Disclosure of data marked as confidential or under embargo is not permitted. Procedures should be in place to prevent such disclosure, including rules for staff, aggregation rules when disseminating data, provision of unit records, etc.

There needs to be a formal agreement between organisations involved in the exchange of confidential data in order to prepare systems and workflows.

Data exchange partners are advised to agree up front on the usage of the embargo mechanism(s) for specific data messages.

The embargo CONF_STATUS value “E” is not recommended for final dissemination to users but only for data exchange.

# Use Cases 

This section describes the confidentiality and embargo use cases that are addressed by these guidelines. The use cases and embargo SDMX representations are summarised in annex 1:

## USE CASE 1: NON-CONFIDENTIAL DATA 

Data is available to the public immediately, meaning that data is not confidential and there is no embargo.

The data’s CONF_STATUS attribute should be set to “Free (free for publication)”.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th><h3 id="sdmx-representation">SDMX representation</h3>
<ul>
<li><p><strong>CONF_STATUS</strong>: F</p></li>
</ul></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

## USE CASE 2: CONFIDENTIAL DATA

### Exchange of confidential data without embargo nor forwarding to secondary recipients

One or more observations in the data message are confidential. Embargo does not play a role in this scenario. Depending on arrangements between data exchange partners, this data can be made available to privileged data users.

The observation’s CONF_STATUS attribute should use a specific code denoting the confidential character of the information. Below are some examples of such confidentiality statuses<sup><a href="#fn-1" id="fnref-1">1</a></sup>:

- **N**: Not for publication, restricted for internal use only. Used to denote observations that are restricted for internal use only within organisations

- **C**: Confidential statistical information (primary confidentiality) due to identifiable respondents

- **D**: Secondary confidentiality set by the sender, not for publication

- **A**: Primary confidentiality due to small counts

### Forwarding confidential data to secondary recipients

A sender sends confidential data to certain primary recipients, and allows those to forward the confidential data to a restricted and pre-defined set of secondary recipients.

The observation’s CONF_STATUS attribute should be marked as “Not for publication, restricted for internal use only”. An additional observation-level attribute: CONF_REDIST, defines the secondary recipient(s) to whom the sender allows the primary recipient to forward confidential data<sup><a href="#fn-2" id="fnref-2">2</a></sup>. See section **Use of the CONF_REDIST attribute** for the appropriate coding of this attribute.

The forwarding of confidential data is represented as follows in SDMX:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th><h3 id="sdmx-representation-1">SDMX representation</h3>
<ul>
<li><p><strong>CONF_STATUS</strong>: N;</p></li>
<li><p><strong>CONF_REDIST</strong> (Observation, Conditional): [Organisation(s)];</p></li>
</ul></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### Adding embargo information to a data message

Following the definition of embargo, the recipient must keep the data confidential until a pre-defined point in time (embargo) when it becomes public.

Two cases can be distinguished:

- Allowing privileged access to embargoed data

- Enabling the frontloading of data into systems

***Allowing privileged access to embargoed data***

If the goal is to allow the data recipient to have privileged access to embargoed observations in a data message (message), the embargoed observation’s CONF_STATUS attribute should be coded as “E: Not for publication until the embargo time expires; free for publication after the embargo time expires.” with an observation level attribute EMBARGO_TIME (date/time/time zone).

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th><h3 id="sdmx-representation-2">SDMX representation</h3>
<ul>
<li><p><strong>CONF_STATUS</strong>: E;</p></li>
<li><p><strong>EMBARGO</strong>_<strong>TIME</strong> (Observation, Conditional): [timestamp]</p></li>
</ul></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

Including a time zone is strongly recommended and the best case is to use the UTC (Coordinated Universal Time) time standard. However, if no time zone is provided then the time zone of the recipient is assumed.

These two examples represent the same time for a recipient established in the Central European time zone (e.g. Germany, Norway, Gibraltar):

- (Recommended) With UTC indicator: 2017-12-15T14:02:29Z

- With timezone indicator: 2017-12-15T15:02:29+01:00

***Enabling the frontloading of data into systems***

If the goal is to allow frontloading of a whole data message into systems so that the data can be made visible to users at the expiry of the embargo date/time, the header section of the message should contain an embargo date/time attribute. This implies that all information in the data message is under the embargo date/time set in the header. The header attribute EmbargoDate with format date/time/time zone indicates until when the whole data message received cannot be shared with any recipient users.

Once the EmbargoDate in the header elapses, each observation’s confidentiality status becomes that which is marked in the CONF_STATUS attributes.

Note that this scenario presumes that all data in the message cannot be viewed before the header EmbargoDate, and that there is no privileged access before this time. However, observations may be marked with any other confidentiality status that is valid after the frontloading EmbargoDate elapses.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th><h3 id="sdmx-representation-3">SDMX Representation</h3>
<ul>
<li><p><strong>CONF_STATUS</strong>: &lt;Set to the required confidentiality status after the embargo time elapses&gt;; &lt;Header&gt;\&lt;EmbargoDate&gt;: [timestamp]</p></li>
</ul></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

The two ways of representing embargoed data exist to provide efficiency in the exchange, allow for differentiating data intended to be frontloaded and data aimed to be provided in advance to a restricted audience, and provide flexibility when few observations need to be embargoed in a large data message. The trade-off is the complication of system implementation to support the two representations of embargo, which has to be done locally on a case-by-case basis.

# Additional recommendations and examples

In data flows that feature confidential data, CONF_STATUS is highly recommended to be a mandatory attribute. However, if CONF_STATUS is optional in the DSD and missing from an observation, it is always implied to be “F” (free).

### Use of the CONF_REDIST attribute

The CONF_REDIST attribute defines the secondary recipient(s) to whom the sender allows the primary recipient to forward confidential data. It is recommended to be an optional attribute at observation level. Ideally it should reference a shared code list containing standard organisation codes. To allow several secondary recipients there are these possibilities:

1.  Use a code that represents multiple organisations, or;

2.  Use several CONF_REDIST attributes to portray the multiple recipients. Each attribute represents one recipient and references the same codelist. This implementation is cleaner than the above point 1, though this will require adding as many attributes to your DSD as there are potential recipients of the redistributed confidential data.

    If the EMBARGO_TIME and CONF_REDIST attributes are both used:

<!-- -->

1.  Data is available only to the organisations in CONF_REDIST until EMBARGO_TIME

2.  Data is available to the public after EMBARGO_TIME

<table style="width:100%;">
<colgroup>
<col style="width: 27%" />
<col style="width: 35%" />
<col style="width: 37%" />
</colgroup>
<thead>
<tr>
<th colspan="3" style="text-align: center;"><h1
id="privileged-access">Privileged Access</h1></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><strong>Use case</strong></td>
<td style="text-align: center;"><strong>No forwarding</strong></td>
<td style="text-align: center;"><strong>Forwarding</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Embargo</strong></td>
<td style="text-align: center;"><p>CONF_STATUS: E</p>
<p>EMBARGO_TIME</p></td>
<td style="text-align: center;"><p>CONF_STATUS: E</p>
<p>EMBARGO_TIME</p>
<p>CONF_REDIST</p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>No embargo</strong></td>
<td style="text-align: center;">CONF_STATUS: N</td>
<td style="text-align: center;"><p>CONF_STATUS:N</p>
<p>CONF_REDIST</p></td>
</tr>
</tbody>
</table>

### An example of sending data for privileged access with data forwarding information

This example describes a case where data needs to be embargoed until a certain date and time, and may be sent to certain other organisations in a single transmission without modification of the data or attributes.

This example is based on the exchange of sector accounts statistics within the European statistical system.

- The national statistical institutes send data to Eurostat, and allow the data to be shared with the ECB for statistical coproduction

- The data may only be shared with the public on the next day

  <strong>CONF_STATUS:</strong>E<strong>;</strong>

  **CONF_REDIST:** ECB<strong>;</strong>

  <strong>EMBARGO_TIME=\<</strong>T+1 day<strong>,</strong> e.g. 2017-12-15T10:00:00Z\>

The solutions suggested above aim at covering the most common confidentiality and embargo use cases within a single transmission from the primary reporter to the primary recipient. However, for some more complex scenarios it might still be required to make multiple transmissions.

It is strongly recommended that use cases are specified in an agreement between organisations involved in regular transmissions up-front in order to avoid unnecessary delay in data publication or – much worse – confidentiality breaches.

**Annex 1: SDMX Representation of the confidentiality use cases**

<table>
<colgroup>
<col style="width: 14%" />
<col style="width: 13%" />
<col style="width: 29%" />
<col style="width: 43%" />
</colgroup>
<thead>
<tr>
<th><h2 id="use-case"><strong>Use case</strong></h2></th>
<th><h2 id="conf_status-observation">CONF_STATUS (Observation)</h2></th>
<th style="text-align: center;"><h2 id="additional-attributes">Additional attributes</h2></th>
<th style="text-align: center;"><h2 id="remarks">Remarks</h2></th>
</tr>
</thead>
<tbody>
<tr>
<td><h2 id="non-confidential-data"><strong>Non-confidential data</strong></h2></td>
<td><h2 id="f">F</h2></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td><h2 id="confidential-data-with-no-embargo"><strong>Confidential data with no embargo</strong></h2></td>
<td><h2 id="cdsaotgmn">C;D;S;A;O;T;G;M;N</h2></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><h2 id="conf_status-will-usually-be-c-but-may-also-be-dsaotgmn-depending-on-the-required-status-and-confidentiality-reason-see-the-cl_conf_status-code-list-for-details">CONF_STATUS will usually be C but may also be D;S;A;O;T;G;M;N depending on the required status and confidentiality reason. See the CL_CONF_STATUS code list for details<sup><a href="#fn-3" id="fnref-3">3</a></sup></h2></td>
</tr>
<tr>
<td style="text-align: center;">Forwarding of confidential data</td>
<td style="text-align: center;">N</td>
<td style="text-align: center;">CONF_REDIST: (Observation, Conditional)</td>
<td style="text-align: center;">CONF_REDIST may represent multiple organisations</td>
</tr>
<tr>
<td><h2 id="embargo-privileged-access"><strong>Embargo: Privileged access</strong></h2></td>
<td><h2 id="e">E</h2></td>
<td style="text-align: center;"><h2 id="embargo_time-observation-conditional">EMBARGO_TIME (Observation, Conditional)</h2></td>
<td style="text-align: center;">Only the observations with an EMBARGO_TIME attribute are embargoed. After the embargo time elapses, the data are free for publication (equivalent to F status).</td>
</tr>
<tr>
<td><h2 id="embargo-privileged-access-with-forwarding"><strong>Embargo: Privileged access with forwarding</strong></h2></td>
<td><h2 id="e-1">E</h2></td>
<td style="text-align: center;"><p>EMBARGO_TIME (Observation, Conditional)</p>
<h2 id="conf_redist-observation-conditional">CONF_REDIST: (Observation, Conditional)</h2></td>
<td style="text-align: center;"><h2 id="only-the-observations-with-an-embargo_time-attribute-are-embargoed-after-the-embargo-time-elapses-the-data-are-free-for-publication-equivalent-to-f-status">Only the observations with an EMBARGO_TIME attribute are embargoed. After the embargo time elapses, the data are free for publication (equivalent to F status).</h2>
<h2 id="conf_redist-may-represent-multiple-organisations">CONF_REDIST may represent multiple organisations</h2></td>
</tr>
<tr>
<td><h2 id="embargo-frontloading"><strong>Embargo: Frontloading</strong></h2></td>
<td><h2 id="set-to-the-required-confidentiality-status-after-the-embargo-time-elapses">Set to the required confidentiality status after the embargo time elapses.</h2></td>
<td style="text-align: center;"><h2 id="headerembargodate-timestamp">&lt;Header\EmbargoDate&gt;: [timestamp]</h2></td>
<td style="text-align: center;">There is no EMBARGO_TIME attribute as the whole message is embargoed with no privileged access.</td>
</tr>
</tbody>
</table>

<!-- footnotes -->

------------------------------------------------------------------------

<a id="fn-1"></a><sup>1</sup> For a full list of confidentiality statuses, see <https://sdmx.org/wp-content/uploads/CL_CONF_STATUS_1_2_2018.docx>.

<a id="fn-2"></a><sup>2</sup> Example: National statistical institute XX reporting data to Eurostat indicates that Eurostat can forward those data to the ECB, IMF and OECD. More complex use case: The reporting organization specifies that Eurostat can forward those data only to the ECB Statistics Department, thus excluding all other organisations as well as all other ECB departments.

<a id="fn-3"></a><sup>3</sup> <https://sdmx.org/wp-content/uploads/CL_CONF_STATUS_1_2_2018.docx>
