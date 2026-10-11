# Field Guide

The single source of truth for how to handle each field. What the form contains (types, limits, required) lives in `form-schema.md`.

Each entry uses up to four labels:
- **Plain meaning**: the one line to tell the founder after quoting the form's question.
- **Ask**: how to ask when the answer is missing, with the choices to offer.
- **Write**: how Claude writes the answer. For Claude only; never put it in the question.
- **Check**: what to verify after the founder gives the answer.

Fields with no entry follow the general rules only.

## General rules for text answers

- English. Judges read hundreds of submissions, so lead with the conclusion in the first sentence and prefer concrete numbers and proper nouns.
- Use only facts from the materials or the chat.
- Stay under the limit in `form-schema.md`; the form truncates anything longer. A first pass does not need to fill the limit; keep it tight.
- Colosseum treats the submission as a pitch to its venture fund, not just a product demo. Judges look for founder-market fit, a unique insight, product and execution, market size, clear communication, a viable business, and traction (hackathon FAQ). Let answers show these where the facts support it.

## Project details

### Brief description
- **Write**: two lines, and Claude must not write either line from scratch (self-written versions tend to be lower quality):
  ```
  <One-liner>
  <Blurb>
  ```
  - One-liner: the title or tagline of the pitch deck (it is usually there). If there is none, run the `one-liner` skill.
  - Blurb: a Blurb-like passage from the project's or founder's X (bio, pinned post, or a launch post), quoted as is or trimmed. If there is none, run the `one-liner` skill.
  - If the `one-liner` skill is not installed and a source is missing, leave that line empty and tell the founder.
  - Tell the founder which source each line came from, in one line each.
- **Ask** (choosing the Blurb source): always say what it is for, e.g.
  > Which source should I use for the Blurb (the second line of your Brief description, a 1-2 sentence summary shown on your public project page)?

  Options: the candidate posts or bio you found (a short excerpt of each) / "Generate with the one-liner skill" / "I'll paste one". Never ask a bare "Which post should I use?".

### What are you building, and who is it for?
- **Write**: target user and their problem before features. Pattern: "For X who struggle with Y, we built Z."

### Why did you decide to build this, and why build it now?
- **Write**: personal origin story, plus market or technology timing (why this is possible now).

### What technologies are you using or integrating with to build your product?
- **Write**: comma-separated list of languages, frameworks, key SDKs, infra, and AI tools (the form asks for developer and AI tools too).

### Which chains does your product use?
- **Write**: select every chain actually integrated in this submission, and nothing else. Track prizes are awarded per chain (Solana, Tempo, Hyperliquid (Hypercore or HyperEVM), Zcash, Ethereum L1, Base, Arbitrum, Robinhood Chain), so do not leave out an integrated chain. Use "Other" for chains not listed. If the materials are unclear, ask.

### How does your product use these chains?
- **Write**: what happens onchain (programs, tokens, payments, etc.). Do not stop at "Solana is fast".

### Did anyone not listed on the team here do meaningful work on this project?
- **Plain meaning**: this is for people outside your listed team who did hands-on work (code, design, contractors, former members). Advice from mentors usually does not count.
- **Ask**: "No one" / "Yes, I'll explain". If "No one", leave it empty (optional field).
- **Write**: who did what, factually, in one or two sentences. (The team's own pre-hackathon work goes in the prior work disclosure below, not here.)

### Is there anything else judges should know about your project that isn't captured above?
- **Plain meaning**: optional. Anything judges should know that other fields don't cover, e.g. deployed program addresses or known limitations of the demo.
- **Ask**: first run the **prior work disclosure** below. Then ask "Nothing to add" / "Yes, I'll add something". If the materials contain likely candidates (a program address, a demo limitation), offer them as options ("Add this?"). If there is nothing to add and no prior work, leave it empty.

### Prior work disclosure (always ask)
There is no dedicated field, but the hackathon FAQ requires it: teams may start before the hackathon and may use pre-existing code, but products are judged only on work done during the hackathon, and teams **must disclose all relevant past development work in the submission form**. Misrepresenting the development history can lead to disqualification, a ban from future hackathons, and revoked prizes. Open-source code written by others is not "pre-existing code" and needs no disclosure.
- **Ask** (never skip, even if the materials say nothing): "Did you start building this product before the hackathon started (on the date shown on the hackathon page)?" Options: "No, everything was built during the hackathon" / "Yes, some work existed before".
- **Write** (if yes): ask what existed before and what was built during the hackathon, then disclose it factually in "Is there anything else judges should know". If it concerns the code, also note it in "Please share any important context about your repo".

## Media and code

### Project logo or graphic
- **Ask**: Claude cannot upload files into the form. Ask the founder to drag their logo onto "Project logo or graphic" (Drag and drop or browse) themselves, and mention the accepted formats. Options: "Uploaded" / "Not ready yet".
- **Check**: take a screenshot and confirm the logo preview appears.

### GitHub link
- **Ask**: the direct repo URL. Open-source is one of the judging criteria in the Official Rules, so a public repo is encouraged; a private repo is allowed if shared with `hackathon@colosseum.com`.
- **Plain meaning** (for "Please share any important context about your repo"): judges look at the repo to see that the team itself did significant work during the hackathon (hackathon FAQ). Use this field when the repo is only part of the product, includes unrelated code, or contains pre-hackathon work.

### Demo video and Pitch video
- **Plain meaning**: these are **two different videos**. Demo video: up to 3 min, shows the live product. Pitch video: up to 2 min, who you are, what you are building, and why you; it is one of the first things judges review, so it should be clear, concise, and high quality.
- **Ask**: ask for each URL separately. Reuse a pitch video link from the materials if there is one.
- **Check**: the Official Rules require all submission content to be in English. If a video is not in English, tell the founder. The time limits come from the form; if the FAQ wording differs (it mentions a two-to-three-minute presentation), follow the form.

### Show demo video on the public project page
- **Plain meaning**: this controls whether your demo video also appears on your public project page. Judges can still see it either way. (Your pitch video is always public.)
- **Ask**: read the checkbox's current state first, then "Show it publicly (Recommended)" / "Judges only".
- **Check**: set the checkbox to match the answer (checked = public) whatever its current state, and read it back.

### Live product link
- **Check**: live products are often private or behind a login, so confirm judges can actually open it.
  - Prefer a check without the founder's cookies (a web fetch tool, if available). If only the browser is available, open the URL in a new tab and keep in mind the founder's own sign-ins may hide access problems.
  - Look for: errors (404, 5xx, DNS), a login or password wall, a localhost or private IP address, a preview deployment that requires team access, or a blank page.
  - If it looks fine, say so in one line. If not, tell the founder what you saw and ask: "I'll fix access and give a new link" / "Add access instructions (e.g. a test account)" / "Leave it as is".

### Access instructions
- **Write**: needed when the live product requires a login. Explain how judges get in (e.g. a test account), within 300 characters.

## Team
- **Ask**: there are no fields. Tell the founder:
  - Every member needs their own Colosseum account, must join the hackathon, and must complete their "Complete submission profile" **before the deadline**. The Official Rules disqualify members who have not registered by then.
  - The team leader (the project owner) invites the members and submits. Prizes go to the team leader.
  - Each person can be on only one team, and each team submits only one project.

## Accelerator

### How do you know people actually need, or will need this product?
- **Plain meaning**: what evidence shows real demand for this.
- **Write**: number of user interviews, waitlist size, people already paying for alternatives. Evidence, not opinion.

### How far along are you? Do you have users?
- **Plain meaning**: your current progress and traction, as numbers.
- **Write**: users, volume, MAU, LOIs, product status. Always give numbers with a time frame (e.g. "120 users in 3 weeks").

### Who else is building in this space, and what do you think they're getting wrong?
- **Plain meaning**: this is about your competitors: who else solves this problem (including what users do today instead), and where they fall short.
- **Write**: name them, and commit to one thing they get wrong. Keep it factual, not insulting.

### How do you make money, or how do you plan to?
- **Plain meaning**: your business model.
- **Write**: who pays, for what, how much. If undecided, state the hypothesis and how you will test it.

### How long have you each been working on this? Full time?
- **Plain meaning**: each member's time on this project, and whether it is full time.
- **Write**: facts only, per member.

### Where is each member based, and do you work in-person together?
- **Plain meaning**: where each member lives now, whether you work in the same place, and whether that would change after funding.
- **Write**: facts only, per member.

### Legal entity / investment / fundraising / live token
- **Plain meaning**: simple Yes/No facts. These almost always need to be asked.
- **Ask**: one question each, with "No" / "Yes".
