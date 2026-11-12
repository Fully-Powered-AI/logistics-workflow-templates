# Carrier freight invoice check

Workflow template, version 0.1.0.

## Purpose

Check one carrier invoice, line by line, against the shipment export and the rate confirmation, and show where each line stands: matched, a duplicate, a rate difference, not on the rate confirmation, missing its support record, or on a shipment that cannot be found. Each line in question is tied to its shipment, and the totals tie back to the invoice. The freight auditor verifies the match and accounts payable approves payment or a dispute. The assistant prepares; it never pays, disputes, contacts a carrier, changes a record, or decides what a term in the rate confirmation means.

## When to use it and when not to

Use it when a carrier invoice arrives that carries extra charges or does not match the expected cost, before it goes to payment.

Do not use it to interpret the wording of a rate confirmation, to decide whether a charge is owed, to compare carriers over a period (see carrier performance review), to check supplier bills for goods and services (see supplier bill review and payment run preparation), or to write to a carrier. Do not use it when the invoice or the shipment export is missing, or when a header does not match.

## Roles

- **Runs it:** the freight audit clerk, the accounts payable clerk or an operations analyst.
- **Verifies the match:** the freight auditor, who checks each line in question against the records.
- **Approves payment or a dispute:** accounts payable, as the company sets it.
- **Raises a dispute with the carrier:** the person who owns that relationship, outside this workflow template.

## Inputs

1. **Settings.** Company, carrier, invoice number, invoice date, today's date, currency, the role that runs the check, the role that verifies, the role that approves, the tolerance (default 0.00: any difference is listed), and the free waiting minutes (no default: blank unless the rate confirmation states them). If the invoice number or today's date is missing, stop and ask. If a role is missing, write "not stated" for it and say so under Not supplied or not checked. If free minutes are blank, waiting time is shown without a comparison and the page says so.
2. **Carrier invoice,** one row per charge line, with these headers exactly: `invoice, line, shipment_id, carrier, charge_type, amount`. `charge_type` is linehaul, fuel, detention, liftgate, lumper or other; linehaul and fuel are base charges and the rest are accessorial charges. `amount` is a number in the one currency; a negative amount is a credit. The run covers one invoice and one carrier.
3. **Shipment export,** one row per shipment billed, with these headers exactly: `shipment_id, carrier, ship_date, lane, delivered_date`. Dates are YYYY-MM-DD. A blank `delivered_date` means not delivered or not recorded.
4. **Rate confirmation,** one row per agreed charge, with these headers exactly: `shipment_id, charge_type, confirmed_amount`.
5. **Delivery and waiting-time records,** one row per record, with these headers exactly: `shipment_id, charge_type, record_type, arrival_time, departure_time, note`. Times are YYYY-MM-DD HH:MM. If no records are supplied, say so and treat every accessorial charge as lacking support.

If a header is missing, renamed or in doubt, stop and ask which column is which; never guess. Shipment, carrier and charge-type names are taken exactly as written.

## The procedure

1. **Check the data before any arithmetic.** Stop and list the rows if: a header does not match; the invoice rows carry more than one invoice number or carrier; a `line` number repeats; a `charge_type` is not one of the six; an `amount` or `confirmed_amount` is not a number; a date or time cannot be read; a `shipment_id` repeats in the shipment export; the same shipment and charge type appears twice in the rate confirmation; or the records file holds two rows for the same shipment and charge type (for example two waiting records for one detention line). Ask before continuing; do not choose between the rows.
2. **Credits.** A line with a negative amount has the status Credit. List it and net it in the invoice total. Never match it to a charge and never treat it as a duplicate.
3. **Find the shipment.** A line whose shipment is not in the export, or is listed there under a different carrier, has the status Shipment not found. State which.
4. **Find duplicates.** Among the other lines, a line is a Duplicate when an earlier line on the invoice has the same shipment, charge type and amount. The earliest line is kept and compared normally; each later one is the duplicate and names the line it repeats. Where the same shipment and charge type appear more than once at different amounts, compare each line normally and list the pair under Data checks.
5. **Check support for accessorial charges.** An accessorial line is supported when the records hold a row with the same shipment and charge type. For detention, the row must also have an arrival and a departure time, with the departure after the arrival; otherwise the support is incomplete. A line without support has the status Support missing, and the line says whether there was no record or an incomplete one.
6. **Compare with the rate confirmation.** For a line not yet given a status, find the confirmation row with the same shipment and charge type. With no row, the status is Not on the rate confirmation. With a row, the line matches when the billed amount differs from the confirmed amount by no more than the tolerance; otherwise its status is Rate difference, with the billed amount, the confirmed amount, and the gap as "over" or "under".
7. **Give each line one status.** Judge in this order and stop at the first that applies: Credit, Shipment not found, Duplicate, Support missing, Rate difference, Not on the rate confirmation, Matched. Where a line fails more than one test, its status is the first, and the line notes the others, such as "also not on the rate confirmation" or the rate gap. A Shipment not found line is not compared with the rate confirmation, so it notes no rate test even where the confirmation has no row for it.
8. **Waiting-time facts.** For every detention line, print the arrival and departure times from the record and the minutes waited, the departure less the arrival. If free minutes were supplied, print the minutes waited against them, as minutes over or within. Do not judge whether the charge is owed or what the free time means. With no complete record, say that minutes waited cannot be worked out.
9. **Amount in question.** For a Duplicate, Support missing, Not on the rate confirmation or Shipment not found line, the full billed amount. For a Rate difference line, the size of the gap, whichever direction. Add them. The billed amount not in question is the invoice total less the amount in question; it is larger than the Matched amount by the confirmed part of any Rate difference lines, because only the gap on those lines is in question.
10. **Totals and tie-out.** Print the invoice total and the line count, then each status with its line count and its billed amount. For Rate difference also print the confirmed amount and the gap. The status totals must add to the invoice total; if they do not, stop and report the figures. Round every printed amount to two decimal places, working from the exact figures.
11. **Gaps in the other direction.** List confirmed charges that are not on the invoice (shipment, charge type, amount) and shipments in the export with no invoice line. List shipments billed with no delivery date.
12. **Decisions for the approver.** Write one numbered decision for the Matched lines, and one for each other status that has lines. Give the line numbers, shipments, amounts and facts, then the question. For matched lines: whether to approve payment once the freight auditor has verified the match; mention any matched line on a shipment with no delivery date, and any matched detention line whose minutes waited are over the free minutes supplied (the waiting-time facts carry the figures; do not judge the charge). For every other status: whether to dispute, hold or approve those lines. Recommend nothing.
13. **Say what was not checked,** and trace the figures. Return the check to the person who runs it only.

## Exceptions and stop conditions

- **A header does not match,** a line number or shipment repeats where it should not, a value cannot be read, or the invoice mixes invoices or carriers: stop; list the rows; ask.
- **The status totals do not add to the invoice total:** stop; report the figures.
- **No rate confirmation supplied:** produce the checks that need only the invoice and the shipment export (credits, shipment not found, duplicates), mark every other line "not checked, no rate confirmation" and say so; never estimate a rate. Accessorial support (step 5) needs no rate confirmation, but it is not checked in this case either, so that the page gives one set of partial checks; say so. Show those lines as one further total, "Not checked, no rate confirmation", with its line count and amount, added to the tie-out. The amount in question then covers only the Duplicate and Shipment not found lines, and the billed amount not in question is not worked out; say so.
- **Asked whether a charge is owed, what a free-time or cap clause means, or to read the wording of the rate confirmation:** decline; show the amounts and records; the freight auditor and accounts payable decide.
- **Asked to pay, approve, dispute, email a carrier, update a record or change an amount, a time or a status so the totals look cleaner:** decline; name the role that does it.

## Output format

```
CARRIER FREIGHT INVOICE CHECK: [carrier], invoice [invoice number]

For: [approver role]; checked by [verifier role], run by [role that runs the check]. Invoice dated [date]; records as supplied on [today]. Currency [currency].

Data checks: [n] invoice lines; [n] shipments billed; [n] lines on a shipment not in the export or listed under another carrier ([line numbers or none]). Credit lines: [line, shipment, charge type, amount or None]. Shipment and charge type billed more than once at different amounts: [list or None]. Shipments billed with no delivery date: [ids and lines or None]. Confirmed charges not invoiced: [shipment, charge type, amount or None]. Shipments in the export not on the invoice: [ids or None].

Totals
- Invoice total: [amount] on [n] lines.
- Matched: [n] lines, [amount].
- Duplicate: [n] lines, [amount].
- Rate difference: [n] lines, billed [amount]; confirmed [amount]; difference [amount].
- Not on the rate confirmation: [n] lines, [amount].
- Support missing: [n] lines, [amount].
- Shipment not found: [n] lines, [amount].
- Credits: [n] lines, [amount].
- Tie-out: [matched] + [duplicate] + [rate difference billed] + [not on the rate confirmation] + [support missing] + [shipment not found] + [credits] = [invoice total].
- Amount in question: [amount]. Billed amount not in question: [amount].

Lines in question
- Line [n], [shipment], [charge type], billed [amount]: [status]. [Facts: the line repeated; the confirmed amount and the gap over or under; the support record found or missing, and for a Support missing line the confirmed amount when the billed amount agrees with it; other tests failed]. In question: [amount].
[One line for each line in question, in line order. Or: None.]

Matched lines: [line numbers; n lines, amount] or None.

Waiting-time facts
- Line [n], [shipment], detention billed [amount]: arrived [time], left [time], waited [n] minutes against [n] free minutes supplied: [n] minutes over / within. [Or: no departure time; minutes waited cannot be worked out. Or: free minutes not supplied.]
[One line for each detention line. Or: None.]

Decisions for [approver role] ([n])
[Number]. [Status]: [line numbers, shipments, amounts and facts]. Whether to [approve payment of these lines once the freight auditor has verified the match / dispute, hold or approve these lines].
[One numbered line for each decision. Or, with no decision: Decisions for [approver role]: None.]

Not supplied or not checked: [what was not supplied; settings taken from defaults; the standing lines below].

Every figure traces to invoice [invoice number] and the shipment export, rate confirmation and records supplied on [today]. The check changes no records, contacts no carrier, pays nothing and sends nothing. A match is not authority to pay.
```

Standing lines for Not supplied or not checked, used when they apply: "earlier invoices were not supplied, so a charge already paid on an earlier invoice would not show as a repeat"; "the wording of the rate confirmation was not read, only its amounts and the free minutes in the settings"; "no delivery documents were supplied beyond the records listed". If a section has nothing to report, write "None." in its place.

## Reviewer checklist

1. Every amount and count matches the invoice, the rate confirmation and the records when recomputed. (Freight auditor)
2. The status totals add to the invoice total, and the amount in question is worked as the procedure says. (Freight audit clerk)
3. Each line has exactly one status, assigned in the stated order. (Freight auditor)
4. Each duplicate names the line it repeats, and the earliest line stays in the comparison. (Freight audit clerk)
5. Every accessorial charge shows whether a record was supplied, and every detention line shows the minutes from the record's own times. (Freight auditor)
6. No decision recommends, scores or rules on what a clause means, and every decision names the lines behind it. (Accounts payable lead)
7. The page states what was not supplied or not checked, and nothing in it pays, disputes or sends. (Accounts payable lead)

## Acceptance tests

Proposed tests. None has been run.

1. **Normal invoice.** Lines of each status among them. Expected: every section complete; totals tie; the amount in question recomputes from the lines.
2. **Renamed column.** `confirmed_amount` appears as `rate`. Expected: stops, names the header, asks which column it is; no figures.
3. **Repeated line.** The same shipment, charge type and amount on lines 3 and 5. Expected: line 5 is the duplicate and names line 3; line 3 is compared normally.
4. **Same charge, different amounts.** Two linehaul lines on one shipment at different amounts. Expected: neither is a duplicate; both are compared with the confirmation; the pair is listed under Data checks.
5. **Shipment not in the export.** Expected: Shipment not found, full amount in question, no rate comparison and no note of a rate test.
6. **Shipment under another carrier.** Expected: Shipment not found, and the line says it is listed under another carrier.
7. **Detention with no departure time.** Expected: Support missing, noted as incomplete; waiting-time facts say minutes cannot be worked out.
8. **Detention with free minutes blank.** Expected: minutes waited shown with the note that free minutes were not supplied; no comparison.
9. **Accessorial with a record but no confirmation row.** Expected: Not on the rate confirmation.
10. **Credit line.** A negative amount. Expected: status Credit, netted in the total, not matched or counted as a duplicate.
11. **Billed under the confirmed rate.** Expected: Rate difference, "under", the size of the gap counted in the amount in question.
12. **Shipment with no delivery date.** Expected: listed under Data checks; named in the decision for matched lines when a matched line is on it.
13. **Asked whether the detention is owed.** Expected: declines; shows the times and minutes; names the roles that decide.
14. **Asked to dispute with the carrier.** Expected: declines; names the role that does it.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You check one carrier freight invoice for a freight auditor, against a
shipment export, a rate confirmation and delivery or waiting-time
records. You prepare; people decide. You never pay, approve, dispute,
contact a carrier, update a record or change an amount, a time or a
status. A person approves any such step. You never decide whether a
charge is owed or what a clause in the rate confirmation means. You
never ask for a password, a login code or any access to a system.

The user will supply: settings (company, carrier, invoice number,
invoice date, today's date, currency, the roles that run, verify and
approve, tolerance with default 0.00, free waiting minutes with no
default); the invoice with headers invoice, line, shipment_id, carrier,
charge_type, amount; the shipment export with headers shipment_id,
carrier, ship_date, lane, delivered_date; the rate confirmation with
headers shipment_id, charge_type, confirmed_amount; and the records with
headers shipment_id, charge_type, record_type, arrival_time,
departure_time, note. If the invoice number or today's date is missing,
or a header does not match, stop and ask. Never guess a column. If a
role is missing, write "not stated" and say so. If no records are
supplied, say so and treat every accessorial charge as lacking support.

1. Check first. Stop and list the rows if the invoice mixes invoices or
   carriers, a line number repeats, a charge_type is not linehaul, fuel,
   detention, liftgate, lumper or other, a number, date or time cannot
   be read, a shipment repeats in the export, or the rate confirmation
   repeats a shipment and charge type, or the records hold two rows for
   the same shipment and charge type. Ask; do not choose between rows.
2. A negative amount is a Credit: list it, net it, never match it.
3. A line whose shipment is not in the export, or is listed under
   another carrier, is Shipment not found.
4. A later line with the same shipment, charge type and amount as an
   earlier line is a Duplicate and names the line it repeats; the
   earliest stays in the comparison.
5. An accessorial line (any type except linehaul and fuel) is supported
   only by a record with the same shipment and charge type. Detention
   also needs an arrival and a departure time, the departure after the
   arrival. Otherwise the status is Support missing, and the line says
   whether the record was missing or incomplete.
6. Compare the rest with the confirmation row for the same shipment and
   charge type: no row is Not on the rate confirmation; a gap above the
   tolerance is Rate difference, shown as over or under; otherwise
   Matched.
7. Give each line one status, judging in this order: Credit, Shipment
   not found, Duplicate, Support missing, Rate difference, Not on the
   rate confirmation, Matched. Note the other tests a line fails. A
   Shipment not found line is not compared with the rate confirmation.
8. For each detention line print the times and the minutes waited, and
   set them against free minutes only if supplied. Do not judge whether
   the charge is owed.
9. Amount in question: the full amount for Duplicate, Support missing,
   Not on the rate confirmation and Shipment not found lines; the size
   of the gap for Rate difference lines. Status totals must add to the
   invoice total; if not, stop and report the figures. Billed amount not
   in question is the invoice total less the amount in question; it
   exceeds Matched by the confirmed part of Rate difference lines. Round
   every printed amount to two decimal places from the exact figures.
10. List confirmed charges not invoiced, export shipments not billed and
    shipments billed with no delivery date.
11. Write one decision for the matched lines and one for each other
    status with lines, with the facts and the question. For the matched
    lines, mention any on a shipment with no delivery date and any
    detention line over the free minutes supplied. Recommend nothing.
12. With no rate confirmation, check only credits, shipment not found
    and duplicates, show every other line as Not checked, no rate
    confirmation with its own total in the tie-out, and estimate no
    rate. Accessorial support is not checked then either, and the amount
    in question covers only Duplicate and Shipment not found lines; do
    not work out the billed amount not in question; say so. Use the
    output format exactly. Print None. for an empty section.
    State what was not supplied or not checked. End with the trace line.

If asked to rule on a clause, say a charge is owed, pay, dispute, email
a carrier or adjust a figure, decline and name the role that does it.
```

## What to customize

- Your file layouts, so the header check passes without a question.
- Your charge types, if you use names beyond the six.
- The tolerance, and the free waiting minutes if your rate confirmations state them.
- Which records count as support for each accessorial charge.
- Who verifies, who approves, and how a dispute reaches the carrier.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried once on its invented example in Claude on 10 November 2026; the record is published with it. Edits made after the trial, including a stop rule for duplicate records, a mention of matched detention over the free minutes and the no-rate-confirmation wording in the instruction block, were not run again. Not yet tested in a client environment.
