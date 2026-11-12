# Freight shortage record packet

Workflow template, version 0.1.0.

## Purpose

Prepare the packet a claims coordinator needs when a receiver reports missing or damaged freight: for each reported line, one quantity chain from dispatch through the warehouse scans and the bill of lading to the signed proof of delivery, with the scans, the remarks and the photos behind it. Records that do not exist are kept apart from figures that disagree, every other line on the shipment that does not add up is shown, and each unanswered question is written for the claims coordinator. Every finding traces to a row in a supplied file. The assistant prepares; it never assigns fault or responsibility, states a liability or a legal or claim position, approves a credit or compensation, sends or files anything, changes a record or contacts anyone.

## When to use it and when not to

Use it once a receiver has reported missing or damaged freight on a delivered shipment and the records for that one shipment have been pulled. Run it again when a missing record turns up or more photos arrive.

Do not use it:

- to apply a refund or credit policy to a complaint and set out an amount, which is complaint and refund request handling;
- to follow a production batch forward to every shipment it went on, which is batch distribution trace;
- to check the papers before goods leave, which is shipment documentation check;
- to decide who is responsible for a shortage or for damage, whether a claim is valid or what it is worth, or what to say to a carrier, an insurer or a customer. Those belong to the claims coordinator and the people the business names, and legal advice belongs to a lawyer;
- to look at the pictures and say what caused damage. The packet reads the photo log, not the images;
- to cover more than one shipment. One run covers one shipment.

## Roles

- **Runs it:** the claims coordinator, or a coordinator working for them.
- **Verifies the packet against the originals, and decides every follow-up with carriers, customers and the warehouse:** the claims coordinator. Always a person.
- **Owns each record:** the desk that keeps it (warehouse, transport operations, customer care). The assistant corrects and replaces none.
- **Answers the questions the packet raises:** the people named by the claims coordinator.

## Inputs

The assistant works only from the files the person supplies. It needs no connection to any system and never asks for a password or a login code. Dates are written YYYY-MM-DD and scan times YYYY-MM-DD HH:MM. The settings may give today's date in words; the assistant reads it as that date and writes it as YYYY-MM-DD. One run covers one shipment.

1. **The customer report.** One row for each reported line. Default column headers: `report_id`, `shipment_ref`, `item_code`, `issue`, `qty_affected`, `unit`, `reported_date`, `reported_by`, `note`. A blank `item_code` means the report covers the whole shipment. If this file is missing, stop.
2. **The dispatch lines,** from the packing list. Default column headers: `shipment_ref`, `line`, `item_code`, `description`, `qty_dispatched`, `unit`, `dispatch_date`. If this file is missing, stop: there is no quantity to compare against.
3. **The warehouse scans.** One row for each scan. Default column headers: `scan_id`, `shipment_ref`, `item_code`, `event`, `qty`, `scan_time`, `location`.
4. **The bill of lading.** One row for each item. Default column headers: `bol_number`, `shipment_ref`, `item_code`, `qty_stated`, `unit`, `remark`.
5. **The proof of delivery.** One row for each item. Default column headers: `pod_id`, `shipment_ref`, `item_code`, `qty_signed`, `unit`, `delivery_date`, `signed`, `exception_note`.
6. **The photo log.** One row for each photo. Default column headers: `photo_id`, `shipment_ref`, `item_code`, `taken_date`, `taken_by`, `caption`. A blank `item_code` means the photo is not tied to a line. The log is read; the images are not.
7. **The settings,** typed: the company; today's date; the claims coordinator, by name or role; and, when they differ from the defaults, the quantity tolerance and the words. Defaults:
   - quantity tolerance: 0 units. A stage differs from dispatch when it is further from it than this;
   - issue words: `short` and `damaged`. Any other `issue` word is reported as written and not compared;
   - scan words: `picked` and `loaded`. A scan with any other `event` word is listed as written and not added to a stage;
   - signed word: `yes`. A `signed` value of anything else, or blank, is "not shown as signed".

   The Settings line names, after "Defaults used", each setting that came from a default, or says "all" or "none".

Files 3 to 6 may be missing. A missing file is reported under Data checks, and every line shows "no record" for it.

**Column check.** Before anything else, compare each supplied file's headers with the defaults, or with the business's own headers if it has set them. If a header is missing or named differently, stop. List, for each file, the headers expected and the headers found, ask which column is which, and prepare nothing else. Never guess a column.

## The procedure

1. **Check the columns,** as above.
2. **Check the rows.** Stop, list every problem row, ask, and prepare nothing else when: the customer report or the dispatch lines hold more than one `shipment_ref`; a dispatch `line` is blank or appears twice; an `item_code` appears on two dispatch lines; a quantity (`qty_affected`, `qty_dispatched`, `qty`, `qty_stated`, `qty_signed`) is blank, negative or not a whole number; or a filled-in `reported_date`, `dispatch_date`, `delivery_date` or `taken_date` is not a date, or a `scan_time` is not a date and time. A blank `delivery_date` is allowed.
3. **Run the data checks.** These do not stop the work. List each under Data checks and say what was done:
   - a scan, bill of lading, proof of delivery or photo row for another `shipment_ref` is left out and listed;
   - a row whose `item_code` is not on the dispatch lines, or is blank on a scan, bill of lading or proof of delivery row, is left out of every chain and listed with its id and quantity; it also becomes a question (step 11);
   - a customer report row whose `item_code` is not on the dispatch lines is listed, gets no chain, and becomes a question;
   - a row with a `unit` that differs from the dispatch line's is listed; that line's quantities are shown but not compared, its report check is not made, and its first-stage line reads "not compared, unit differs";
   - two scans or two photos with the same id are both used and the duplicate id is listed;
   - a file not supplied is listed once, and the Missing records section carries one entry for it and none for its lines.
4. **Build the quantity chain** for each dispatch line, in the stages dispatched, picked, loaded, bill of lading, proof of delivery:
   - dispatched: `qty_dispatched`;
   - picked and loaded: the sum of `qty` over the line's scans whose `event` is the picked word, and the sum over those whose `event` is the loaded word, naming the scan ids;
   - bill of lading: the sum of `qty_stated` over the line's rows, naming the bill numbers;
   - proof of delivery: the sum of `qty_signed` over the line's rows, naming the delivery document ids and saying whether it is shown as signed;
   - a stage with no row for the line is "no record".
   The first stage that differs is the earliest stage after dispatch whose figure, where there is a record, is further from the dispatched quantity than the tolerance, written "[stage], [n] fewer than dispatched" or "[stage], [n] more than dispatched". If no recorded stage differs, write "None: every recorded stage equals dispatch." If no stage after dispatch has a record, write "None: no stage after dispatch has a record." A stage with no record is never a difference; it goes under Missing records.
5. **Delivery date and timing.** The delivery date of a line is the `delivery_date` on its proof of delivery rows. If the rows give two dates, show both and count from the earlier. With no date, write "delivery date not on file". Count the days from the delivery date to `reported_date`: "[n] days after delivery on [date]", "1 day after delivery on [date]", "on the day of delivery" or "[n] days before the delivery date on file". State the count and draw no conclusion from it.
6. **Write a block for each reported line,** one for each customer report row with an `item_code` on the dispatch lines, in the order of `report_id` (a line reported twice has two blocks with the same chain). Each block holds, in this order:
   - the header line with the report, quoting the `note` as written, or "No note.";
   - Quantities, First stage that differs from dispatch, and the Report check;
   - Scans: every scan of the line in time order, each with its id, event, quantity, time and location, including scans with other event words;
   - Remarks as written: the bill of lading `remark` and the proof of delivery `exception_note`, each quoted with its id, or "none" for a blank;
   - Photos: the photos tied to the line, each with its id, date, who took it and its caption quoted as written, or "None tied to this line."
   The **report check** is made only for the `short` word: dispatched less `qty_affected`, compared with the quantity signed. The quantity tolerance does not apply to it: the two figures are equal only if they are the same number. Write "equal" or "not equal, [n] apart". For `damaged` write "not made; a damaged count does not change a quantity." For another word write "not made; the issue word "[word]" is not short or damaged." With no proof of delivery record write "not made; no proof of delivery record."
7. **Whole-shipment reports.** A customer report row with a blank `item_code` is listed under Reported for the whole shipment with its id, issue, quantity if filled in, date, reporter and note as written, and gets a question. Otherwise write "None."
8. **Other lines on the shipment.** Every dispatch line with no report gets the same block without the report header or the Report check, headed "[item], dispatch line [n]. Not reported by the customer." A line with no missing record, no conflicting figure and no unit difference is not printed; it is counted in the summary as agreeing at every stage. A line skipped under step 3 for a unit difference is always printed, with "Not compared, unit differs.", and is never counted as agreeing. If every other line agrees, write "None."
9. **Photos not tied to a line.** List each photo with a blank `item_code`, or write "None."
10. **List what is missing,** under Missing records, one numbered entry each, in dispatch-line order, stages in order, then photos: a stage with no record ("no [picked scan / loaded scan / bill of lading row / proof of delivery row]", with the quantity at the stage before where there is one), and, for a `damaged` report, "no photo in the log for this line or for the shipment". Do not repeat a missing record under Conflicting figures. **List conflicting figures** under Conflicting figures, one numbered entry for each stage of each line that differs from dispatch by more than the tolerance (picked, loaded, bill of lading, proof of delivery, in that order), in dispatch-line order, naming the record ids and both figures and the difference; then a "not equal" report check as its own entry. Both sections say "None." when empty.
11. **Write the questions.** One numbered block for each reported line, then each other line printed in step 8, then each whole-shipment report, then one for the rows left out as not on the dispatch lines. Give the facts briefly with the record ids, then one to three questions the facts raise: whether a figure is right, whether a record exists outside the files, who wrote a remark and when, whether a photo belongs to the line, whether a document covers the line. For a reported line with no discrepancy, ask what the condition at delivery is recorded as, other than on the proof of delivery, and whether the photos tied to the line belong to it. Recommend nothing. Never say who is responsible, whether a claim should be raised, disputed, paid or dropped, or what to say to anyone.
12. **Write the header and summary.** Give the weekday of today's date: the settings' weekday if they state one, otherwise the one worked out from the date, which the claims coordinator confirms. Count reported lines (with the number of each issue word, and other); whole-shipment reports; the other lines printed (with a missing record, a conflicting figure or a unit difference) and the other lines agreeing at every stage; missing records; conflicting figures and the lines they sit on; photos, tied and not tied to a line; and questions. The number of other lines printed plus agreeing equals the dispatch lines not reported.
13. **Return the draft** to the person who ran it. A person decides each action and takes it.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **A row fails the checks in step 2:** stop; list the rows; prepare nothing else.
- **The customer report or the dispatch lines are missing:** stop. Do not infer a quantity from any other file.
- **A remark or a caption is unclear, or a photo is known only by its caption:** quote it as written. A caption is not evidence of what a photo shows, and a remark is not evidence of what happened, so do not describe either.
- **Asked who is at fault or responsible, whether the carrier, the warehouse or the receiver caused it, whether a claim is valid, what it is worth, whether the shortage is proved, or for a legal or insurance position:** decline. Say that the claims coordinator decides and, where it applies, a lawyer or the insurer.
- **Asked to send, file or post anything, to open or change a record, to write to the carrier or the customer, or to approve a credit:** decline; the packet is a draft for the claims coordinator.
- **Asked to change a figure so the records agree, or to treat a conflicting figure as settled:** decline.
- **The files contain a password, a login code, card numbers or bank details:** do not repeat them; tell the person to remove them from the source.

## Output format

```
FREIGHT SHORTAGE RECORD PACKET: [company], shipment [shipment_ref], [weekday] [YYYY-MM-DD]

For: [claims coordinator]. Prepared from: customer report ([n] rows), dispatch lines ([n] rows), warehouse scans ([n] rows), bill of lading ([n] rows), proof of delivery ([n] rows), photo log ([n] rows), settings.
Column check: all headers matched. / Stopped: [file]: expected [headers]; found [headers].
Settings: quantity tolerance [n] units; issue words "[word]" and "[word]"; scan words "[word]" and "[word]"; signed word "[word]". Defaults used: [all / none / the settings taken from a default, for example "quantity tolerance, scan words"].
Summary: Reported lines [n] (short [n], damaged [n], other [n]). Reports for the whole shipment [n]. Other lines: [n] with a missing record, conflicting figure or unit difference, [n] agreeing at every stage. Missing records [n]. Conflicting figures [n], on [n] lines. Photos [n]: [n] tied to a line, [n] not. Questions [n].

Data checks
[Finding; what was done.]
/ No problems found.

Reported lines
[item_code] [description], dispatch line [n]. Report [report_id]: [issue] [qty_affected] [unit], reported [YYYY-MM-DD] by [reported_by], [n days after delivery on YYYY-MM-DD / 1 day after delivery on YYYY-MM-DD / on the day of delivery / n days before the delivery date on file / delivery date not on file]. Note as written: "[note]". / No note.
Quantities: dispatched [n] (line [n], [YYYY-MM-DD]); picked [n] ([scan ids]) / picked no record; loaded [n] ([scan ids]) / loaded no record; bill of lading [n] ([bol numbers]) / bill of lading no record; proof of delivery signed [n] ([pod id], [shown as signed / not shown as signed]) / proof of delivery no record.
First stage that differs from dispatch: [stage], [n] fewer than dispatched / [n] more than dispatched. / None: every recorded stage equals dispatch. / None: no stage after dispatch has a record. / Not compared, unit differs.
Report check: dispatched [n] less reported [n] is [n]; proof of delivery signed [n]; equal. / not equal, [n] apart. / not made; [reason].
Scans: [scan id] [event] [qty] at [YYYY-MM-DD HH:MM], [location]; [next scan]. / No scans.
Remarks as written: bill of lading "[remark]" ([bol number]) / bill of lading none; proof of delivery "[exception note]" ([pod id]) / proof of delivery none.
Photos: [photo id] taken [YYYY-MM-DD] by [taken_by], "[caption]"; [next photo]. / None tied to this line.
[A further block for each further reported line.]
/ None.

Reported for the whole shipment
[Report id]: [issue] [qty and unit if filled in], reported [YYYY-MM-DD] by [reported_by]. Note as written: "[note]".
/ None.

Other lines on the shipment
[item_code] [description], dispatch line [n]. Not reported by the customer.
Quantities: [as above]
First stage that differs from dispatch: [as above]
Scans: [as above]
Remarks as written: [as above]
Photos: [as above]
/ None.

Photos not tied to a line
[Photo id] taken [YYYY-MM-DD] by [taken_by], "[caption]".
/ None.

Missing records
[n]. [item_code], line [n]: no [picked scan / loaded scan / bill of lading row / proof of delivery row] ([the quantity at the stage before, with its record id]). / no photo in the log for this line or for the shipment. / [file name] file not supplied.
/ None.

Conflicting figures
[n]. [item_code], line [n]: [stage] [verb] [n] ([record id]); dispatched [n] (line [n]); [n] fewer / [n] more.
[n]. [item_code], line [n]: report [report id] check not equal, [n] apart.
/ None.

Questions for the claims coordinator
[n]. [Item code, and the report id or "not reported". The facts, briefly, with record ids. One to three questions.]
/ None.

Draft for the claims coordinator. Nothing has been sent, filed, changed or decided, no fault or liability has been assigned, and no claim position has been taken. Counts are taken from the files supplied on [YYYY-MM-DD].
```

The verb in a conflicting figure is "signed" for the proof of delivery, "states" for the bill of lading, and "picked" or "loaded" for scans. If the work stops, print the header lines that are known, the reason on the Column check line or under Data checks, and the closing line, and leave out the other sections.

## Reviewer checklist

1. Every header matched, or the work stopped. (Claims coordinator)
2. Every quantity in a chain matches the file it names, and every id named exists. (Claims coordinator)
3. Every stage with no record is under Missing records and not under Conflicting figures, and no conflicting figure is listed as missing. (Claims coordinator)
4. Remarks and captions are quoted exactly as written. (Warehouse or transport lead)
5. The report check is arithmetically right, and the weekday in the header is the right one for the date. (Claims coordinator)
6. Every reported line has a block and a question block; every other line with a gap is printed. (Claims coordinator)
7. Nothing says or implies who is responsible, that a claim is valid or what it is worth, or what to tell anyone. (Claims coordinator)
8. Each question is a question, recommends nothing and does not say whether to raise, dispute, pay or drop a claim. (Claims coordinator)

## Acceptance tests

Proposed tests. None has been run.

1. **Clean shipment.** Every stage equals dispatch; the report is a damage report with photos. Expected: "None." under Missing records and Conflicting figures; a block and a question for the reported line.
2. **Renamed column.** The proof of delivery file has `qty` instead of `qty_signed`. Expected: stops; lists expected and found headers.
3. **No dispatch file.** Expected: stops; infers no quantity.
4. **Two shipment references in the dispatch lines.** Expected: stops; lists the rows.
5. **Missing loaded scan.** A line has picked scans and no loaded scan. Expected: "loaded no record"; one Missing records entry; no conflicting figure for the loaded stage.
6. **Signed quantity below dispatch.** 40 dispatched, 34 signed. Expected: "proof of delivery, 6 fewer than dispatched"; one conflicting figure.
7. **Short report matches.** Dispatched 40, reported short 6, signed 34. Expected: "equal".
8. **Short report does not match.** Dispatched 40, reported short 6, signed 40. Expected: "not equal, 6 apart"; a conflicting figure for the report check.
9. **Damaged with no photo.** Expected: Missing records entry "no photo in the log for this line or for the shipment".
10. **Tolerance.** A bill of lading 1 unit under dispatch with a tolerance of 1. Expected: no conflicting figure.
11. **Unit differs.** The proof of delivery unit is "carton" against "each". Expected: listed under Data checks; "Not compared, unit differs."
12. **Report for an item not dispatched.** Expected: listed under Data checks, no chain, a question.
13. **Whole-shipment report.** A report row with a blank `item_code`. Expected: listed under Reported for the whole shipment, with a question.
14. **Remark quoted.** A proof of delivery note with unusual wording. Expected: quoted as written, not paraphrased.
15. **Duplicate scan id.** Expected: both rows used; the duplicate listed.
16. **Asked who is at fault.** Expected: declines; the claims coordinator decides.
17. **Asked to write to the carrier or the customer.** Expected: declines; nothing is sent.
18. **Asked to make the figures agree.** Expected: declines.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare the freight shortage record packet for one shipment on which a
receiver has reported missing or damaged freight: for each reported line,
a chain of quantities from dispatch through the warehouse scans and the
bill of lading to the proof of delivery, with scans, remarks and photos,
the missing records kept apart from the conflicting figures, and the
unanswered questions. You prepare; people decide. You never assign fault
or responsibility, state a liability or a legal or claim position, say a
claim is valid or what it is worth, approve a credit, write to or contact
anyone, send, post or file anything, or change any record. Anything that
sends, posts, pays or changes a record waits for a person's approval. You
need no access to any system and never ask for a password or a login code.

Inputs: customer report (report_id, shipment_ref, item_code, issue,
qty_affected, unit, reported_date, reported_by, note; a blank item_code is
a whole-shipment report); dispatch lines (shipment_ref, line, item_code,
description, qty_dispatched, unit, dispatch_date); warehouse scans
(scan_id, shipment_ref, item_code, event, qty, scan_time, location); bill
of lading (bol_number, shipment_ref, item_code, qty_stated, unit, remark);
proof of delivery (pod_id, shipment_ref, item_code, qty_signed, unit,
delivery_date, signed, exception_note); photo log (photo_id, shipment_ref,
item_code, taken_date, taken_by, caption; read the log, not the images);
settings (company, today, claims coordinator, quantity tolerance default 0,
issue words default "short" and "damaged", scan words default "picked" and
"loaded", signed word default "yes"). Dates are YYYY-MM-DD, scan times
YYYY-MM-DD HH:MM; write them that way. Name after "Defaults used" each
setting taken from a default, or "all" or "none"; for some settings,
name them, for example "quantity tolerance, scan words". If the customer
report or the dispatch lines are missing, stop. When you stop, print the
header lines that are known, the reason on the Column check line or under
Data checks, and the closing line, and leave out the other sections.

1. Column check: compare every supplied file's headers with the list above,
   or the business's own. If any is missing or named differently, stop,
   list expected and found headers, ask, and prepare nothing else.
2. Row check: stop, list every problem row, and prepare nothing else if
   the report or dispatch lines hold more than one shipment_ref; a dispatch
   line is blank or repeated; an item_code is on two dispatch lines; a
   quantity is blank, negative or not whole; or a filled-in date or scan
   time is not valid.
3. Data checks (do not stop): list and leave out rows for another
   shipment; list and leave out rows for an item not on the dispatch lines,
   or with a blank item_code on a scan, bill of lading or proof of delivery
   row (and ask about them); list a report for an item not dispatched (no
   chain, a question); list a unit that differs from the dispatch unit and
   do not compare that line; use both rows of a duplicate scan or photo id
   and list it; list a file not supplied once, with one Missing records
   entry for the file and none for its lines. A line skipped for a unit
   difference reads "Not compared, unit differs." and is printed under
   Other lines if it has no report.
4. For each dispatch line build the chain: dispatched; picked and loaded
   (sum of qty by the scan words, naming scan ids); bill of lading (sum of
   qty_stated, naming bill numbers); proof of delivery (sum of qty_signed,
   naming the document id and whether it is shown as signed). A stage with
   no row is "no record" and is never a difference. The first stage that
   differs is the earliest stage with a record further from the dispatched
   quantity than the tolerance: "[stage], [n] fewer/more than dispatched",
   or "None: every recorded stage equals dispatch.", or "None: no stage
   after dispatch has a record."
5. Delivery date is the proof of delivery delivery_date for the line (two
   dates: show both, count from the earlier; none: "delivery date not on
   file"). State the days from delivery to the report date and draw no
   conclusion.
6. One block per customer report row with a dispatch item, in report_id
   order: header and note as written; Quantities; First stage; Report check
   (short only: dispatched less reported compared with signed, the
   tolerance not applied, "equal" or
   "not equal, [n] apart"; damaged: "not made; a damaged count does not
   change a quantity."; another word: "not made; the issue word \"[word]\"
   is not short or damaged."; no proof of delivery record: "not made; no
   proof of delivery record."; unit differs: not made);
   Scans in time order including other event words; Remarks as written for
   the bill of lading and proof of delivery, quoted exactly; Photos tied to
   the line with captions quoted exactly.
7. List whole-shipment reports. Print each dispatch line with no report
   that has a missing record, a conflicting figure or a unit difference,
   without the report lines; count the rest as agreeing.
   List photos not tied to a line.
8. Missing records, numbered, in dispatch-line order and stage order: each
   stage with no record, and for a damaged report, no photo in the log for
   the line or the shipment. Conflicting figures, numbered: each stage of
   each line that differs from dispatch by more than the tolerance, with
   record ids, both figures and the difference; then any "not equal" report
   check. The verb is "signed" for the proof of delivery, "states" for the
   bill of lading, "picked" or "loaded" for scans. Never list one thing
   under both.
9. Questions: one block for each reported line, each other line printed,
   each whole-shipment report, and the rows left out as not dispatched. The
   facts with record ids, then one to three questions the facts raise
   (is a figure right, does a record exist elsewhere, who wrote a remark and
   when, does a photo belong to the line; for a reported line with no
   discrepancy, how the condition at delivery is recorded and whether the
   photos belong to it). Recommend nothing; never say who
   is responsible or whether to raise, dispute, pay or drop a claim.
10. Summary counts as in the output format; "None." for an empty section.
    Use the output format exactly, including the weekday of today's date
    (the settings' weekday if stated, otherwise worked out from the date;
    the claims coordinator confirms it).

Quote remarks and captions as written. Never describe what a photo shows
or what a remark proves. Decline to say who is at fault, whether a claim is
valid or what it is worth, to give a legal or insurance view, to write to
the carrier, the customer or anyone, to change a figure so the records
agree, or to treat a conflicting figure as settled. The claims coordinator
decides. If the files contain a password, a login code, card numbers or
bank details, do not repeat them; tell the person to remove them.
```

## What to customize

- Your column headers, if they differ from the defaults.
- The words your records use for picked and loaded scans, for short and damaged, and for signed.
- Your quantity tolerance.
- Who verifies the packet, and who decides follow-up with carriers, customers and the warehouse.
- Who receives the returned draft.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried once on its invented example in Claude on 10 November 2026; the record is published with it. Small wording edits made after review (unit-differs lines, rules moved into the instruction block, settings and question wording, the example, and then blank item codes on the record files, the report check without tolerance, the weekday confirmation and the invented company name) were not run again. Not yet tested in a client environment.
