# Freight shortage record packet: trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Sonnet 5.5 (claude-sonnet-5-5). It did not write the template.
- **Date:** 2026-11-10

The inputs were the invented example in `public/example.md` (shipment SH-2210: settings, customer report, dispatch lines, warehouse scans, bill of lading, proof of delivery, photo log). No client data was used. The template's fenced instruction block and output format were followed as written, and the packet was produced before the example's own output was read.

## What came out

```
FREIGHT SHORTAGE RECORD PACKET: the Distributor, shipment SH-2210, Tuesday 2026-11-10

For: the claims coordinator. Prepared from: customer report (2 rows), dispatch lines (3 rows), warehouse scans (6 rows), bill of lading (3 rows), proof of delivery (3 rows), photo log (3 rows), settings.
Column check: all headers matched.
Settings: quantity tolerance 0 units; issue words "short" and "damaged"; scan words "picked" and "loaded"; signed word "yes". Defaults used: all.
Summary: Reported lines 2 (short 1, damaged 1, other 0). Reports for the whole shipment 0. Other lines: 1 with a missing record or conflicting figure, 0 agreeing at every stage. Missing records 1. Conflicting figures 3, on 2 lines. Photos 3: 2 tied to a line, 1 not. Questions 3.

Data checks
No problems found.

Reported lines
CHR-110 Folding chair, dispatch line 1. Report R-1: short 6 each, reported 2026-11-06 by Customer A receiving lead, 1 day after delivery on 2026-11-05. Note as written: "Six chairs missing from pallet".
Quantities: dispatched 40 (line 1, 2026-11-03); picked 40 (S-01, S-02); loaded 40 (S-03); bill of lading 40 (BOL-9051); proof of delivery signed 34 (POD-77, shown as signed).
First stage that differs from dispatch: proof of delivery, 6 fewer than dispatched.
Report check: dispatched 40 less reported 6 is 34; proof of delivery signed 34; equal.
Scans: S-01 picked 25 at 2026-11-03 07:40, Aisle 4; S-02 picked 15 at 2026-11-03 07:52, Aisle 4; S-03 loaded 40 at 2026-11-03 09:10, Dock 2.
Remarks as written: bill of lading "Shipper load and count" (BOL-9051); proof of delivery "6 chairs not on pallet" (POD-77).
Photos: None tied to this line.

TBL-220 Trestle table, dispatch line 2. Report R-2: damaged 2 each, reported 2026-11-06 by Customer A receiving lead, 1 day after delivery on 2026-11-05. Note as written: "Two table tops damaged".
Quantities: dispatched 12 (line 2, 2026-11-03); picked 12 (S-04); loaded 12 (S-05); bill of lading 12 (BOL-9051); proof of delivery signed 12 (POD-77, shown as signed).
First stage that differs from dispatch: None: every recorded stage equals dispatch.
Report check: not made; a damaged count does not change a quantity.
Scans: S-04 picked 12 at 2026-11-03 08:05, Aisle 9; S-05 loaded 12 at 2026-11-03 09:12, Dock 2.
Remarks as written: bill of lading "Shipper load and count" (BOL-9051); proof of delivery none.
Photos: PH-1 taken 2026-11-06 by Customer A receiving, "Table top corner chipped"; PH-2 taken 2026-11-06 by Customer A receiving, "Second table top cracked edge".

Reported for the whole shipment
None.

Other lines on the shipment
CRT-330 Storage crate, dispatch line 3. Not reported by the customer.
Quantities: dispatched 60 (line 3, 2026-11-03); picked 60 (S-06); loaded no record; bill of lading 54 (BOL-9051); proof of delivery signed 54 (POD-77, shown as signed).
First stage that differs from dispatch: bill of lading, 6 fewer than dispatched.
Scans: S-06 picked 60 at 2026-11-03 08:20, Aisle 2.
Remarks as written: bill of lading "Shipper load and count" (BOL-9051); proof of delivery none.
Photos: None tied to this line.

Photos not tied to a line
PH-3 taken 2026-11-06 by Customer A receiving, "Pallet wrapping torn on one side".

Missing records
1. CRT-330, line 3: no loaded scan (picked 60, S-06).

Conflicting figures
1. CHR-110, line 1: proof of delivery signed 34 (POD-77); dispatched 40 (line 1); 6 fewer.
2. CRT-330, line 3: bill of lading states 54 (BOL-9051); dispatched 60 (line 3); 6 fewer.
3. CRT-330, line 3: proof of delivery signed 54 (POD-77); dispatched 60 (line 3); 6 fewer.

Questions for the claims coordinator
1. CHR-110, report R-1 (short 6). Picked (S-01, S-02), loaded (S-03) and BOL-9051 all show 40; POD-77 shows 34 signed with the remark "6 chairs not on pallet". Who wrote that remark, and when? Is there a count at delivery outside the files supplied?
2. TBL-220, report R-2 (damaged 2). Every stage shows 12 and POD-77 has no remark for this line. PH-1 and PH-2 are tied to the line and dated 2026-11-06. Is the condition of the freight at delivery recorded anywhere other than POD-77? Does PH-3 belong to this line?
3. CRT-330, not reported. Picked 60 (S-06), no loaded scan; BOL-9051 states 54 and POD-77 shows 54 signed. Is a loaded scan recorded elsewhere? Is 54 on BOL-9051 a count or an entry difference? Is the 6-unit difference known to the customer?

Draft for the claims coordinator. Nothing has been sent, filed, changed or decided, no fault or liability has been assigned, and no claim position has been taken. Counts are taken from the files supplied on 2026-11-10.
```

## What was observed

- **Every required part was produced,** in the order the format gives. Nothing in the run called for a stop: all headers matched, no row failed the row checks, and there were no data-check findings.
- **No instruction forced a guess that changed a figure.** The arithmetic was unambiguous: the short report on chairs (40 less 6 is 34) equals the 34 signed; the crate line has no loaded scan (a missing record) and is 6 under at the bill of lading and the proof of delivery (two conflicting figures).
- **Differences from the published example:** the figures, counts, sections and order are the same. Only the wording of the three questions differs (the example asks, for instance, whether the original images and their capture times are available, and whether the 6-unit difference has been mentioned by the customer; this run asked fewer and slightly different questions), and the missing-record entry reads "picked 60, S-06" where the example reads "60 picked, S-06". The template's format shows the quantity "with its record id", so both are within it.
- **Facts not in the inputs:** none in this run's output. In the example's output, the question "Has the customer mentioned the 6-unit difference?" assumes a customer contact the inputs do not mention, and "was it written at the delivery?" asks about something the inputs do not say; both are questions, not statements of fact.
- **Where the template was ambiguous:**
  - The weekday is required but the settings give only a date; it had to be worked out (Tuesday), which a model can get wrong. The template was changed afterwards: the weekday is taken from the settings if they state it, and the claims coordinator confirms it on the reviewer checklist.
  - The Summary line reads "Other lines: [n] with a missing record or conflicting figure" while step 8 prints lines with a gap; the two agree here, but a line with only a unit difference is not clearly in either group. The format's Summary line was reworded afterwards to "missing record, conflicting figure or unit difference", and the example's Summary line carries that wording; the Summary line recorded above is the one this run produced.
  - A conflicting figure at both the bill of lading and the proof of delivery on one line is listed as two entries; the template says one entry per stage, so this follows it, but the "first stage that differs" line shows only the earlier one.
  - The format gives no clear place for the "Defaults used" wording when only some settings are defaults beyond "all / none / list", though this run did not need it.
  - Step 11 says one question block for each reported line, including a line with no discrepancy (TBL-220); the content of such a block is left to the assistant.
- **Edits made after this run:** the example's three questions were reworded afterwards (for instance "Who wrote that remark, and when?", "Is the 6-unit difference known to the customer?" and "Are the original images available?"), so the question wording this run is compared with is the earlier wording. The invented company name was also changed from "the Depot" to "the Distributor" in the example and, as a plain name substitution, in the header line above. Neither change was run again.
- **Limits of this trial:** one run, on one small invented shipment, by one model. It does not test the stop conditions, the unit-differs path, tolerance, whole-shipment reports or the declining rules. It says nothing about how the template performs on a real client's exports.
