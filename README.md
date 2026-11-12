# Fully Powered Workflow Templates: Logistics and Trade

Every shipment accounted for, every exception traced. These workflow templates are written for logistics and distribution businesses. They prepare the checking and tracing around receiving, shipping documents and freight invoices from your own records. They classify nothing for customs and decide no claim: your people do.

This repository holds 6 workflow templates for warehouse, dock and transport leads. Each one is a single piece of work with its own folder: what it is for and who starts it, the complete template an AI assistant follows, a worked example with invented data, what to change for your company, what has been checked, and its sources.

## The workflow templates

- **[Bill of lading field check](bill-of-lading-field-check/)**: When a draft bill of lading arrives before it is issued, the documentation specialist gets a field-by-field comparison with the booking, the shipper's instructions and the packing list, with every difference marked. Nothing is issued or corrected.
- **[Carrier freight invoice check](carrier-freight-invoice-check/)**: The freight auditor gets a carrier invoice checked line by line against the shipment export and the rate confirmation: duplicate lines, rate differences and extra charges with no delivery or waiting-time record, each tied to its shipment. Accounts payable decides what to pay or dispute.
- **[Freight shortage record packet](freight-shortage-record-packet/)**: When a receiver reports missing or damaged freight, the claims coordinator gets one packet lining up dispatch quantities, warehouse scans, bill of lading, proof of delivery, photos and the customer report, with each unanswered question listed. It assigns no fault and sends nothing.
- **[Inbound receiving exception trace](inbound-receiving-exception-trace/)**: When what arrived does not match the advance shipment notice, the receiving supervisor or inventory controller gets the notice, the packing list and the scans side by side by item and lot, with missing references and questions to investigate. Nothing is adjusted and nobody is contacted.
- **[Missed dock window recovery brief](missed-dock-recovery-brief/)**: The dispatch supervisor gets one brief when a truck misses its dock appointment and the reports disagree: each stated arrival time, the receiving cutoff, the appointment record and the questions that need a decision. It contacts no one and books nothing.
- **[Yard shift handover brief](yard-shift-handover-brief/)**: The outgoing yard or warehouse lead hands the incoming lead one brief: where each trailer stands, how long it has been on site, which dock issues are open and who follows up on each. No trailer is moved and no appointment is changed.

## How to use one

Open a folder and start with its README. Every folder stands alone, so copy the one you want and leave the rest. The templates are written for ChatGPT, Claude, Copilot and Gemini: paste the instruction block and the output format in as custom instructions, or load the folder in a product that reads `SKILL.md` packages.

To take the whole collection, press **Use this template** at the top of this page: it copies every folder into a repository in your own account, yours to change.

In every template a person starts the work, supplies the inputs and decides. The template prepares and checks. Anything that sends, posts, pays or changes a record waits for a person to approve it.

## What SKILL.md is

Each folder holds a file named `SKILL.md`. It is the technical file: the same instructions and output format as the template, in the packaged form that AI products which load instructions from a folder read. It is generated from `TEMPLATE.md`, so the two always agree. The workflow template is the whole folder; `SKILL.md` is one way of loading it. If your AI product does not read that format, use `TEMPLATE.md`.

## What "checked" means here

Each folder says exactly what was checked and when: who wrote it, that its sources and rights were reviewed, the date of its editorial review, and whether it has been tried on its invented example in a named AI product. Nothing is described as tested for a client unless it was. Test a template on your own past work before your team relies on it; each one comes with acceptance tests for that.

## More workflow templates

The [Fully Powered Workflows Directory](https://fullypowered.ai/workflows/) lists every workflow template across functions and industries, with search. A machine-readable list of this repository is in [index.json](index.json).

## Licence and credits

MIT, in [LICENSE](LICENSE) and in every folder. Each folder's SOURCES.md names what the workflow template drew on. Published by [Fully Powered AI](https://fullypowered.ai/).
