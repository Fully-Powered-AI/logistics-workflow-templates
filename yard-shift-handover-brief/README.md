# Yard shift handover brief

The outgoing yard or warehouse lead hands the incoming lead one brief: where each trailer stands, how long it has been on site, which dock issues are open and who follows up on each. No trailer is moved and no appointment is changed.

*Workflow template · Logistics and trade · Operations and process improvement · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflow templates/yard-shift-handover-brief/)*

## The outcome

A shift change is where yard knowledge goes missing. The outgoing lead knows that one trailer has been parked since yesterday, that a dock door has a damaged seal, and that nobody is sure where another trailer was left. The incoming lead usually hears some of it standing at the gate. This workflow template puts it on one page before the handover.

You get every trailer on the site with its carrier, load, location, status and whether it is loaded, how long it has been in the yard, and the appointments that are due or overdue. Each open dock issue is listed with the person who owns it. Where two records disagree, the brief shows both and does not pick one. Where a record is missing or out of date, it says so. At the bottom, each open item has an owner and a question.

The brief does not tell anyone what to do with a trailer. Dispatch decides every movement and every appointment.

## Who starts the work, and when

The outgoing yard lead, the warehouse shift lead or a coordinator working for either starts it shortly before the shift ends, once the exports are fresh. Run it again if the exports are refreshed or a conflict is resolved on the ground.

The outgoing lead checks the brief against what they have seen and the incoming lead accepts it. Dispatch approves any movement or appointment change. The workflow template contacts nobody and updates nothing.

## What they supply

- **The yard export:** the trailers the system shows on site, with carrier, load, location, status, load state, arrival time and door.
- **The gate log:** the in and out events at the gate.
- **The appointment board:** inbound and outbound appointments with door, time and status.
- **The exception notes:** dock and yard issues raised during the shift, with an owner and whether each is open.
- **The confirmed dispatch updates:** location, load state or status that dispatch has confirmed.
- **Settings:** the handover time, the two leads, the time each export was taken, and the follow-up role for each kind of item.

Each file's column headers are checked first. If one does not match, the work stops and asks which column is which. It works from files you supply and needs no connection to your systems.

## What comes out

One page in a fixed order: a check of each export's age, the trailers with their dwell time, the appointments to watch, the open dock issues, the conflicts and unknowns, and a numbered list of follow-ups, each with an owner and a question. A section with nothing in it says "None." The page ends with lines for the outgoing lead to verify, the incoming lead to accept and dispatch to approve, all left empty for people to complete.

Every figure can be checked against the files you supplied, and each item names the record it comes from.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Operations and process improvement](https://fullypowered.ai/functions/operations-and-process-improvement/): the daily handover that keeps yard control, the dock and dispatch working from the same facts.
- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): the trailers, loads and dock doors where stock enters and leaves.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): yards and cross-dock sites where trailers wait between gate, door and dispatch.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): plants with a shipping and receiving yard that changes hands between shifts.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): fulfilment sites with inbound trailers waiting for a door.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when the handover lives in a notebook and a conversation at the gate.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when more trailers pass through than one lead can hold in their head.

It covers one yard and one shift change. An office's weekly list of open matters is [weekly open matter check](https://fullypowered.ai/workflows/weekly-open-matter-check/). The record that passes a client from the seller to the account manager is [account handoff](https://fullypowered.ai/workflows/account-handoff/). The comparison of one finished order's papers with its quantities is [shipment documentation check](https://fullypowered.ai/workflows/shipment-documentation-check/).

## What has to change for your company

- **Your export headers,** set once so the column check passes without a question.
- **Your dwell threshold,** which depends on your carriers, your free time and your yard space.
- **How old an export may be** before the brief calls it stale.
- **Your words** for a completed appointment, a closed note, and an unknown location.
- **Your follow-up roles:** who owns conflicts, long dwell and appointment problems when a note does not name someone.
- **Who verifies, who accepts and who approves.** The leads and dispatch are named in your settings.
- **Your AI product.** It is written to run in ChatGPT, Claude, Copilot or Gemini from the files you supply. It sends nothing and never asks for a password.

## What has been checked

Fully Powered AI wrote this workflow template in its own words from its own map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026; the record is published with it. Edits made after that trial (the rule for which items go to dispatch, follow-up numbering, one question per item, dates on every time, the example's timeline and some clarifying wording) have not been run again. It has not yet been tested in a client environment.

Testing in your environment means running it on a past shift your leads remember well, plus hard cases written in advance with their expected results: a renamed column, a trailer the gate log shows as departed, an unknown location, a note with no owner, a stale appointment board. The outgoing lead checks every item against the files before anyone relies on it.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete workflow template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the workflow template drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related workflow templates

- [Weekly open-matter check](https://fullypowered.ai/workflow templates/weekly-open-matter-check/)
- [Account handoff](https://fullypowered.ai/workflow templates/account-handoff/)
- [Shipment documentation check](https://fullypowered.ai/workflow templates/shipment-documentation-check/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
