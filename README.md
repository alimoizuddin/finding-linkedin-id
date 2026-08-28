# Find Public LinkedIn Profiles

A portable Codex skill for verifying and writing public LinkedIn profile URLs for leads in a spreadsheet.

It treats precision as the priority: an unresolved cell is better than a convincing but unverified match.

## What it does

- Reads the requested lead rows and preserves unrelated workbook content
- Researches only public sources and observed direct LinkedIn `/in/` profiles
- Requires a matching name, company evidence, a second matching attribute, and no contradiction before writing a URL
- Keeps compact research notes outside the workbook
- Reopens and checks the saved workbook before handoff

## Important boundaries

- Does not use Sales Navigator unless the user explicitly requests it
- Never constructs or guesses a LinkedIn profile slug
- Never replaces an existing URL unless asked
- Leaves ambiguous, conflicting, or unverified rows blank
- Does not buy data, install a service, or add evidence columns without a request

## Use

Place `SKILL.md` in your Codex skills directory, then ask Codex to verify or enrich the LinkedIn URL column in a workbook. The skill contains the complete evidence rules and quality gates.

## Repository contents

- `SKILL.md` is the complete skill definition.
- `LICENSE` is the MIT license.

No spreadsheets, lead records, research notes, browser sessions, credentials, or other private material are included.
