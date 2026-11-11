# Carrier freight invoice check: one trial on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs are the invented example in `public/example.md` (Alder Mill Home Goods, Carrier A, invoice INV-A-9142). No client data was used. The model that ran the trial did not write the template. It read the template and only the invented inputs of the example, followed the instruction block and the output format as written, and read the example's output afterwards.

## Inputs used

The settings, the 17-line carrier invoice, the six-row shipment export, the 14-row rate confirmation and the two delivery and waiting-time records from "What the freight audit clerk supplies" in `public/example.md`. The tolerance is 0.00 and the rate confirmation states 120 free waiting minutes.

## What came out

```
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
- Credits: 0 lines, 0.00.
- Tie-out: 3,265.50 + 640.00 + 614.00 + 0.00 + 195.00 + 380.00 + 0.00 = 5,094.50.
- Amount in question: 1,241.50. Billed amount not in question: 3,853.00.

Lines in question
- Line 5, P202, linehaul, billed 640.00: Duplicate. Repeats line 3 (same shipment, charge type and amount). In question: 640.00.
- Line 6, P203, linehaul, billed 545.00: Rate difference. Confirmed 520.00; billed 25.00 over. In question: 25.00.
- Line 13, P205, liftgate, billed 45.00: Support missing. No record was supplied for this shipment and charge type. The billed amount equals the confirmed 45.00. In question: 45.00.
- Line 14, P205, detention, billed 150.00: Support missing (incomplete). The waiting record has no departure time. Also not on the rate confirmation. In question: 150.00.
- Line 16, P206, fuel, billed 69.00: Rate difference. Confirmed 67.50; billed 1.50 over. In question: 1.50.
- Line 17, P299, linehaul, billed 380.00: Shipment not found. P299 is not in the shipment export. In question: 380.00.

Matched lines: 1, 2, 3, 4, 7, 8, 9, 10, 11, 12, 15; 11 lines, 3,265.50.

Waiting-time facts
- Line 10, P204, detention billed 150.00: arrived 2026-10-20 08:30, left 2026-10-20 11:45, waited 195 minutes against 120 free minutes supplied: 75 minutes over.
- Line 14, P205, detention billed 150.00: arrived 2026-10-22 13:05, no departure time; minutes waited cannot be worked out.

Decisions for the accounts payable lead (5)
1. Matched lines: lines 1, 2, 3, 4, 7, 8, 9, 10, 11, 12 and 15, 11 lines, 3,265.50. Line 15 is on P206, which has no delivery date in the export. Whether to approve payment of these lines once the freight auditor has verified the match.
2. Duplicate: line 5 repeats line 3 (P202, linehaul), 640.00. Whether to dispute, hold or approve this line.
3. Rate difference: line 6 (P203, linehaul) billed 545.00 against 520.00 confirmed, 25.00 over; line 16 (P206, fuel) billed 69.00 against 67.50 confirmed, 1.50 over; 26.50 in question. Whether to dispute, hold or approve these lines.
4. Support missing: line 13 (P205, liftgate, 45.00) has no record supplied; line 14 (P205, detention, 150.00) has a waiting record with no departure time and is not on the rate confirmation; 195.00 in question. Whether to dispute, hold or approve these lines.
5. Shipment not found: line 17 (P299, linehaul), 380.00, is on a shipment that is not in the export. Whether to dispute, hold or approve this line.

Not supplied or not checked: earlier invoices were not supplied, so a charge already paid on an earlier invoice would not show as a repeat; the wording of the rate confirmation was not read, only its amounts and the free minutes in the settings; no delivery documents were supplied beyond the records listed.

Every figure traces to invoice INV-A-9142 and the shipment export, rate confirmation and records supplied on 2026-11-04. The check changes no records, contacts no carrier, pays nothing and sends nothing. A match is not authority to pay.
```

## What was observed

- Every part of the output format was produced, in order, and the status totals added to the invoice total (5,094.50) on the first pass.
- Nothing in the instructions made the run stop. All headers matched, no line number or shipment repeated, and every value could be read.
- The figures, counts, statuses, waiting-time facts and decisions are the same as the published example's. No figure appears in either output that cannot be worked out from the inputs.
- Differences from the published example are small and only in wording. Line 13 in this run says the billed amount equals the confirmed 45.00; the example says "Confirmed at 45.00". Line 14 here is marked "Support missing (incomplete)", as step 5 asks, and the example's decision 1 reads "match the rate confirmation" where this run left that phrase out. After the trial the example was aligned on line 14, which now also carries "Support missing (incomplete)"; the wording difference on line 13 remains.
- Where the instructions left room to guess:
  - Step 7 says to note the other tests a failed line fails. The example notes that line 14 is not on the rate confirmation but says nothing about line 17, which also has no confirmation row. This run followed the example's pattern for line 17 only because acceptance test 5 says "no rate comparison" for a shipment not found. The template should say whether such a line is noted as also not on the rate confirmation.
  - The line "Billed amount not in question" is the invoice total less the amount in question (3,853.00). That is not the same as the Matched amount (3,265.50), because a rate-difference line is only partly in question. The procedure says exactly this, but a reader may expect the two figures to agree, and the format does not explain the gap.
  - The format shows "Facts" for a line in question without saying whether the confirmed amount should be given on Support missing lines when the amounts agree. This run included it for line 13.
  - A matched detention line that is over the free minutes (line 10, 75 minutes over) is paid as Matched. The template says not to judge whether the charge is owed, and it follows that rule, but the matched-lines decision in this run does not mention it. The waiting-time section carries the fact.
- After the trial, four of these observations were answered in the template and the example, and the changes were not run again: the note on a Shipment not found line (step 7), the explanation of the gap between the two figures (step 9), the confirmed amount on a Support missing line (the format) and the matched detention line over the free minutes (step 12, now also in decision 1 of the example). The recorded output above is unchanged.
- Nothing in the run asked for a password, sent anything, or changed a record.
- This was one run by one model on one invented example. It shows that the instructions can be followed to a complete, tying-out page. It is not a test in a client environment, and the template's acceptance tests were not run.
