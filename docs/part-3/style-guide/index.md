# Fractal Data Documentation Quick Style Guide

Use these standards when creating or updating internal data and analytics documentation.

## Titles, tone, and terminology

- Use sentence case.   
- For metric and data asset reference pages, use the official metric or asset name as the title—for example, **Total Converted Leads**.
- Begin procedure titles with an imperative verb, such as **Validate dashboard results**,” and troubleshooting titles with **Resolve** or **Fix**.  
- Write in active voice, present tense, and plain American English.
- Use **you** for reader actions and begin procedural steps with a verb.  
- Lead with what readers can understand, complete, decide, or resolve. 
- Avoid slang, hype, blame, unnecessary formality, and unsupported claims such as **always accurate** or **real time**.  
- Use one approved term for each concept. Explain the business meaning before the technical implementation.  
- Define unfamiliar terms in the glossary or link to the relevant topic in the Data & Analytics Knowledge Base docs. Spell out abbreviations on first use.


## Technical formatting

Use inline code and preserve exact case for:

| -----| ------| 
| Tables and views:  | `analytics.fct_mktg_leads_deduped`| 
|  Fields and parameters:|  `hashed_email_id`| 
|  Literal values: | `'SPAM'`, `TRUE`, `NULL`| 
|  Files, jobs, APIs, and paths:|  `models/attribution.sql`| 

- Bold interface labels and approved metrics on first definition.   
- Put multi-line queries in fenced Markdown code blocks with a language identifier.   
- Remove credentials or sensitive information.

## Callouts

Use standardized callouts:

| ---| --| 
| **Note:** | Supporting context or a caveat | 
|  **Tip:** | An optional recommendation and its benefit| 
|  **Caution:** | A condition that may affect interpretation| 
|  **Warning:** | A material reporting, security, compliance, or production risk| 
|  **Beta:** | A feature or method still under restricted testing| 

## Links and dependencies

- Use descriptive link text, not **click here**.
- Link to approved, maintained content at the point of need, and place prerequisite links before procedural steps.  
- Name the target page or section instead of using  **above** or  **below**.
- For dependencies, identify the upstream or downstream asset, relationship, effect of delay or change, owner, and canonical reference.
- Link only the first meaningful mention in a section and keep related resources selective.
