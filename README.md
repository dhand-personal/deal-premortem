# deal-premortem

A Claude skill that runs a premortem on one live sales deal.

It assumes the deal has already failed, works backward to the most likely causes using the account's real communications and CRM data, and ends with dated tripwires you can check against.

## Why a premortem

Asking "is this deal on track?" invites reasons to say yes. Asking "it failed, what happened?" gets people to name the risks they were avoiding. The technique comes from Gary Klein's project premortem. This skill applies it to a single open deal and ties every finding to the record, so the output is specific to the account and not a generic list of deal risks.

## What it does

- Builds a sourced baseline: stage, amount, close date, next step, stakeholders, competitors, and what the buyer has said about timing, budget, and decision process.
- Sets a failure date and a failure type, then writes the 5 to 7 most likely causes (fewer for a small deal).
- Tests each cause against two layers: the methodology in use (MEDDPICC, Command of the Message, Sandler, BANT, SPICED, Challenger, or others) and the things no methodology tracks, such as reorgs, spending freezes, security reviews, and procurement lead time.
- Tags each cause as signal present, unknown, or contradicted, with a dated source.
- Names the most likely cause, the most dangerous cause, and the biggest hidden assumption.
- Plays the adversary: the competitor, status quo, or internal skeptic who benefits if the deal fails.
- Ends with 3 to 5 tripwires, each with an observable signal, a check date, and a stop result.

## What it does not do

- It does not assign a forecast category, a score, or a win probability.
- It does not grade qualification. That is a deal review.
- It does not analyze closed deals. Use a postmortem for those. See [deal-postmortem](https://github.com/dhand-personal/deal-postmortem).
- It does not write to your CRM, send messages, or create tasks. It proposes changes and waits for your approval.

## Inputs

- The account name, and which opportunity if more than one is open.
- Communications for the account. The skill uses the `unified-communication` skill if you have it. If not, paste a transcript, email thread, or notes.
- A CRM snapshot, optional. If a HubSpot or Salesforce connector is available, the skill reads the opportunity (read only). Without one, it asks for the close date, amount, and stage.

## Install

The skill is one file, `SKILL.md`, in a folder named `deal-premortem`.

- **Claude (web, desktop, mobile):** zip the `deal-premortem` folder so `SKILL.md` sits inside it, then upload it as a custom skill in your Claude settings. Check Anthropic's current documentation for the exact steps, since the settings layout changes.
- **Claude Code:** copy the `deal-premortem` folder into your skills directory, for example `~/.claude/skills/`.

## Companion skills

This skill works on its own. It is built to pair with:

- `unified-communication`, which gathers email, call transcripts, CRM activity, and notes for an account.
- `crm-deal-updater`, which can log approved tripwires to your CRM.
- `deal-postmortem`, the closed-deal counterpart.

If a companion is not installed, the skill says so and falls back to pasted material or a plain summary.

## Example prompts

- "Run a premortem on the Acme renewal."
- "How could this deal die? Here is the email thread."
- "Poke holes in the Northwind opportunity before my forecast call."

## License

MIT. See [LICENSE](LICENSE).
