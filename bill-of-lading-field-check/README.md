# Bill of lading field check

When a draft bill of lading arrives before it is issued, the documentation specialist gets a field-by-field comparison with the booking, the shipper's instructions and the packing list, with every difference marked. Nothing is issued or corrected.

*Capability template · Logistics and trade · Supply chain and inventory · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/bill-of-lading-field-check/)*

## The outcome

A bill of lading is far easier to fix before it is issued than after. A consignee spelled two ways, a port of discharge that was changed on the booking and not on the draft, a seal number with two digits swapped: each of these costs a few minutes now and a good deal more once the document is out. This capability makes the comparison in one pass, while the draft is still a draft.

You get the draft laid next to its sources. Each party, routing and freight-terms field is shown as the draft has it, as the booking has it and as the shipper's instructions have it, and marked as a match or a difference. Each container is compared with the packing list on packages, gross weight and seal. The draft's own totals are added up from its own lines and compared too. What the files cannot settle, such as a missing weight, freight terms that are neither prepaid nor collect, or a booking and a set of instructions that disagree with each other, is listed as an open item.

Every difference ends as a question for the documentation specialist. The capability does not decide which document is right.

## Who starts the work, and when

A documentation specialist at a forwarder, a shipper's documentation desk or a carrier's operations team starts it when a draft bill of lading arrives and before anyone approves it for issue. It can run again on the next draft after corrections are requested.

The specialist confirms which corrections to ask for. The authorized carrier or agent issues the document. The capability issues nothing, changes no draft, contacts nobody, and makes no customs classification, duty or export-control determination.

## What they supply

- **The draft:** its header fields (parties, routing, vessel and voyage, freight terms, total packages and total gross weight) and its cargo lines, each with container number, seal number, description, packages and gross weight.
- **The booking:** the booking reference, the parties, routing, vessel and voyage, freight terms and the number of containers.
- **The shipper's instructions:** the fields the shipper has approved for the document, such as parties and freight terms. Any field may be left out.
- **The packing list,** with container number, seal number, description, packages and gross weight on each line.
- **Settings:** your business, today's date, who the specialist is, the weight tolerance and the freight terms your documents use.

Each file's column headers are checked first. If one does not match, the work stops and asks which column is which. It works from files you supply, needs no connection to your systems and never asks for a password.

## What comes out

One page in a fixed order: a summary and data checks; each header field with the three values side by side and its result; each container against the packing list; the totals; the open items; the differences, numbered; and a numbered question for the documentation specialist on each point that needs a decision. A section with nothing in it says "None."

Every figure can be traced to a row in a file you supplied, and each finding names where it comes from.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): the document that travels with the goods has to describe the goods that were booked and packed.
- [Operations and process improvement](https://fullypowered.ai/functions/operations-and-process-improvement/): a fixed pre-issue check that does not depend on one person's memory.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): forwarding and shipper documentation desks, where several drafts arrive each day.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): exporters who prepare their own shipping instructions and want the draft checked against them.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): sellers and importers moving full containers of stock.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when shipment volume has outgrown a check done by eye.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when the check lives with one experienced person.

It checks one draft bill of lading against the booking, the instructions and the packing list. Checking a finished order's records and certificates before goods leave is [shipment documentation check](https://fullypowered.ai/capabilities/shipment-documentation-check/). Checking supplier bills and preparing a payment run is [supplier bill review and payment run preparation](https://fullypowered.ai/capabilities/supplier-bill-review-and-payment-run-preparation/). Reviewing how carriers have performed is [carrier performance review](https://fullypowered.ai/capabilities/carrier-performance-review/).

## What has to change for your company

- **Your column headers,** set once so the column check passes without a question.
- **Your weight tolerance,** if your documents allow a small difference between the packing list and the draft. The default is none.
- **Your freight terms words,** if you use something other than prepaid and collect.
- **Which source wins** when the booking and the shipper's instructions disagree. The capability never decides this; your specialist or your shipper does.
- **Who confirms corrections,** and who is authorized to issue the document.
- **Your AI product.** It is written to run in ChatGPT, Claude, Copilot or Gemini from the files you supply. It sends nothing and never asks for a password.

## What has been checked

Fully Powered AI wrote this capability template in its own words from its own map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried on its invented example on 10 November 2026 in Claude; the record is published with it, and the run was made by an assistant that had not written the template, before the example's own output was read, and the example was revised afterwards. It has not yet been tested in a client environment.

Testing in your environment means running it on a recent draft that your specialist knows well, plus hard cases written in advance with their expected results: a renamed column, a seal number with transposed digits, a weight that differs by a few kilograms, a notify party the booking and the instructions give differently, freight terms left vague. The specialist checks every finding against the files before anyone relies on it.

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

- [Shipment documentation check](https://fullypowered.ai/capabilities/shipment-documentation-check/)
- [Supplier bill review and payment-run preparation](https://fullypowered.ai/capabilities/supplier-bill-review-and-payment-run-preparation/)
- [Carrier performance review](https://fullypowered.ai/capabilities/carrier-performance-review/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
