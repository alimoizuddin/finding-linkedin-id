---
name: finding-linkedin-id
description: Find and verify public LinkedIn profile URLs for known leads using Google results only. Use when a lead list has names, positions, and companies and LinkedIn profiles must not be opened.
---

# Google-Only LinkedIn URL Discovery

Use this skill to find a public LinkedIn URL for existing lead records without navigating to LinkedIn, Sales Navigator, company LinkedIn pages, or LinkedIn posts.

## Scope

- Work only on the rows the user requests.
- Treat the source lead row as authoritative for `Name`, `Position`, and `Company`.
- Default output columns are `Name`, `Position`, `Company`, and `LinkedIn URL`.
- Preserve existing valid URLs unless the user explicitly asks to recheck or replace them.
- Do not edit a workbook until the user explicitly authorizes the edit.

## Google-Only Workflow

For each lead:

1. Build one focused query: `Name Position Company LinkedIn`.
2. Read Google search-result titles, displayed URLs, and snippets only.
3. Accept a result only when it is a public person profile on `linkedin.com/in/...` and the visible result information strongly matches the person's name and at least one of their position or company.
4. Save the canonical public profile URL without query strings, fragments, or tracking parameters.
5. Mark the row `Needs review` instead of guessing when the result is missing, ambiguous, contradictory, or not a person-profile URL.

Do not open any LinkedIn result to inspect the profile. Google is the sole discovery and verification surface for this skill.

## Confidence Rules

Accept only when all apply:

- The result path contains `/in/`.
- The visible result name is an exact or credible variant of the lead name.
- The title or snippet supports the expected position or company.
- No stronger result clearly identifies a different person.

Do not accept LinkedIn company pages, posts, people directories, search pages, Sales Navigator pages, or a guessed slug. For common names, require both position and company in the visible Google evidence.

## Safety And Checkpointing

- Use small batches and persist a row-level checkpoint after every query.
- If Google shows CAPTCHA, unusual-traffic, sign-in, or verification pages, stop the batch immediately and report the exact resume row.
- Never work around a verification page or send any LinkedIn request.
- Do not connect, message, save, follow, react, or modify LinkedIn data.

## Deliverable

Report the processed rows, confirmed URLs, unresolved rows, and saved workbook or checkpoint path. Before handoff, confirm every saved value is a public `/in/...` URL and every unresolved row is clearly marked rather than silently filled.
