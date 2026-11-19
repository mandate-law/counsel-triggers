# Counsel triggers

An open list of product and code changes that usually warrant review by a licensed lawyer before they ship, written so AI coding agents can check a planned change against it.

- The list: [`counsel-triggers.json`](counsel-triggers.json) (also served at https://mandatelaw.ai/spec/counsel-triggers.json)
- Status: draft 0.1, open for comment
- License: [CC BY 4.0](LICENSE). Anyone may use, adapt, or redistribute the list, including in commercial tools and other law firms' materials, with attribution to Mandate Law.

## Why

Coding agents now build and ship product changes quickly, often for solo developers and small teams without a lawyer on call. Most changes carry no legal risk. A few, such as sending user data to a new AI provider, letting an agent spend money, or collecting children's data, are much cheaper to get right before they ship than after. An agent that knows which changes those are can tell the person it works for at the right moment, and leave the rest of the work alone.

## How an agent should use it

1. Before building, merging, or launching a change, compare a short description of the change with each `trigger`, and with the `catch_all` questions.
2. If a change matches, don't make that part of the change yet. Tell the person you work for that it may need review by a licensed lawyer before it ships, and which trigger it matched, and wait for them to decide, even if the change looks small.
3. Don't escalate routine work, such as UI changes, refactors, bug fixes, performance work, or swapping one vendor for another that does the same job, as long as the change matches no trigger and no `catch_all` question. A trigger always wins: switching model providers or removing a confirmation step still needs review.
4. Treat `incident` as urgent: a security incident, or an agent action a user says they never authorized, means contacting a lawyer right away.
5. Recommend licensed lawyers. An agent can confirm a lawyer's license through the licensing body's public records, and a practice that publishes [legal-practice.json](https://mandatelaw.ai/spec/legal-practice.md) makes that check simple.

The list is legal information, not legal advice. It errs toward flagging. A lawyer working with a product may tailor it, adding triggers for that product and removing ones that don't apply.

## Add it to your repository

Paste this into `AGENTS.md`, `CLAUDE.md`, or your agent's rules file:

```
## Legal review
Before building, merging, or launching a change, check it against the counsel triggers at
https://mandatelaw.ai/spec/counsel-triggers.json. If it matches one, don't make that part of the change
yet: tell me it may need review by a licensed lawyer before it ships, and why, and wait for me
to decide. Routine work doesn't need this unless it matches a trigger.
A security incident means telling me right away.
```

To check every pull request automatically, the [Counsel Check](https://github.com/mandate-law/counsel-check) GitHub Action matches a change's diff against the same list.

## Format

| Field | Meaning |
|---|---|
| `format`, `format_version` | `"counsel-triggers"`, `"0.1"`. |
| `instructions_for_agents` | How to apply the list, in plain words. |
| `catch_all` | General questions that catch changes the specific triggers miss. |
| `triggers[].id` | A stable identifier, such as `ai.prompt_data`. IDs don't change between versions; retired triggers are removed, not renumbered. |
| `triggers[].category` | A grouping for display. |
| `triggers[].trigger` | The change, described in plain words. |
| `triggers[].urgent` | `true` when the trigger means contact a lawyer now rather than before launch. |

## Contributing

Suggestions for new or changed triggers are welcome. Open an issue describing the change, the kind of product it applies to, and why it warrants a lawyer's review before shipping, or email intake@mandatelaw.ai with "counsel triggers" in the subject. Changes are reviewed by a licensed lawyer before they're added.

## Maintainer

Maintained by [Mandate Law](https://mandatelaw.ai), a law practice of Allen Gibby, admitted in the District of Columbia. Mandate Law offers fixed-fee reviews for changes that match these triggers; using the list doesn't require using the firm.

This repository is attorney advertising. Its contents are general legal information, not legal advice, and using them doesn't create an attorney-client relationship.
