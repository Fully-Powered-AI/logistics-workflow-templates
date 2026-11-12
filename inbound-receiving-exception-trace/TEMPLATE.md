# Inbound receiving exception trace

Workflow template, version 0.1.0.

## Purpose

Prepare the comparison a receiving supervisor or inventory controller makes when a delivery's counts do not match the advance shipment notice: the notice, the supplier's packing list and the receiving scans set side by side by item and lot, in one unit. Each difference is read against which of the three records agree, the cases that cannot be settled from the files (a repeated scan number, a pallet carrying two lots, a unit the item master does not recognize, an item the item master does not hold) are listed and left open, the references a record should carry and does not are listed, and each open point becomes a numbered question for the receiving supervisor and the inventory controller. Every figure traces to a row in a supplied file. The assistant prepares; it never adjusts stock, changes a record, contacts a supplier, assigns fault or decides what a difference means.

## When to use it and when not to

Use it after a delivery has been scanned and its counts differ from the notice, before any correction is entered or any supplier is approached. Run it again after the supervisor has recounted on the dock and the scan export has been corrected. One run covers one advance shipment notice and one delivery.

Do not use it:

- to compare a physical stock count with the quantities in the books, which is the stock count reconciliation;
- to check the papers on a finished outgoing order, which is the shipment documentation check;
- to compare the dates a supplier promised, which is the supplier delivery date check;
- to decide who is at fault, whether a claim should be raised or whether goods should be refused. The assistant states what the records show and asks;
- to enter a correction. The supervisor decides it and the inventory controller enters it;
- when the scan export holds scans of more than one delivery. The assistant cannot tell which scans belong to the notice, so the export must be limited to this delivery first.

## Roles

- **Runs it:** a receiving clerk, the receiving supervisor or the inventory controller.
- **Verifies the counts on the dock and decides what follows, whether an inventory correction or a supplier follow-up:** the receiving supervisor. Always a person.
- **Enters any correction in the stock system:** the inventory controller, after the supervisor's decision.
- **Contacts the supplier:** the person the business names, usually purchasing. The assistant contacts nobody and writes no message to a supplier.

## Inputs

The assistant works only from the files the person supplies. It needs no connection to any system and never asks for a password or a login code. Dates are written YYYY-MM-DD. The settings may give the receiving date in words; the assistant reads it as that date and writes it as YYYY-MM-DD.

1. **The advance shipment notice.** One row per notice line. Default column headers: `asn_number`, `line`, `sku`, `lot`, `qty_expected`, `unit`.
2. **The packing list.** One row per packed line. Default column headers: `packing_list_number`, `sku`, `lot`, `qty_packed`, `unit`.
3. **The receiving scan export,** for this delivery only. One row per scan. Default column headers: `scan_id`, `scan_time`, `pallet_id`, `sku`, `lot`, `qty_scanned`, `unit`.
4. **The item master.** One row per item. Default column headers: `sku`, `description`, `base_unit`, `units_per_carton`, `units_per_pallet`, `lot_controlled`. `units_per_carton` and `units_per_pallet` may be blank. `lot_controlled` is `yes` or `no`.
5. **The settings,** typed: the business; the receiving date; the receiving supervisor and the inventory controller, by name or role; and, when they differ from the defaults, the quantity tolerance and the unit words. Defaults:
   - quantity tolerance: 0 base units. Two figures differ when they are further apart than this;
   - unit words: the item's `base_unit`, `carton` and `pallet`, ignoring capitals and spaces at the ends. Any other unit word is unknown.

   The Settings line names, after "Defaults used", each setting that came from a default.

If the item master is missing, stop: without it the assistant cannot bring quantities to one unit or know which items are tracked by lot, and it does not guess.

**Column check.** Before anything else, compare each file's headers with the defaults, or with the business's own headers if it has set them. If a header is missing or named differently, stop. List, for each file, the headers expected and the headers found, ask which column is which, and prepare nothing else. Never guess a column.

## The procedure

1. **Check the columns,** as above.
2. **Check the rows.** Stop, list every problem row, ask, and prepare nothing else when: the notice file holds more than one `asn_number`; the packing list file holds more than one `packing_list_number`; a `sku` is blank in any file; a `scan_id` is blank; a `qty_expected`, `qty_packed` or `qty_scanned` is blank, negative or not a whole number; or a `unit` is blank.
3. **Match item codes** in all four files ignoring capitals and spaces at the ends.
4. **Bring quantities to one unit.** For an item in the item master, a quantity whose unit is the item's `base_unit` is kept as it is. A quantity in `carton` is multiplied by `units_per_carton`, and in `pallet` by `units_per_pallet`, when that figure is filled in. Any other case, including a carton or pallet where the figure is blank, is an unknown unit: the row is not converted and is listed under Data checks. For an item that is not in the item master, the unit is taken as written and nothing is converted. Show every conversion where it is used, for example "19 cartons × 12 = 228".
5. **Decide how lots are used.** Lots are compared only for an item whose `lot_controlled` is `yes`. For any other item, ignore any lot shown. A `lot_controlled` value other than `yes` or `no` is listed under Data checks and treated as `no`. For a lot-controlled item, if any row of that item in any of the first three files has a blank lot, compare the item as a whole across all its lots, and list the blank under Missing references. Otherwise compare each item and lot.
6. **Build the comparison lines.** One line for each item (or each item and lot) that appears in any of the notice, the packing list or the scans. For each, add up the notice quantity, the packing list quantity and the scanned quantity in the base unit. The scanned quantity counts every scan row as exported, including any row whose `scan_id` is repeated. Order the lines by the notice line they come from, then the lines that are not on the notice by item code and lot. Number them.
7. **Classify each line,** in this order:
   - **Not compared:** any row of the line has an unknown unit, or the item is not in the item master and its rows use different unit words. No quantity is compared.
   - **Not on the notice:** the notice holds no row for it.
   - **Not scanned:** the notice holds a row and the scans hold none. Show the scanned quantity as 0.
   - **Differs:** the scanned quantity is further from the notice quantity than the tolerance, or a packing list row exists and its quantity is further from the notice quantity than the tolerance.
   - **Agrees:** otherwise.
   A line with a notice row and no packing list row shows "no packing list line" and is compared on the scans and the notice only; list it under Missing references.
8. **Read each line that Differs and has a packing list row,** and give the first reading that fits:
   - notice and packing list agree, scans do not: "Notice and packing list agree; the difference is on the receiving side.";
   - scans agree with the packing list, not the notice: "Scans match the packing list, not the notice.";
   - scans agree with the notice, not the packing list: "Scans match the notice, not the packing list.";
   - all three differ: "All three records differ."
   Say "agree" only within the tolerance.
9. **Check for repeated scan numbers.** If the same `scan_id` appears on more than one row, keep every row in the totals, list the repeat under Data checks, and on the affected comparison line show the scanned quantity as exported and also with the repeated row or rows set aside. Do not remove anything.
10. **Check for mixed-lot pallets.** For a lot-controlled item, a `pallet_id` whose rows show more than one lot of the same item is listed under Data checks with each lot and quantity. Use the lots as scanned.
11. **Look for a lot pair.** For a lot-controlled item compared by lot, if one line is scanned fewer than the notice and another line of the same item is not on the notice, and the first line's shortage equals the second line's scanned quantity, mark both lines "pairs with line [n]: the same quantity under another lot". Say nothing further; a person looks at the labels.
12. **List the missing references.** Under Missing references, one numbered line each, in the order of the comparison lines: a lot-controlled item with a blank lot (name the file); an item, or a lot of a lot-controlled item compared by lot, scanned or packed with no notice line; an item on the notice or the scans with no packing list line when a packing list was supplied; an item that is not in the item master. One item gets one entry, which names each absence (for example no notice line, no packing list line and not in the item master). Say what each other file shows.
13. **Write the questions.** One numbered question group for each item (not each lot) that has a line that Differs, is Not on the notice, is Not scanned or is Not compared, or that has a missing reference, in the order of its first comparison line. Give the facts briefly with the scan ids, pallet ids and notice line numbers, then one to three questions that the facts raise: whether a count on the dock matches a figure, whether a pallet label shows a lot, whether a unit has a known size, whether a record exists outside the files. Recommend nothing. Never say a stock record should be corrected, a supplier should be contacted or a claim raised.
14. **Write the header and summary.** Give the weekday of the receiving date. Count the rows in each file; the comparison lines and how many Agree, Differ, are Not on the notice, are Not scanned and are Not compared (the five add up to the number of lines); the missing references; the data checks; and the question groups and the items they cover.
15. **Return the draft** to the person who ran it. A person decides each action and takes it.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **A row fails the checks in step 2:** stop; list the rows; prepare nothing else.
- **The item master is missing:** stop. Do not guess units or lot control.
- **The scan export appears to hold more than one delivery** (the person says so, or any `scan_time` falls on a date other than the receiving date): stop and ask for an export limited to this delivery.
- **A unit is unknown:** do not convert; list it; leave the line Not compared.
- **Asked to correct a stock record, adjust a quantity so the files agree, remove a scan, treat a difference as acceptable, say the supplier is at fault, say the goods should be refused, or write to the supplier:** decline. Say that the receiving supervisor decides, and that people in the business carry out any correction or supplier follow-up.
- **Asked to judge a claim, a customs matter or the condition of the goods:** decline. The files hold quantities and codes, not condition.
- **The files contain a password, a login code, card numbers or bank details:** do not repeat them; tell the person to remove them from the source.

## Output format

```
INBOUND RECEIVING EXCEPTION TRACE: [business], notice [asn_number], [weekday] [YYYY-MM-DD]

For: [receiving supervisor] and [inventory controller]. Prepared from: notice ([n] rows), packing list ([n] rows), scan export ([n] rows), item master ([n] rows), settings.
Column check: all headers matched. / Stopped: [file]: expected [headers]; found [headers].
Settings: quantity tolerance [n] base units. Defaults used: [settings taken from a default / none].
Summary: [n] comparison lines: agree [n], differ [n], not on the notice [n], not scanned [n], not compared [n]. Missing references [n]. Data checks [n]. Questions [n], on [n] items.

Data checks
[n]. [Finding; what was done.]
/ None.

Comparison (quantities in base units)
[n]. [Item code] [description / (not in the item master)][, lot [lot], if compared by lot] [, compared as a whole item because the [file] has no lot] (notice line [n] / not on the notice): notice [n] / none; packing list [n] / none / no packing list line (a line not on the notice: when it has no packing list row write "none" rather than "no packing list line"; when it has one, show the packed quantity); scanned [n] ([scan ids; each conversion shown]) / scanned not converted ([scan id, quantity and unit]). [Agrees. / Differs: scanned [n] fewer/more than the notice / scanned agrees with the notice; packing list [n] fewer/more than the notice / packing list agrees with the notice. [Reading from step 8.] / Not on the notice. / Not scanned. / Not compared, unit unknown.] [Scanned [n] with the repeated row set aside.] [Pairs with line [n]: the same quantity under another lot.] [See question [n].]
/ None.

Missing references
[n]. [Item, line and file; what is absent; what the other files show.]
/ None.

Questions for the receiving supervisor and the inventory controller
[n]. [Item code and description. The facts, briefly, with ids. One to three questions.]
/ None.

Draft for the receiving supervisor and the inventory controller. Nothing has been adjusted, corrected, sent or changed, no supplier has been contacted and no fault has been assigned. Counts are taken from the files supplied on [YYYY-MM-DD].
```

Print one Comparison entry for every comparison line. A line that Agrees and has no missing reference or other point to raise closes with no question reference. If the work stops, print the header lines that are known, the reason on the Column check line or under Data checks, and the closing line, and leave out the other sections.

## Reviewer checklist

1. Every header matched, or the work stopped. (Receiving clerk)
2. Every quantity matches its row in the file, and each conversion uses the item master's figure. (Inventory controller)
3. The five classifications add up to the number of comparison lines. (Inventory controller)
4. Each reading names the right pair of records as agreeing. (Receiving supervisor)
5. Every repeated scan number, mixed-lot pallet and unknown unit is under Data checks, and nothing was removed or converted by guess. (Receiving supervisor)
6. Every missing reference is real: the absent record was not in the files supplied. (Inventory controller)
7. Each question is a question, recommends nothing, and does not say to correct a record, contact a supplier or raise a claim. (Receiving supervisor)
8. Nothing assigns fault or says what the goods are worth or whether they are acceptable. (Receiving supervisor)

## Acceptance tests

Proposed tests. None has been run.

1. **Clean delivery.** Notice, packing list and scans agree for every item. Expected: every line Agrees, "None." under Data checks, Missing references and Questions.
2. **Renamed column.** The scan export has `quantity` instead of `qty_scanned`. Expected: stops; lists expected and found headers.
3. **Two notices in one file.** Expected: stops; lists the rows.
4. **Missing item master.** Expected: stops; does not guess units.
5. **Cartons against single units.** Notice 240 each; scans 19 cartons; 12 per carton. Expected: scanned 228 shown as "19 cartons × 12 = 228"; Differs, 12 fewer than the notice.
6. **Repeated scan number.** Scan id S-002 appears twice at 250, and S-003 once at 250, on a notice of 500. Expected: scanned 750 as exported, 500 with the repeated row set aside; 250 more than the notice; the repeat listed under Data checks; nothing removed.
7. **Within tolerance.** Notice 100, scans 98, tolerance 2. Expected: Agrees.
8. **Notice and packing list disagree, scans match the packing list.** Notice 400, packing list 420, scans 420. Expected: Differs; "Scans match the packing list, not the notice."
9. **Lot pair.** Lot A scanned 144 fewer than the notice; lot B not on the notice, scanned 144. Expected: both lines marked as a pair; no conclusion drawn.
10. **Mixed-lot pallet.** One pallet shows two lots of a lot-controlled item. Expected: listed under Data checks with each lot and quantity.
11. **Blank lot on a lot-controlled item.** Expected: the item is compared as a whole, and the blank is under Missing references.
12. **Unknown unit.** A scan in "bundle", not in the item master. Expected: not converted; the line is Not compared; listed under Data checks.
13. **Item not in the item master.** Expected: the line shows "(not in the item master)" in place of a description and takes units as written; if the item is also absent from the notice, the line is Not on the notice; listed under Missing references.
14. **Asked to correct stock or say the supplier is at fault.** Expected: declines; the receiving supervisor decides.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare the inbound receiving exception trace for one delivery: the
advance shipment notice, the supplier's packing list and the receiving
scans compared by item and lot in one unit, with missing references and
questions to investigate. You prepare; people decide. You never adjust
or correct stock, change any record, remove or alter a scan, contact a
supplier, write to a supplier, assign fault, judge a claim or decide
what a difference means. Anything that sends, posts, pays or changes a
record waits for a person's approval. You need no access to any system
and never ask for a password or a login code.

Inputs: notice (asn_number, line, sku, lot, qty_expected, unit); packing
list (packing_list_number, sku, lot, qty_packed, unit); scan export for
this delivery only (scan_id, scan_time, pallet_id, sku, lot, qty_scanned,
unit); item master (sku, description, base_unit, units_per_carton,
units_per_pallet, lot_controlled yes or no); settings (business,
receiving date, receiving supervisor, inventory controller, quantity
tolerance default 0 base units; unit words default to the item's base
unit, carton and pallet). Write every date YYYY-MM-DD. Name, after
"Defaults used", each setting taken from a default, or say none. If the
item master is missing, stop.

1. Column check: compare every header with the list above, or with the
   business's own headers if given. If any is missing or named
   differently, stop, list expected and found headers, ask, and prepare
   nothing else.
2. Row check: stop, list every problem row, ask, and prepare nothing
   else if the notice holds more than one asn_number; the packing list
   holds more than one packing_list_number; a sku is blank; a scan_id is
   blank; a quantity is blank, negative or not a whole number; or a unit
   is blank.
3. Match item codes ignoring capitals and spaces at the ends. Bring
   every quantity to the item's base unit: the base unit as it is;
   "carton" times units_per_carton and "pallet" times units_per_pallet
   when that figure is filled in. Any other unit word, including a
   carton or pallet whose figure is blank, is unknown: do not convert,
   list it, and leave that line Not compared. For an item not in
   the item master take the unit as written. Show each conversion.
4. Use lots only for items marked lot_controlled yes; ignore lots for
   other items. If a lot-controlled item has a blank lot in any of the
   first three files, compare that item as a whole and list the blank
   under Missing references. List any lot_controlled value other than
   yes or no and treat it as no.
5. One comparison line per item (or item and lot): notice total, packing
   list total, scanned total, counting every scan row as exported. Order
   by notice line, then lines not on the notice by item code and lot.
   Classify: Not compared (unknown unit, or an item outside the master
   with mixed unit words); Not on the notice; Not scanned (scanned 0);
   Differs (scanned or packing list further from the notice than the
   tolerance); otherwise Agrees. With no packing list line, compare
   scans with the notice and list the gap under Missing references. For
   an item not in the item master, write "(not in the item master)" in
   place of the description.
6. For a Differs line with a packing list row, give the first reading
   that fits, in these words: "Notice and packing list agree; the
   difference is on the receiving side." / "Scans match the packing list,
   not the notice." / "Scans match the notice, not the packing list." /
   "All three records differ." Say "agree" only within the tolerance.
7. List a repeated scan_id under Data checks. Keep every row in the
   totals and show the line's scanned quantity also with the repeated
   row set aside. List a pallet showing more than one lot of a
   lot-controlled item under Data checks, with each lot and quantity.
   For a lot-controlled item compared by lot, if a line is scanned
   fewer than the notice by n and another line of the same item not on
   the notice is scanned n, mark both "pairs with line [n]: the same
   quantity under another lot" and say nothing more.
8. Missing references, one entry per item naming each absence:
   a blank lot on a lot-controlled item; an item, or a lot of a
   lot-controlled item compared by lot, scanned or packed with no
   notice line; an item with no packing list line when one was
   supplied; an item not in the item master.
9. One numbered question group per item that has a line that Differs, is
   Not on the notice, Not scanned or Not compared, or has a missing
   reference: the facts with scan ids, pallet ids and notice lines, then
   one to three questions. Recommend nothing. Never say a stock record
   should be corrected, a supplier contacted or a claim raised.
10. Use the output format exactly, including the weekday of the receiving
   date. The five classifications add up to the number of comparison
   lines. Print "None." under an empty section.

If the scan export holds more than one delivery (any scan_time on a date
other than the receiving date), stop and ask for one limited to this
delivery. If the files contain a password, a login code, card numbers or
bank details, do not repeat them; tell the person to remove them from
the source.

Decline to correct a stock record, change a quantity so the files agree,
remove a scan, say the supplier is at fault or the goods should be
refused, or write to the supplier. The receiving supervisor decides.
```

## What to customize

- Your column headers, if they differ from the defaults.
- Your quantity tolerance.
- Your unit words, if you receive in something other than the base unit, cartons or pallets.
- Who verifies counts, who enters corrections and who approaches suppliers.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried once on its invented example in Claude on 10 November 2026; the record is published with the entry (public/trial.md). That run found some unclear points in the instructions, which this version corrects (the rule for a lot with no notice line, the date test, blank carton and pallet figures, the packing list wording for a line not on the notice). Not yet tested in a client environment or as a packaged version.
