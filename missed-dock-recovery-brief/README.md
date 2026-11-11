# Missed dock window recovery brief

The dispatch supervisor gets one brief when a truck misses its dock appointment and the reports disagree: each stated arrival time, the receiving cutoff, the appointment record and the questions that need a decision. It contacts no one and books nothing.

*Capability template · Logistics and trade · Operations and process improvement · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/missed-dock-recovery-brief/)*

## The outcome

When a truck misses its slot, three people usually say three different things. The driver gives one arrival time, the carrier's planner another, and the receiving office says what it will and will not take. Phone calls pile up and nobody is sure which statement is the newest or who said it.

This capability puts every stated arrival time on one page, in the order it was reported, each measured in minutes against the end of the appointment window and the receiving cutoff. It shows which source said what and how old each report now is, whether the latest times from different sources agree, and whether the cutoff the receiver quotes matches the one in the appointment record.

It also keeps three things apart that conversations blur. A late arrival counts as accepted only when the receiver said so; a driver passing on what the dock clerk said is shown as the driver's report. A possible fee is quoted from the record and never worked out. And the brief chooses nothing: it ends with the questions the facts raise, and the supervisor answers them.

## Who starts the work, and when

A dispatch supervisor, or a dispatcher or dock coordinator on the supervisor's behalf, starts it when a truck has missed its appointment window and the reports differ. It can be run again when a new report comes in.

The supervisor confirms the facts and decides what happens next, including whether to ask for a changed appointment. The capability contacts no driver, carrier or receiver, books no slot, and changes no appointment.

## What they supply

- **The appointment record** for the shipment: carrier, receiving site, date, window start and end, receiving cutoff, status and any fee terms.
- **The reports received:** for each, when it came in, who it came from, any arrival time or cutoff stated, whether the receiver was said to accept a late arrival, and what was said.
- **Settings:** the shipment reference, the date and time now, the supervisor's role, how far apart two arrival times may be and still agree, and how old a report may be before it is called stale.

Each file's column headers are checked first. If one does not match, the work stops and asks which column is which. It works from the notes and exports you supply and needs no connection to your transport or yard system.

## What comes out

One brief in a fixed order: the appointment record, where things stand now, every stated arrival time, where the reports differ, the receiving cutoff, whether a late arrival is accepted, possible fees, data checks and a numbered list of questions for the supervisor. A section with nothing in it says "None."

Every minute count can be checked with a clock and the reports. Nothing is sent, booked or changed, and no recovery is chosen.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Operations and process improvement](https://fullypowered.ai/functions/operations-and-process-improvement/): a repeatable way to turn a scramble of calls into one set of facts.
- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): inbound loads that stock, production or customer orders are waiting on.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): carriers, dock appointments and receiving cutoffs are the daily material.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): a late inbound load can hold up a production run that was scheduled around it.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): inbound stock to a fulfilment site on a booked dock slot.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when the cutoff and the fee terms live in people's heads and old emails.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when there are more dock appointments than one supervisor can follow by phone.

It looks at one inbound truck and one missed slot. The review of orders that have not gone out is [unshipped order review](https://fullypowered.ai/capabilities/unshipped-order-review/), the comparison of a supplier's promised and revised dates is [supplier delivery date check](https://fullypowered.ai/capabilities/supplier-delivery-date-check/), and the look at a carrier over time is [carrier performance review](https://fullypowered.ai/capabilities/carrier-performance-review/).

## What has to change for your company

- **Your export or note layout,** so the column check passes without a question.
- **Your tolerance and staleness limit:** how many minutes apart two arrival times may be and still agree, and how old a report may be before it is stale.
- **Your roles:** who the supervisor is, and who may ask a receiver for a changed appointment.
- **Where your fee terms and cutoffs are recorded,** so they are in the appointment record when the brief is run.
- **Your AI product.** It is written to run in ChatGPT, Claude, Copilot or Gemini from the files you supply. It sends nothing and never asks for a password or a login code.

## What has been checked

Fully Powered AI wrote this capability template in its own words from its own map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026, and the record is published with it. It has not yet been tested in a client environment.

Testing in your environment means running it on a missed appointment your supervisor remembers well, plus cases written in advance with their expected results: a renamed column, two sources giving arrival times far apart, a receiver cutoff that differs from the record, a driver saying the dock will accept the truck while the receiver says it has not agreed, a blank fee term. The supervisor checks every time and every minute count against the reports before anyone acts.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete capability template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the capability drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related capabilities

- [Unshipped order review](https://fullypowered.ai/capabilities/unshipped-order-review/)
- [Supplier delivery date check](https://fullypowered.ai/capabilities/supplier-delivery-date-check/)
- [Carrier performance review](https://fullypowered.ai/capabilities/carrier-performance-review/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
