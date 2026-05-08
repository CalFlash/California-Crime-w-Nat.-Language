# Natural Language Scope

This project defines natural language broadly. Users do not need to ask questions in formal database language. The system should handle plain English, slang, shorthand, vague phrasing, and common colloquialisms when mapping a question to California crime data.

## What "natural language" means here

Natural language includes:
- plain spoken English
- incomplete questions
- casual wording
- slang
- colloquialisms
- abbreviations
- region-specific phrasing
- messy analyst-style shorthand

The goal is to interpret what the user means, not just what the user literally says.

## Examples

### Plain language
- Which California counties have the highest violent crime rates?
- Show me crime trends over time in Los Angeles County.

### Casual phrasing
- Where is violent crime running hot?
- What parts of California look worse lately?

### Slang or colloquial phrasing
- Where is crime popping off?
- Which spots are getting sketchy?
- Is LA getting rough again?
- What counties look the most cooked right now?

### Analyst shorthand
- Compare LA vs SF violent trend.
- Need county-level violent crime over time.
- Pull biggest risers in CA crime rate.

## System expectations

The chatbot should:
- recognize that slang may map to formal crime or safety concepts
- translate casual language into a structured data task
- ask a follow-up question when wording is too ambiguous
- avoid pretending vague language has one exact statistical meaning
- distinguish between user intent and dataset capability

## Examples of language mapping

- "getting rough" -> possible mapping to violent crime trend
- "sketchy" -> possible mapping to public-safety concern, but requires clarification
- "popping off" -> possible mapping to increase in reported incidents
- "bad area" -> too vague, likely requires follow-up
- "crime rate" -> may refer to violent crime, property crime, or total reported crime; do not assume without context

## Principle

The system should be tolerant of informal language but strict about factual claims. It can interpret slang, but it should not convert ambiguity into fake precision.
