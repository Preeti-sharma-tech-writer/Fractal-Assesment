# Standard Data Asset Documentation Template


<!-- For authors: 
 Use this template when a production data model, table, view, or KPI is released for a Fractal customer. Replace all text in `[square brackets]`. Keep the sections relevant to the asset and remove author instructions before publishing. If a required field does not apply, enter `Not applicable` and explain why -->


---


# [Customer or project name]: [Data asset name]


## 1. Overview


[In 2-3 sentences, explain what the asset represents, why it was created, and how it helps the customer's business.]


| Attribute | Details |
| --- | --- |
| Customer or project | [Customer or project name] |
| Business domain | [For example: Marketing, Finance, Supply Chain, Customer Analytics] |
| Asset name | [`database.schema.asset_name` or KPI name] |
| Asset type | [Data model / Table / View / KPI] |
| Data platform | [For example: Snowflake, Databricks, BigQuery, PostgreSQL] |
| Environment | [Production] |
| Version | [For example: 1.0] |
| Status | [Draft / Approved / Certified / Deprecated] |
| Release date | [YYYY-MM-DD] |
| Last reviewed | [YYYY-MM-DD] |


### Business context


- **Business problem:** [Describe the customer problem or decision this asset supports.]
- **Business value:** [Explain the expected outcome or benefit.]
- **Primary users:** [List the customer teams or roles that should use the asset.]
- **Recommended use:** [Explain when users should use this asset and whether it is the canonical source.]
- **Do not use for:** [List purposes for which the asset is unsuitable.]


### Ownership and support


| Role | Name or team | Responsibility | Contact or link |
| --- | --- | --- | --- |
| Customer business owner | [Name or team] | Approves the business definition and intended use | [Email, channel, or link] |
| Fractal technical owner | [Name or team] | Maintains the model, pipeline, or KPI logic | [Email, channel, or link] |
| Data steward | [Name or team] | Oversees data quality, access, and documentation | [Email, channel, or link] |


---


## 2. Asset definition and technical metadata


| Attribute | Details |
| --- | --- |
| Business definition | [Define the asset in plain language.] |
| Grain | [State exactly what one row or one KPI result represents.] |
| Primary key | [`field_name`, composite key, or `Not applicable`] |
| Foreign or unique keys | [`field_name`, relationship, or `Not applicable`] |
| Refresh frequency | [Real time / Hourly / Daily / Weekly / Other] |
| Refresh schedule | [Schedule and time zone] |
| Expected availability | [For example: Available by 08:00 UTC each day] |
| Update method | [Full refresh / Incremental / Streaming] |
| Retention period | [Retention rule] |
| Data classification | [Public / Internal / Confidential / Restricted] |


---


## 3. Model or relationship diagram


<!-- For authors: Use this section for data models, tables, or views. For a KPI with no structural relationships, link to the relevant semantic model or remove this section. ... -->


**Diagram:** [Link to the approved ERD, data model, dbt documentation, Miro board, or architecture diagram]


**Relationship summary:**


```text
[SOURCE_TABLE] 1 -> 0..N [CURRENT_ASSET] N -> 1 [REFERENCE_TABLE]
```


[Explain the main entities and how they relate. Define any cardinality that could affect joins or record counts.]


---


## 4. Data dictionary


<!-- For authors:  Use this section for each documented table, view, or model output. Copy the table subsection when the model contains multiple tables. For a KPI, document the dimensions and fields exposed with the metric, or remove this section if none are exposed.-->


### Table or view: `[table_name]`


- **Description:** [Explain what the table or view contains.]
- **Grain:** [Describe what one row represents.]
- **Primary key:** [`field_name` or composite key]
- **Business rule:** [State the most important rule governing valid records.]


| Field name | Data type | Constraints | Business description | Source or derivation | Sample value |
| --- | --- | --- | --- | --- | --- |
| [`field_name`] | [`DATA_TYPE`] | [Primary Key / Foreign Key / Not Null / Unique / Nullable] | [Define the field in plain language.] | [`source.field` or calculation] | [`sample_value`] |
| [`field_name`] | [`DATA_TYPE`] | [Constraint] | [Definition] | [Source or derivation] | [`sample_value`] |


---


## 5. KPI definition


<!-- For authors:  Keep this section for a KPI or for a data model that produces a governed KPI. Otherwise, remove it.-->


### [KPI name]


- **Business definition:** [Explain exactly what the KPI measures.]
- **Formula:** `[Numerator / Denominator] x [Scaling factor, if applicable]`
- **Aggregation:** [SUM / COUNT / COUNT DISTINCT / AVG / Other]
- **Time window:** [Daily / Weekly / Monthly / Rolling number of days / Other]
- **Reporting time zone:** [Time zone]
- **Unit or format:** [Number / Percentage / Currency / Duration / Other]
- **Target or threshold:** [Target, threshold, or `Not applicable`]
- **Dimensions available:** [For example: Region, channel, product, customer segment]


```sql
-- [Add the governed KPI logic or pseudocode.]
[KPI calculation]
```


---


## 6. Business rules, filters, and joins


### Inclusion rules


- [State which records, statuses, dates, users, or events are included.]


### Exclusion rules


- [State which records, statuses, dates, test data, or events are excluded.]


### Required filters


| Field | Filter condition | Business reason |
| --- | --- | --- |
| [`field_name`] | [`condition`] | [Explain why the filter must be applied.] |


### Join guidance


- **Recommended join key:** [`field_name`]
- **Expected cardinality:** [One-to-one / One-to-many / Many-to-one]
- **Join type:** [INNER / LEFT / Other]
- **Avoid:** [Describe joins that can duplicate rows, omit records, or change the KPI.]


---


## 7. Data lineage and dependencies


### Lineage summary


```text
[Source system] -> [Raw or staging asset] -> [Transformation or model] -> [This asset] -> [Dashboard, report, API, or KPI]
```


### Upstream dependencies


| Source system or asset | Data received | Refresh dependency | Owner | Reference |
| --- | --- | --- | --- | --- |
| [`source_asset`] | [Fields, events, or files used] | [Required timing or job] | [Name or team] | [Link] |


### Downstream consumers


| Consumer | How the asset is used | Impact if delayed or changed | Owner | Reference |
| --- | --- | --- | --- | --- |
| [Dashboard, report, model, API, or customer team] | [Usage] | [Business or technical impact] | [Name or team] | [Link] |


---


## 8. Caveats and known edge cases


| Caveat or edge case | Effect on results | Recommended handling | Status |
| --- | --- | --- | --- |
| [Describe the condition or limitation.] | [Explain how records, values, or interpretation are affected.] | [Tell the user what to do.] | [Open / Accepted / Fix planned for YYYY-MM-DD] |


> **Warning:** [Add a warning if using the asset incorrectly could cause a material reporting or business error. Remove this callout if no warning applies.]


---


## 9. Data quality and validation


| Validation check | Expected result or threshold | Frequency | Owner | Monitoring or result link |
| --- | --- | --- | --- | --- |
| [Freshness check] | [Expected delay or SLA] | [Frequency] | [Team] | [Link] |
| [Completeness check] | [Threshold] | [Frequency] | [Team] | [Link] |
| [Uniqueness or reconciliation check] | [Threshold] | [Frequency] | [Team] | [Link] |


- **Known quality issue:** [Describe any current issue, or enter `None`.]
- **Issue reporting:** [Explain how customer users should report a data issue.]


---


## 10. Usage example


[Explain what the following example returns and when a customer user should use it.]


```sql
SELECT
   [field_or_metric]
FROM [database.schema.asset_name]
WHERE [required_filter];
```


**Expected result:** [Describe how to interpret the output.]


---


## 11. Related resources


- [Canonical dashboard or report](URL)
- [Related data model, table, or KPI](URL)
- [Pipeline or orchestration job](URL)
- [Runbook or troubleshooting guide](URL)
- [Access request process](URL)


---


## 12. Update log


| Date | Version | Change | Customer impact | Author or approver |
| --- | --- | --- | --- | --- |
| [YYYY-MM-DD] | [Version] | [Describe the release or documentation change.] | [State the impact or `No impact`.] | [Name or team] |


---

