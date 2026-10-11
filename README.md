# Colosseum Arena Submit

A Claude skill that fills in your [Colosseum Arena](https://colosseum.com/arena) hackathon submission form with you. Claude operates the form in the browser while you just chat.

## Why use it

- **No blank page.** Claude drafts each answer from your pitch deck and X, right in the form.
- **Edit by chat.** Say "make this shorter" and the field is rewritten on screen.
- **Nothing missed.** Every empty field, the prior work disclosure, and the Accelerator toggle are checked before you submit.
- **Safe.** Claude never clicks Save or Submit. You do.

## Features

- Fills the form tab by tab: Project details, Media and code, Accelerator
- Asks one question at a time with clickable choices
- Uses only your facts (pitch deck, X, chat). No made-up numbers
- Warns if the Accelerator toggle is off
- Checks that your live product link opens for judges
- Pre-submit check before you click `Save and review`

You do by hand: upload the logo, invite teammates, click `Save draft`, `Save and review`, and the final submit button.

## Install

1. Download `SKILL.zip` from [Releases](../../releases/latest).
2. In Claude desktop, open **Settings > Customize > Skills** and upload the zip.
3. (Recommended) Also install the [one-liner](https://github.com/256hax/one-liner) skill. It is used for the Brief description.

## Run

1. Start a new chat in Claude desktop with **Opus** and **Effort: Medium or higher**.
2. Type:
   ```
   Help me draft answers for Arena at the Colosseum hackathon submission form.
   ```
3. Sign in to Colosseum (team leader account) and X when asked, then follow the chat.

## Disclaimer

This is an unofficial community project, not affiliated with or endorsed by Colosseum or Superteam. Use it at your own risk. It is provided as is, with no warranty: review every answer yourself before you submit, and the author is not responsible for any result of your submission.
