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
3. If the first result is insufficient, refine only with quoted name or company terms. Do not weaken the query into a name-only search for common names.
4. Accept a result only when it is a public person profile on `linkedin.com/in/...` and the visible result information strongly matches the person's name and at least one of their position or company.
5. Save the canonical public profile URL: remove query strings, fragments, locale suffixes such as `/en`, and unnecessary `www.` host prefixes.
6. Mark the row `Needs review` instead of guessing when the result is missing, ambiguous, contradictory, or not a person-profile URL.

Do not open any LinkedIn result to inspect the profile. Google is the sole discovery and verification surface for this skill.

## Confidence Rules

Accept only when all apply:

- The result path contains `/in/`.
- The visible result name is an exact or credible variant of the lead name.
- The title or snippet supports the expected position or company.
- No stronger result clearly identifies a different person.

Do not accept LinkedIn company pages, posts, people directories, search pages, Sales Navigator pages, or a guessed slug. For common names, require both position and company in the visible Google evidence.

## Safety And Checkpointing

- Use one query at a time and persist a row-level checkpoint immediately after every decision. For large lists, stop after each small user-approved batch.
- Record `row`, `name`, `company`, `position`, `status`, `url`, query, and a short evidence or unresolved reason. Use `Found`, `Needs review`, or `Not found`; a blank URL alone is not a status.
- If Google shows CAPTCHA, unusual-traffic, sign-in, or verification pages, stop the batch immediately and report the exact resume row.
- Never work around a verification page or send any LinkedIn request.
- Do not connect, message, save, follow, react, or modify LinkedIn data.

## Workbook Completion

Use this only when the user explicitly authorizes workbook edits.

1. Keep the source workbook unchanged while discovery is in progress.
2. Build an enriched copy from the completed checkpoint. Write only `Found` URLs into LinkedIn cells that were blank in the original source.
3. Preserve all pre-existing URLs exactly. Do not add columns, reorder rows, or change unrelated sheets, formulas, formatting, hyperlinks, or validations.
4. Reopen the exported workbook and verify every original populated URL is unchanged, every added value equals a `Found` checkpoint URL and is a canonical public `/in/` URL, and every unresolved original blank remains blank.
5. If the user asks to replace the original, archive the original with a date-time suffix only after the enriched copy passes verification. Then move the verified copy into the original path and perform the same comparison against the archived original.

## Deliverable

Report the processed rows, URL additions, unresolved rows, checkpoint path, and final workbook path. Before handoff, confirm every saved value is a public `/in/...` URL and every unresolved row is clearly marked rather than silently filled.
