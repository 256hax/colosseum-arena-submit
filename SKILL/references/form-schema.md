# Colosseum Arena Submission Form Spec

The single source of truth for what the form contains. If Colosseum changes the form, update this file only.
How to handle each field lives in `field-guide.md`.
Last verified: 2026-10-10 (taken from the live form DOM)

Official sources (checked 2026-10-11; the per-field rules drawn from them live in `field-guide.md`):
- Hackathon page: https://colosseum.com/worldsfair
- Hackathon FAQ: https://colosseum.com/hackathon#faqs
- Official Rules: https://colosseum.com/legal/Crypto%20World's%20Fair%20Hackathon%20Rules.pdf
- Contest period (Crypto World's Fair): September 14, 2026 6:00am PT to October 12, 2026 11:59pm PT. For other hackathons, read the dates from the hackathon page.

- Editor URL: `https://colosseum.com/arena/hackathon/project/editor?section=details`
- Tabs: `section=details` / `media` / `team` / `accelerator` (tab labels: Project details / Media and code / Team / Accelerator)
- Field ids are random UUIDs that change. **Locate fields by label text.**
- Owner: `auto` = Claude fills / `try` = Claude tries, falls back to the founder after two failures / `manual` = founder from the start

## Header (shared across tabs)

| Field | Type | Owner |
|---|---|---|
| Accelerator application (`aria-label="Apply to accelerator"`) | switch (`aria-checked`) | auto (SKILL.md Step 4 and Step 8) |

## Project details (`section=details`)

| Label | Type | Limit | Required | Public | Owner |
|---|---|---|---|---|---|
| Project name | text | 100 | yes | Public | auto |
| Brief description | textarea | 500 | yes | Public | auto |
| Project website | text (url) | - | | Public | auto |
| What are you building, and who is it for? | textarea | 1000 | yes | | auto |
| Why did you decide to build this, and why build it now? | textarea | 1000 | yes | | auto |
| What technologies are you using or integrating with to build your product? | text | 500 | yes | | auto |
| Which chains does your product use? | checkbox group (Solana, Tempo, Zcash, Hyperliquid, Base, Robinhood Chain, Arbitrum, Ethereum L1, Other) | - | yes | | auto |
| How does your product use these chains? | textarea | 500 | yes | | auto |
| What category best describes your product? | combobox (searchable) | - | yes | Public | try |
| Is your project a mobile-focused dApp? | checkbox | - | | | auto |
| Where is your team primarily based? | combobox (country) | - | yes | Public | try |
| Please share a team Telegram contact | text | - | yes | | auto |
| Did anyone not listed on the team here do meaningful work on this project? | textarea | 600 | | | auto |
| Is there anything else judges should know about your project that isn't captured above? | textarea | 500 | | | auto |

## Media and code (`section=media`)

| Label | Type | Limit | Required | Public | Owner |
|---|---|---|---|---|---|
| Project logo or graphic | file (JPEG/PNG/WebP/GIF, up to 20 MB; stored at 0.5 MB, GIFs must already be under 0.5 MB) | - | yes | Public | manual |
| GitHub link | text (url) | - | yes | Public | auto |
| Please share any important context about your repo | textarea | 500 | | | auto |
| Please submit a demo video of your product | text (url) | - | yes | | auto |
| Show demo video on the public project page | checkbox | - | | | auto |
| Live product link | text (url) | - | | | auto |
| Access instructions | text | 300 | | | auto |
| Pitch video | text (url) | - | yes | Public | auto |
| X profile | text (@username or URL) | - | | Public | auto |

Constraints stated on the form:
- GitHub: direct repo link only (no org or user profile pages), the code written during the hackathon. A private repo must be shared with `hackathon@colosseum.com`.
- Demo video: YouTube, Loom, or Vimeo, up to 3 min. Shows the live product (not a slide deck, not a code walkthrough).
- Pitch video: YouTube, Loom, or Vimeo, up to 2 min. Separate from the demo video: introduce yourselves, what you are building, why you are the people to build it.
- Telegram: used to reach out about prize distribution and accelerator interviews.

## Team (`section=team`)

| Item | Owner |
|---|---|
| Invite teammates (requires searching for users) | manual |
| Each member's "Complete submission profile" (required to submit, e.g. "0 of 1 complete") | manual |

There are no input fields on this tab.

## Accelerator (`section=accelerator`)

Only relevant when the toggle is on. Answers are visible only to organizers and the Colosseum team.

| Label | Type | Limit | Required | Owner |
|---|---|---|---|---|
| How do you know people actually need, or will need this product? | textarea | 1000 | yes | auto |
| How far along are you? Do you have users? Please be as specific as possible. | textarea | 1000 | yes | auto |
| Who else is building in this space, and what do you think they're getting wrong? | textarea | 1000 | yes | auto |
| How do you make money, or how do you plan to? | textarea | 500 | yes | auto |
| How long have you each been working on this? Have you been working on it full time? | textarea | 500 | yes | auto |
| Where is each member of the team currently based, and do you work in-person together? Would this change after receiving funding? | textarea | 500 | yes | auto |
| Have you formed a legal entity yet? | radio No/Yes | - | yes | auto |
| Have you taken any investment yet? | radio No/Yes | - | yes | auto |
| Are you currently fundraising? | radio No/Yes | - | yes | auto |
| Do you have a live token? | radio No/Yes | - | yes | auto |

## Footer and side panel

| Element | Notes |
|---|---|
| Save draft | Founder clicks (SKILL.md principle 6). Shows "All changes saved" when saved. |
| Save and review | Founder clicks, after the pre-submit check. |
| Final submit (inside Review submission) | Founder clicks. |
| Project preparation panel | "N fields need attention" per tab, "N of M complete" for Team. Use it to find what is left. |
| Deadline | Shown on the page, e.g. "Submit by October 12 at 11:59 PM PDT." Read it from the page every time. |
