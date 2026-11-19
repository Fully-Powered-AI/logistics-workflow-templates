# AI workflow templates for logistics and freight teams

FullyPowered Workflow Templates for logistics and trade teams turn the AI your company already pays for into a team that knows how the work is done: a claims coordinator with the freight shortage record packet assembled, a dispatch supervisor with the missed dock window brief prepared, a freight auditor with the carrier invoice checked line by line. 6 workflow templates, made to be customized and deployed. All plain Markdown, all free, MIT license.

We are FullyPowered AI. We build AI workflows for companies, and these are the templates we start from. We publish them because a good starting point should be open to everyone. Copy one. Change it. Make it yours.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** These are templates, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See more examples for logistics and trade teams](https://fullypowered.ai/industries/logistics-and-trade/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=logistics-readme&from=gh-logistics-readme) · [Have one built for your team](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=logistics-readme&from=gh-logistics-readme) Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Who this is for**

- Owners and operations heads who want the AI they pay for working on dock, yard and freight.
- Warehouse, dock and transport leads who want something their team can run this week.
- The coordinator or auditor who does the work, gets a precise brief, and still makes the call.

**What these are for**

- **Your best way of doing it, for the whole team.** One piece of work, written down precisely enough that an assistant prepares it the same way every time.
- **Work you can check.** Every template says what it needs, what it produces, what it checked and what it could not.
- **A person decides.** Anything that sends, posts, pays or changes a record waits for someone to approve it.
- **Tied into your business systems.** A workflow can be designed to pull from the systems your company already runs, and even push data back into them, with guardrails and a person approving. [Browse the Connectors Directory](https://fullypowered.ai/connectors/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=logistics-readme&from=gh-logistics-readme).
- **Free, open and portable.** MIT-licensed plain instructions that run in the assistant or agent your team already uses: ChatGPT, Claude, Claude Code, Claude Cowork, Codex, Copilot, Gemini, Grok, Perplexity.

**Quick start**

1. **Check a carrier invoice in your AI assistant.** Open ChatGPT, Claude, Copilot or Gemini. Copy the text below into it. Then paste in your own carrier invoice lines, the shipment list and the agreed rates. Use made-up or cleaned-up data if you prefer.

   ```text
   You are helping a freight auditor check one carrier invoice. I will paste: the invoice lines (invoice, line, shipment, charge type, amount), the shipment list, the agreed rates by shipment and charge, and any waiting-time or delivery records for extra charges. First check the column names and ask me if any are unclear. Then place every invoice line in exactly one group: matched, duplicate, rate difference, not on the agreed rates, support missing, or shipment not found. For each line in question, show the facts behind it. Show totals that add up to the invoice total. List what you were not given. Compare amounts only; do not interpret contract wording. Do not tell me to pay or dispute anything. I decide, and nothing is sent or changed.
   ```

2. Read what comes back. It marks what it checked and what is left for you. What comes out, with invented data:

   ```text
   CARRIER FREIGHT INVOICE CHECK: Carrier A, invoice INV-A-9142

   For: the accounts payable lead; checked by the freight auditor, run by the freight audit clerk. Invoice dated 2026-11-02; records as supplied on 2026-11-04. Currency dollars.

   Data checks: 17 invoice lines; 7 shipments billed; 1 line on a shipment not in the export or listed under another carrier (line 17). Credit lines: None. Shipment and charge type billed more than once at different amounts: None. Shipments billed with no delivery date: P206 (lines 15, 16). Confirmed charges not invoiced: None. Shipments in the export not on the invoice: None.

   Totals
   - Invoice total: 5,094.50 on 17 lines.
   - Matched: 11 lines, 3,265.50.
   - Duplicate: 1 line, 640.00.
   - Rate difference: 2 lines, billed 614.00; confirmed 587.50; difference 26.50.
   - Not on the rate confirmation: 0 lines, 0.00.
   - Support missing: 2 lines, 195.00.
   - Shipment not found: 1 line, 380.00.
   ```

3. Stop there. You will know if this is for you. When you want it fitted to your company, or built into your agents, [that is what we do](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=logistics-readme&from=gh-logistics-readme).

A person decides: your dock, dispatch, claims and accounts payable people start each workflow, supply the records and make every call, while the template only prepares and checks.

These are examples and a starting point. They are made to be customized to your carriers, documents and records. Work that is not here can be built for your company, as one step or many.

## The workflow templates here today

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

The [FullyPowered Workflows Directory](https://fullypowered.ai/workflows/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=logistics-readme&from=gh-logistics-readme) lists every workflow template across functions and industries, with search. A machine-readable list of this repository is in [index.json](index.json).

For the work these templates come from, by area of the business and by task, see [AI workflow examples for logistics and trade businesses](https://fullypowered.ai/industries/logistics-and-trade/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=logistics-readme&from=gh-logistics-readme).

## Licence and credits

MIT, in [LICENSE](LICENSE) and in every folder. Each folder's SOURCES.md names what the workflow template drew on. Published by [FullyPowered AI](https://fullypowered.ai/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=logistics-readme&from=gh-logistics-readme).
