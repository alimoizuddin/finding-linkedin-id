---
name: finding-linkedin-id
description: Find, verify, and write public LinkedIn profile URLs for spreadsheet leads. Use when a lead list contains names, companies, and roles and the user wants existing LinkedIn URLs checked or a batch enriched without relying on Sales Navigator.
---

# Find Public LinkedIn Profiles

Enrich only the rows the user requested. Optimize for precision: a blank cell is better than a plausible but unverified profile. Use public web and LinkedIn pages; do not buy data, install a service, or use Sales Navigator solely to recover a public profile URL unless the user explicitly asks.

## Establish Scope

1. Read the workbook, identify the lead fields and LinkedIn URL column, and render the relevant rows before editing.
2. Resolve the target rows before researching:
   - For an explicit range, use exactly that range.
   - For "next N" with a known prior batch boundary, use the next N data rows after that boundary.
   - Otherwise, use the first N eligible rows with blank LinkedIn URL cells, in worksheet order.
   - Do not count headers, fully blank rows, or rows outside the lead table.
3. Recheck populated URLs only when the user asks. Never replace an existing URL merely because another candidate ranks higher in search.
4. Record the target row numbers and original cell values so the final verification covers exactly the intended cells.

## Research Each Lead

1. Normalize the input for searching without changing the workbook:
   - Remove decorative emojis, honorific punctuation, and repeated symbols from names.
   - Try canonical company names alongside trademark marks, ampersands, parentheticals, abbreviations, and slash variants.
   - Treat shortened names, title suffixes, renamed companies, and changed locations as variants, not proof.
2. Start with a focused public query: `site:linkedin.com/in "Name" "Company"`. Batch independent queries when supported.
3. If the result is incomplete or ambiguous, use only the minimum useful escalation:
   - Search the exact name with role and company.
   - Inspect the strongest public LinkedIn profile result.
   - Inspect the company's official website, LinkedIn page, or employee listing.
   - Search for a public LinkedIn post authored by the candidate that connects the person to the company or role.
4. On a company employee listing, click the person's name to recover the direct public profile slug. A people-directory or employee-list URL may corroborate identity but is not the final profile URL.
5. Stop once a candidate passes the acceptance gate with no contradiction. If the available evidence remains ambiguous after reasonable targeted checks, leave the row unresolved rather than broadening into guesswork.

## Evidence Rules

Evaluate the person, company, role, location, and URL together.

Strong identity signals:

- The direct LinkedIn profile shows the matching person, exact current company, and a compatible role.
- An official company team page names the person and role.
- The company's LinkedIn employee listing links that person to the direct profile.
- A public LinkedIn post authored by that profile explicitly connects the person to the company or founder role.

Supporting signals:

- Matching location, industry, education, prior company, distinctive career history, or a close name variant.
- Search-result snippets or third-party pages that repeat matching details.

Evidence is independent only when it comes from a different underlying source. Multiple search results quoting the same LinkedIn profile, or a search snippet plus the page it quotes, count as one source. Reposts, comments, generic people directories, and third-party mentions are supporting evidence only.

Hard contradictions:

- The direct profile clearly belongs to a different person, company, profession, or career history.
- The company or role is incompatible with the workbook and there is no credible renamed-company, prior-company, or role-change explanation.
- The URL is a company, school, search, post, directory, or Sales Navigator page rather than a person's `/in/` profile.

A location mismatch alone is not a hard contradiction when exact company and role evidence identifies a founder or owner.

## Acceptance Gate

Write a URL only when all conditions are true:

1. The profile name is an exact or credible variant of the workbook name.
2. At least one strong identity signal ties the profile to the workbook company.
3. A second matching attribute is visible, such as role, company, location, distinctive career history, or independent first-party corroboration. For common names, require exact company plus role or equivalent independent corroboration.
4. No hard contradiction exists.
5. The final URL is taken from an observed direct profile link. Never construct or guess a slug from the person's name.

An exact direct profile showing both the company and distinctive role can satisfy conditions 2 and 3. A bare name match, name plus location, or two correlated search snippets cannot.

For a prior-company match, require an exact public post authored by the profile or independent first-party evidence connecting the person to that company. If the current company differs and no such bridge exists, leave the row blank.

## URL and Workbook Rules

- Accept only public person-profile URLs shaped like `https://<regional-host>.linkedin.com/in/<slug>` or `https://www.linkedin.com/in/<slug>`.
- Remove query strings, fragments, tracking parameters, duplicate slashes, and a trailing slash. Preserve the observed slug; do not invent a canonical spelling.
- Do not assign one profile URL to different people unless the rows are demonstrably the same lead.
- Write only the requested URL cells. Preserve names, companies, roles, formulas, styles, hyperlinks, sheet names, row order, and unrelated worksheets.
- Save through a temporary output and replace the requested workbook only after reopening and verifying the result. Do not leave partial edits if export or verification fails.
- Keep compact research notes outside the workbook: row, accepted URL or unresolved, decisive signals, and contradiction check. Do not add evidence columns unless requested.

## Final Quality Gate

Before finishing:

1. Reopen the saved workbook and confirm the target row count equals resolved rows plus unresolved rows.
2. Confirm every written value is a valid direct `/in/` URL and every unresolved target remains blank.
3. Confirm only intended URL cells changed and no formula errors or duplicate-person conflicts were introduced.
4. Render the edited range and visually check headers, row alignment, URL placement, and formatting.
5. Spot-check common names and any prior-company acceptance against the decisive source.
6. Report the exact rows processed, resolved count, unresolved names/rows, and saved file path. Never describe unresolved rows as completed matches.
