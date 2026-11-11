# Inbound receiving exception trace

When what arrived does not match the advance shipment notice, the receiving supervisor or inventory controller gets the notice, the packing list and the scans side by side by item and lot, with missing references and questions to investigate. Nothing is adjusted and nobody is contacted.

*Capability template · Logistics and trade · Supply chain and inventory · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/inbound-receiving-exception-trace/)*

## The outcome

A truck is unloaded, the scans are in, and the counts do not agree with the advance shipment notice. Without a comparison, the first hour goes on working out which record to believe. This capability does that work in one pass. Every item and lot gets a line showing what the notice said to expect, what the supplier's packing list says was packed and what the scanners recorded, all in the item's own unit.

Each difference is read against the three records. Each line that differs says which records agree and which do not, so the supervisor sees at once whether the scans, the packing list or the notice stands apart. Where a shortage in one lot is matched by an unexpected quantity in another lot of the same item, the comparison says so.

The work is honest about what it cannot settle. A scan number used twice, a pallet carrying two lots, a unit the item master does not recognize and an item that is not in the item master are each listed and left open. Then the missing references are listed, and each open point is written as a question for the supervisor and the inventory controller.

It records no stock correction, assigns no fault and writes to no supplier. The supervisor counts what is on the dock and decides what follows.

## Who starts the work, and when

The receiving supervisor or the inventory controller starts it once a delivery has been scanned and the counts look wrong, before any correction is entered or any supplier is asked about it. A receiving clerk can run it for either. It covers one advance shipment notice at a time.

The receiving supervisor verifies the counts on the dock and decides whether to correct inventory records or follow up with the supplier. The inventory controller makes any correction in the stock system after that decision.

## What they supply

- **The advance shipment notice:** what the supplier said was coming, by line, item, lot and quantity.
- **The packing list** that came with the goods, by item, lot and quantity.
- **The receiving scan export** for this delivery only: each scan with its pallet, item, lot, quantity and unit.
- **The item master:** each item's base unit, how many units are in a carton or on a pallet, and whether the item is tracked by lot.
- **Settings:** the business, the receiving date, the two people who receive the result, and the quantity tolerance if you allow one.

Each file's column headers are checked first. If one does not match, the work stops and asks which column is which. It works from the files you supply and needs no connection to your systems.

## What comes out

One page in a fixed order: a summary, data checks, a comparison with one line for each item and lot, the missing references, and numbered questions for the receiving supervisor and the inventory controller. A section with nothing in it says "None."

Every figure can be traced to a row in a file you supplied, and each conversion from cartons or pallets is shown. See the worked example below.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): the point where the stock system first meets what physically arrived.
- [Procurement and suppliers](https://fullypowered.ai/functions/procurement-and-suppliers/): the facts a buyer needs before anyone raises a difference with a supplier.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): warehouses and distribution centres that receive many deliveries a day against notices.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): stores and online sellers whose stock for sale depends on receiving being right.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): inbound parts and materials, many tracked by lot.
- [Consumer brands](https://fullypowered.ai/industries/consumer-brands/): brands receiving finished goods from contract manufacturers into their own or a partner's warehouse.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when receiving differences are sorted out from memory and a shared spreadsheet.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when more deliveries a day make the habit of eyeballing the dock stop working.

It compares one delivery against its notice. Comparing a physical count of stock against the books is [stock count reconciliation](https://fullypowered.ai/capabilities/stock-count-reconciliation/). Checking the papers on a finished outgoing order is [shipment documentation check](https://fullypowered.ai/capabilities/shipment-documentation-check/). Comparing supplier promised dates is [supplier delivery date check](https://fullypowered.ai/capabilities/supplier-delivery-date-check/).

## What has to change for your company

- **Your export headers,** set once so the column check passes without a question.
- **Your quantity tolerance,** if your suppliers may ship a few units over or under.
- **Your unit words,** if you receive in something other than the item's base unit, cartons or pallets.
- **Who decides** whether a count is verified, whether a correction is made and whether a supplier is approached, and who makes the entry in the stock system.
- **Your scan export,** limited to one delivery, with the pallet, item, lot, quantity and unit on each row.
- **Your AI product.** It is written to run in ChatGPT, Claude, Copilot or Gemini from the files you supply. It changes nothing in your systems and never asks for a password.

## What has been checked

Fully Powered AI wrote this capability template in its own words from its own map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026, and the record of that run is published with the template. The run found a few unclear points in the instructions, and the template was corrected for them afterwards. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a few past deliveries your receiving supervisor remembers well, with hard cases written in advance: a renamed column, a pallet scanned twice, a delivery in cartons where the notice is in single units, a lot on the packing list that the notice leaves blank, a shortage in one lot and a surplus in another, and an item that is not in the item master. The supervisor checks every line against the files and the dock before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/capabilities/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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

- [Stock count reconciliation](https://fullypowered.ai/capabilities/stock-count-reconciliation/)
- [Shipment documentation check](https://fullypowered.ai/capabilities/shipment-documentation-check/)
- [Supplier delivery date check](https://fullypowered.ai/capabilities/supplier-delivery-date-check/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
