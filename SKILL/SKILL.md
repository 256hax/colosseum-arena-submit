---
name: colosseum-arena-submit
description: Helps founders draft and fill in their answers for the Arena at the Colosseum hackathon submission form, end to end. Opens the submission form in the browser first, then fills it section by section while chatting with the founder, drafting answers from their materials and revising fields on request. Always warns when the Accelerator application toggle is off. Trigger when the user mentions "submit to Colosseum", "hackathon submission", "Arena submission", "project submission", "apply to the accelerator", "fill in the submission form", or works with a colosseum.com/arena form, in any language.
---

# Colosseum Arena Submit

The founder looks at the form in the browser and chats; Claude operates the form.
The founder only does four things by hand: **upload the logo / click `Save draft` (Claude prompts them) / invite teammates / click `Save and review` and the final submit button**.

Read both reference files before starting:
- `references/form-schema.md`: what the form contains (labels, types, limits, required, public, who fills each field). The single source of truth for the form.
- `references/field-guide.md`: how to handle each field (plain meaning, how to ask, how to write, what to check). The single source of truth for per-field rules.

## Principles

1. **The form on screen is the workspace.** Open the browser first and work one tab at a time, so the founder always knows "this is the screen we are filling now". Do not prepare a full draft document up front.
2. **Good-enough first pass, then iterate.** Put a reasonable first answer straight into the field and let the founder react to it on screen. Do not polish everything before showing it.
3. **Keep chat short.** The text is visible in the form, so do not paste long answers into chat. Say which fields you filled and flag assumptions in one line each.
4. **Ask just in time, one question at a time.** Ask for a missing fact when you reach the field that needs it, not in a big list at the start.
5. **Never invent facts.** Do not write numbers, traction, background, example answers, or candidates that are not in the materials or chat. Leave the field empty and ask.
6. **Claude never clicks save or submit buttons.** This includes `Save draft`, `Save and review`, and the final submit button, so a misclick can never submit by accident. Claude prompts the founder to click them.
7. **Talk in the founder's language; write form answers in English.**
8. **Never use the em dash (U+2014) or en dash (U+2013).** This applies to every output: form answers, chat replies, and anything else. Write naturally with commas, periods, conjunctions, or parentheses instead. A normal hyphen `-` in compound words (non-vote, stress-test) is fine. Search your text for these characters before typing it into the form or sending it. Do not report the check result ("0 em dashes found", "verified clean"); following the rule is a given, not an achievement. Only if you found and fixed one, say so in one line.

## How to ask

- **Clickable choices.** Whenever a question has a small set of answers, use the multiple-choice question tool if one is available (the UI where the founder clicks an option). Include a free-text or "Skip" option where it makes sense. Fall back to a short numbered list only if no such tool exists. The choice UI cannot show a file upload field; for files, tell the founder to attach them with the paperclip (attach) button in the chat input.
- **Form questions.** Quote the form's question as written, then add **one plain-language line** saying what it is really asking (the "Plain meaning" in `field-guide.md` where available).
- **Do not leak writing tactics.** "Write" guidance in `field-guide.md` (e.g. "commit to one thing they get wrong") is for how Claude writes the answer, never for how the question is phrased.
- **Skipping.** Optional fields can be skipped. Required fields cannot; say so if the founder tries.

## How to operate the form

- Locate fields by **label text** (ids are random UUIDs that change).
- **Text:** click the field, select all, then type (`type` action). The form is React-controlled, so do not set `value` via JS; use real input actions. Read the value back to confirm it landed.
- **Checkboxes / radios / the accelerator toggle:** click, then read the state back to confirm.
- **Comboboxes (category, country):** click, type a search term, click the matching option. **After two failed attempts, switch to manual** and ask the founder: "Please select this one yourself: Category = X".
- **Save draft prompt.** Used at the end of every tab, after edits, and before moving to another tab:
  1. Ask the founder to click `Save draft` at the bottom of the page, with choices: "Saved" / "I can't find it".
  2. Do not move on until they confirm.
  3. Check that the page shows "All changes saved" and that the tab's count in "Project preparation" dropped. If not, ask them to click it again.

## Flow

### Step 1. Recommended model and effort
In your very first message, tell the founder the recommended settings, because a weaker model or less thinking gives noticeably weaker answers:
- **Model: Opus**
- **Effort (thinking): Medium or higher**

If you know you are not running on Opus, say so plainly and suggest switching (in the model picker) and starting a new chat. You cannot see the effort setting, so just state the recommendation. Ask with choices: "Settings are OK, continue" / "I'll change them first". Keep this to a few lines.

### Step 2. Check the one-liner skill
The Brief description depends on the `one-liner` skill (see `field-guide.md`). Check whether a skill named `one-liner` appears in your available skills.
- If it is available, continue.
- If not, tell the founder it is needed and point them to the setup steps in the repository README (section "1. Set up (once)"): https://github.com/256hax/one-liner
  After installing, they start a new chat so the skill is loaded, and ask again to submit to Colosseum.
- Ask with choices: "Install now" / "Continue without it". If they continue without it, the Brief description uses only the pitch deck and X, and a line stays empty for the founder if its source is missing.

### Step 3. Sign in to Colosseum and X
Open two tabs with a browser tool (prefer the Claude desktop built-in browser; otherwise use whatever browser tool is available):
- `https://colosseum.com/arena/hackathon/project/editor?section=details`
- `https://x.com/home`

Ask the founder to sign in to **both** (Claude never types passwords). The Colosseum account should be the team leader's, since the team leader submits the project. X must be signed in, or Claude cannot read the X profiles and posts used as materials. Confirm with choices: "Signed in to both" / "Need help". If no Colosseum project exists yet, guide them to create one.

Then switch back to the Colosseum tab so the form is what the founder sees.

### Step 4. Accelerator toggle (first check)
The toggle sits at the top of every tab, so check it right away.
- Read `aria-checked` on the switch with `aria-label="Apply to accelerator"`.
- Ask with choices: "Are you applying to the Colosseum Accelerator with this submission?" Options: "Yes (Recommended)" / "No". If yes and the toggle is off, turn it on.
- If they choose No, show this warning and ask again with choices ("Apply to the Accelerator" / "I'm sure, don't apply"):
  > Heads up: if the toggle stays off, your submission is not treated as an Accelerator application from this hackathon. Are you sure you do not want to apply?

### Step 5. Materials, one at a time
Ask these three questions in order, one per message, each with choices. Whatever they have now is fine; more can come later.
1. **Pitch material.** Options: "Attach a PDF deck" / "Paste a link (deck or video)" / "Not ready yet". For a PDF, tell them to attach it with the paperclip button. For a link, let them type it in the free-text option or paste it in the next message. If a Google Slides link cannot be read, ask for a PDF.
2. **Project's X account.** Options: "I'll paste it" / "No project account (I'll share a post instead)" / "Skip".
3. **Founder's X account.** If the founder's Colosseum profile already has an X handle, offer it: "Use @handle" / "Use a different one". Otherwise: "I'll paste it" / "Skip".

Read the materials. Reuse them later wherever a field asks for the same thing (e.g. a pitch video link goes into "Pitch video", the project's X into "X profile"). Then move on to the first tab.

### Step 6. Fill tab by tab
Order: Project details, then Media and code, then Accelerator (if applying), then Team (manual).

For each tab:
1. Switch to the tab and tell the founder in one line, e.g. "Now filling: Project details."
2. Work through the fields in small groups (2-4 fields), following `field-guide.md` for each field:
   - If the materials support it, write a first-pass answer and type it into the form.
   - If it needs a fact you do not have, ask now and leave the field empty until answered.
   - Scroll so the filled fields are visible, then tell the founder which fields you filled and any assumption you made.
3. Wait for the founder's reaction, apply edits (Step 7), then continue with the next group.
4. When the first pass is done, go through **every field that is still empty** (required and optional) one by one, with choices such as "I'll paste it" / "Skip (leave empty)".
5. Run the **Save draft prompt**, then move to the next tab.

### Step 7. Edits
When the founder asks for a change ("make this shorter", "mention our 300 users"):
1. Rewrite only that field and overwrite it in the form.
2. Read it back, then say in one line what changed.
3. If the change affects other fields (e.g. a new target user), list those fields and ask before updating them.
4. After a batch of edits on a tab, run the **Save draft prompt**.

### Step 8. Pre-submit check (accelerator gate, second check)
When the founder says they want to submit or review, check the following before they click `Save and review`:
1. Read the toggle's `aria-checked` again.
   - If the founder chose to apply but the toggle is off, **stop and turn it on**.
   - If they chose not to apply, show the Step 4 warning again and get a final confirmation.
2. Read the "Project preparation" panel ("N fields need attention") and list every tab that is not at 0.
3. Confirm there are no empty required fields, and that the prior work disclosure was asked (see `field-guide.md`).
4. Confirm the logo is uploaded, and ask whether the Team tasks are done (every member registered with a completed profile before the deadline).
5. Tell the founder the deadline shown on the page.

If everything passes, tell the founder: "Everything looks ready. Please click `Save and review`, check the review page, then click the final submit button yourself." Claude does not click either button.
