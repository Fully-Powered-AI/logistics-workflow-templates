# Carrier freight invoice check

The freight auditor gets a carrier invoice checked line by line against the shipment export and the rate confirmation: duplicate lines, rate differences and extra charges with no delivery or waiting-time record, each tied to its shipment. Accounts payable decides what to pay or dispute.

*Workflow template · Logistics and trade · Finance and accounting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/carrier-freight-invoice-check/)*

## The outcome

When a carrier invoice arrives with extras on it, or a total that is not what the shipments led you to expect, the freight auditor has one page that shows where every line stands. Each line is matched to its shipment and to the amount the rate confirmation gave for that charge, and each ends in exactly one place: matched, duplicate, rate difference, not on the rate confirmation, support missing, or shipment not found.

Every line in question lists the facts behind it. A repeated line names the line it repeats. A rate difference shows the billed amount, the confirmed amount and the gap. An extra charge such as detention or a liftgate shows whether a delivery or waiting-time record was supplied for that shipment, and for waiting time it works out the minutes between arrival and departure from the times in the record.

The totals tie back to the invoice: the amounts in each group add up to the invoice total, and the page says how much is in question and how much is not. The check compares amounts. It does not read the wording of the rate confirmation, so what a free-time clause or a cap means stays with the people who agreed it.

## Who starts the work, and when

The freight auditor or an accounts payable clerk starts it when a carrier invoice arrives that carries extra charges or does not match the expected cost, before the invoice goes to payment. The freight auditor verifies the match line by line. Accounts payable approves payment or a dispute. The workflow template pays nothing, disputes nothing and contacts no carrier.

## What they supply

- **The carrier invoice,** one row per charge line: invoice, line number, shipment, carrier, charge type and amount.
- **The shipment export** for the shipments billed: shipment, carrier, ship date, lane and delivered date.
- **The rate confirmation,** one row per agreed charge: shipment, charge type and confirmed amount.
- **Delivery and waiting-time records** for any extra charge: shipment, charge type, the kind of record, and arrival and departure times where they apply.
- **The settings:** the invoice date, today's date, the roles involved, the currency, how far an amount may differ and still match, and, only if your rate confirmation states it, the free waiting minutes.

The headers of each file are checked first. If one does not match, the work stops and asks which column is which.

## What comes out

One page in a fixed order: data checks, totals that tie to the invoice, each line in question with its facts, the matched lines, the waiting-time facts, and the decisions for accounts payable. A section with nothing in it says "None." The last lines say what was not supplied or not checked, and that a match is not authority to pay.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Finance and accounting](https://fullypowered.ai/functions/finance-and-accounting/): the check that sits between receiving a carrier invoice and approving it, on one fixed method whoever runs it.
- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): freight charges read against the shipments that caused them.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): businesses that book freight through several carriers and receive invoices in their own formats.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): inbound and outbound freight where accessorial charges creep into invoices.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): parcel and freight invoices with many small lines, where one repeated line is easy to miss.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when freight volume has outgrown a spot check.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when rate confirmations and invoices have been matched by eye for years.

Checking supplier bills for goods and services before a payment run is [supplier bill review and payment run preparation](https://fullypowered.ai/workflows/supplier-bill-review-and-payment-run-preparation/). Comparing carriers on delivery, damage and cost across a period is [carrier performance review](https://fullypowered.ai/workflows/carrier-performance-review/). This workflow template looks at one carrier's invoice.

## What has to change for your company

- **Your file layouts,** set once so the header check passes without a question.
- **Your charge types,** if you use names beyond linehaul, fuel, detention, liftgate, lumper and other.
- **How far an amount may differ** and still count as matching; the default is no difference at all.
- **Free waiting minutes,** if your rate confirmations state them, so the page can set minutes waited against them.
- **Which records count as support** for each extra charge, and where your team keeps them.
- **Who verifies and who approves,** and how a dispute reaches the carrier, which is done by a person outside this workflow template.
- **Your AI product.** It runs in ChatGPT, Claude, Copilot or Gemini from the files you supply. It needs no connection to your accounting or transport systems, contacts no carrier and never asks for a password.

## What has been checked

Fully Powered AI wrote this workflow template in its own words. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026, and the record is published with it. Any edits made after the trial have not been run again. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on invoices your freight auditor has already checked by hand, plus hard cases written in advance, each with its expected behavior: a renamed column, a repeated line, a charge on a shipment not in the export, a detention charge with no departure time, a credit line. The freight auditor checks every figure against the invoice and the rate confirmation before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/) builds that test set, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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

- [Supplier bill review and payment-run preparation](https://fullypowered.ai/workflows/supplier-bill-review-and-payment-run-preparation/)
- [Carrier performance review](https://fullypowered.ai/workflows/carrier-performance-review/)
- [Product landed cost worksheet](https://fullypowered.ai/workflows/product-landed-cost-worksheet/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
