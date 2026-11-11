# Freight shortage record packet

When a receiver reports missing or damaged freight, the claims coordinator gets one packet lining up dispatch quantities, warehouse scans, bill of lading, proof of delivery, photos and the customer report, with each unanswered question listed. It assigns no fault and sends nothing.

*Capability template · Logistics and trade · Customer support and service · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/freight-shortage-record-packet/)*

## The outcome

A call comes in that six chairs were not on the pallet, or that two table tops arrived chipped. The records that could explain it sit in six places: the customer's report, the packing list, the warehouse scanner, the bill of lading, the receiver's signed delivery paper and a folder of photos. This capability reads them together and gives you the story in one page, in the order the freight travelled.

For every line the customer reports, you see how many were dispatched, picked, loaded, written on the bill of lading and signed for, with the record behind each figure. The first place the number changes is named. A record that does not exist is listed on its own, apart from a record that exists and disagrees with another, so a missing scan is never mistaken for a count that does not match. The words written on the delivery paper and the captions on the photos are quoted exactly as they were written.

It ends with a numbered list of what nobody has answered yet. Deciding what the records mean, who is responsible and what to say to the carrier or the customer stays with you.

## Who starts the work, and when

The claims coordinator starts it the day a receiver reports a shortage or damage, once the records have been pulled for that one shipment. Run it again when a missing record turns up or the customer sends more photos.

The claims coordinator verifies the packet against the originals and decides every follow-up with carriers, customers and the warehouse. The capability states no liability and no legal or claim position, approves no credit and sends nothing.

## What they supply

- **The customer report:** one row for each reported line, with the item, the kind of problem, the quantity, the date, who reported it and their note.
- **The dispatch lines** from the packing list: item, description, quantity, unit and dispatch date.
- **The warehouse scans** for the shipment: picked and loaded events with quantities, times and places.
- **The bill of lading rows:** item, quantity stated and any remark.
- **The proof of delivery rows:** quantity signed for, delivery date, whether it is signed and any exception note.
- **The photo log:** one row for each photo, with the item if it is known, the date, who took it and a caption.
- **Settings:** today's date, your company, the claims coordinator, and the words your records use.

Every file's column headers are checked first. If one does not match, the work stops and asks which column is which. It works from files you supply and needs no connection to your systems.

## What comes out

One packet in a fixed order: a summary, one block for each reported line with its quantity chain, scans, remarks and photos, the other lines on the shipment that do not agree, photos not tied to a line, the records that are missing, the figures that conflict, and a numbered question for the claims coordinator on every reported line and every other line with a gap. A section with nothing in it says "None."

Every figure names the scan, row or document it comes from, so each can be checked against the originals.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Customer support and service](https://fullypowered.ai/functions/customer-support-and-service/): the person answering the receiver has the facts in one place before replying.
- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): the warehouse and transport records tied to one shipment.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): freight handed to carriers, where the paper is spread across several desks.
- [Ecommerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): bulk orders shipped from a warehouse to a store or a trade customer.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): finished goods sent to customers on pallets.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when the packet is assembled by hand from five systems.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when reports arrive faster than one person can pull the records.

It prepares the record for one shipment after a report. Working out where a production batch went is [batch distribution trace](https://fullypowered.ai/capabilities/batch-distribution-trace/). Applying your policy to a complaint and setting out a refund for approval is [complaint and refund request handling](https://fullypowered.ai/capabilities/complaint-and-refund-request-handling/). Checking the papers before goods leave is [shipment documentation check](https://fullypowered.ai/capabilities/shipment-documentation-check/).

## What has to change for your company

- **Your export headers,** set once so the column check passes without a question.
- **The words your records use** for picked and loaded scans, for short and damaged reports, and for signed.
- **Your quantity tolerance,** if your records allow a few units either way.
- **Who verifies the packet** and who decides follow-up with carriers and customers.
- **Where the originals live,** so that a question the packet raises can be answered from the source.
- **Your AI product.** It is written to run in ChatGPT, Claude, Copilot or Gemini from the files you supply. It sends nothing and never asks for a password.

## What has been checked

Fully Powered AI wrote this capability template in its own words from its own map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026; the record is published with it. Small wording edits made to the instructions and example after that trial have not been run again. It has not yet been tested in a client environment.

Testing in your environment means running it on a recent report your claims coordinator already knows, plus hard cases written in advance with their expected results: a renamed column, a loaded scan that was never recorded, a signed quantity that differs from the bill of lading, a damaged line with no photo, a report for an item that was not dispatched. The claims coordinator checks every figure against the originals before anyone relies on the packet.

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

- [Complaint and refund request handling](https://fullypowered.ai/capabilities/complaint-and-refund-request-handling/)
- [Batch distribution trace](https://fullypowered.ai/capabilities/batch-distribution-trace/)
- [Shipment documentation check](https://fullypowered.ai/capabilities/shipment-documentation-check/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
