# Query to Data Map

This file defines how natural-language questions should be translated into structured data tasks inside the California crime chatbot project.

The goal is not just to answer questions. The goal is to identify what kind of question the user is really asking, what evidence the question requires, and which data source or retrieval path best fits that need.

## Core idea

Every user query contains at least four things:
- a topic
- an intent
- a time frame, explicit or implied
- a tolerance for ambiguity

The system should map the query to a data path, not just a verbal answer.

## Query modes

The system should classify each user question into one primary query mode.

### 1. Lookup
User wants a specific fact or value.
Example:
- What is the violent crime rate in Alameda County?

### 2. Comparison
User wants to compare two or more entities.
Example:
- Compare Los Angeles County and Orange County violent crime trends.

### 3. Trend
User wants change over time.
Example:
- Has violent crime gone up in Sacramento over the last five years?

### 4. Ranking
User wants highest, lowest, fastest-rising, or outlier results.
Example:
- Which California counties have the highest violent crime rates?

### 5. Definition
User wants help understanding the dataset, field, or metric.
Example:
- What does violent crime include in this dataset?

### 6. Source selection
User wants to know which dataset should answer a certain question.
Example:
- What public data source should I use for city-level crime?

### 7. Ambiguous concern
User asks in vague, slang-heavy, or emotionally loaded language.
Example:
- Where is crime popping off?
- What areas are getting sketchy?

### 8. Analyst framing
User speaks in shorthand and expects compressed analytical output.
Example:
- Pull biggest risers in CA violent crime.

## Query-to-data routing table

| Query mode | User language pattern | System task | Best data path | Response style |
|---|---|---|---|---|
| Lookup | direct fact request | retrieve one metric or record | single dataset lookup | concise factual answer |
| Comparison | compare X vs Y | retrieve parallel values | same metric across two places or periods | side-by-side comparison |
| Trend | over time, lately, since, change | retrieve time series | yearly or periodic trend data | short trend summary |
| Ranking | highest, lowest, worst, best, rising | sort and rank results | statewide or multi-county dataset | ranked list with caveats |
| Definition | what does this mean, what counts as | explain schema or metric | metadata or documentation layer | explanatory answer |
| Source selection | what dataset should I use | route to correct source | source catalog layer | recommendation with reason |
| Ambiguous concern | rough, sketchy, bad area, popping off | infer likely metric, request clarification if needed | clarification layer before retrieval | cautious and clarifying |
| Analyst framing | pull, run, trend, risers, outliers | translate shorthand to structured request | direct routing to query template | compressed analytical output |

## Hidden variables inside a query

A user question may contain hidden analytical variables even when they are not explicitly stated.

### Concern level
Some questions are emotionally loaded rather than statistically precise.
Examples:
- Is LA getting rough again?
- What places are getting bad?

These should be treated as concern-driven queries, not fully specified analytical requests.

### Precision level
Some users want exact metrics. Others want directional insight.
Examples:
- exact: What was the violent crime rate in 2023?
- directional: Is this county trending worse?

### Evidence expectation
Some questions imply the user wants:
- a single number
- a ranking
- a summary trend
- a dataset recommendation
- a clarification before retrieval

### Vocabulary distance
Some users speak close to the dataset language.
Examples:
- violent crime rate
- county-level trend

Others speak far from the dataset language.
Examples:
- hot spots
- sketchy
- popping off
- getting rough

The system should detect the distance between user language and formal data vocabulary, then decide whether to answer directly or clarify first.

## Example mappings

### Example 1
User query:
- Which California counties have the highest violent crime rates?

Interpretation:
- mode: ranking
- topic: violent crime
- geography: California counties
- time frame: latest available
- evidence expectation: ranked list

Data path:
- statewide county-level violent crime dataset
- sort descending by violent crime rate
- return top results with source note

### Example 2
User query:
- Is LA getting rough again?

Interpretation:
- mode: ambiguous concern
- likely topic: violent crime or overall public safety concern
- geography: Los Angeles
- time frame: recent trend implied
- clarification needed: yes

Data path:
- ask follow-up question about metric, geography, and time frame
- if user stays broad, default to latest violent crime trend with a caution note

### Example 3
User query:
- Pull biggest risers in CA violent crime.

Interpretation:
- mode: analyst framing
- topic: violent crime
- geography: California
- task: identify largest increases
- style: compressed analytical output

Data path:
- compute change over time across counties
- rank largest increases
- return short bullet summary

## Routing guardrails

The system should not:
- assume that vague concern words map perfectly to one crime metric
- answer ranking questions without specifying the time frame
- compare entities using mismatched datasets
- invent city-level answers when only county-level data exists
- treat informal language as low-value input

The system should:
- ask clarifying questions when precision is missing
- preserve user intent even when language is sloppy
- remain grounded in the actual coverage of the dataset
- explain when the requested answer exceeds the available data

## Design philosophy

This project treats queries as analytical signals, not just sentences.

A useful intelligence-style chatbot should do three things well:
1. understand what kind of question the user is asking
2. choose the right data path instead of forcing every query into one template
3. answer with the right balance of precision, caution, and usefulness

The mapping layer is where natural language becomes operational.


