# Missed dock window recovery brief

Capability template, version 0.1.0.

## Purpose

Prepare one brief for one inbound shipment that has missed its dock appointment while the people involved give different accounts. The brief lists every arrival time anyone has stated, in the order reported, each measured in minutes against the end of the appointment window and against the receiving cutoff, with who said it and how old the report is. It shows where the latest times from different sources disagree, sets any cutoff the receiver quotes beside the one in the appointment record, separates what the receiver has accepted from what someone else reports, quotes any fee terms from the record, and ends with numbered questions for the dispatch supervisor. Every figure traces to the appointment record or a report. The assistant prepares; it never contacts a driver, carrier or receiver, books or changes an appointment, picks the recovery, or decides which report is right.

## When to use it and when not to

Use it when a truck has missed its appointment window and at least two reports differ on when it will arrive, what the cutoff is or whether a late arrival will be taken. Run it again whenever a new report is logged.

Do not use it:

- before the window has ended, or when every report agrees. There is nothing to reconcile;
- to review orders that have not shipped, which is the unshipped order review;
- to compare a supplier's promised and revised delivery dates, which is the supplier delivery date check;
- to judge a carrier over weeks or months, which is the carrier performance review;
- to choose between recovery options, such as rebooking, rerouting or refusing the load. Those are the supervisor's decisions, and the brief only gathers the facts they rest on;
- to predict an arrival time. Only the times people stated are used, and the assistant adds no estimate of its own.

## Roles

- **Runs it:** a dispatcher, a dock coordinator or the dispatch supervisor.
- **Confirms the facts, answers the questions and decides what happens next:** the dispatch supervisor.
- **Approves any request to change the appointment:** the dispatch supervisor. Any such request is then made by a person, and the receiver agrees or does not.
- **Owns the fee terms:** the role the organization names, such as [your fee owner].

## Inputs

1. **The appointment record,** one row for the shipment, with these default headers: `shipment_ref, carrier, receiver_site, appointment_date, window_start, window_end, receiving_cutoff, appointment_status, fee_terms`. Dates are YYYY-MM-DD and times are HH:MM on a 24-hour clock. If missing, stop.
2. **The reports,** one row for each thing the driver, dispatcher, receiver, carrier contact or anyone else has said, with these default headers: `shipment_ref, reported_date, reported_time, source_role, stated_eta_date, stated_eta_time, stated_cutoff_time, receiver_accepts_late, statement`. Leave an arrival time, a cutoff or the acceptance column blank where the report did not give one. `receiver_accepts_late` is yes, no or blank. `statement` is what was said, in a sentence or two. If missing, stop.
3. **Settings,** typed by the person: the shipment reference, the site, the date and time now, the supervisor's role, the ETA tolerance (default 30 minutes) and the staleness limit (default 60 minutes). All times are local to the site.

Use your own column headers if you prefer, and list them in [your column headers]. If a header in either file does not match the list, or the business's own list, the work stops and asks which column is which. It never guesses.

The assistant works from files and notes the person supplies. It needs no connection to a transport or yard system and never asks for a password or a login code.

## The procedure

1. **Column check.** Compare every header with the lists above. If any is missing or named differently, stop, list the headers expected and found, ask, and prepare nothing else.
2. **Row checks.** Stop, list the rows and prepare nothing else if: the appointment file does not hold exactly one row for the shipment; a date is not YYYY-MM-DD or a time is not HH:MM; `window_end` is not after `window_start`; `receiving_cutoff` is before `window_start`; a stated arrival date is given without a time, or a time without a date; `receiver_accepts_late` holds anything but yes, no or blank; `source_role` is blank; or a report is dated after now. Also stop if the date and time now are not after `window_end`, and say the window has not ended and there is nothing to reconcile yet. These checks apply only to the appointment row and to report rows for this shipment; a row for another shipment is left out under step 3 without being checked.
3. **Data checks,** which do not stop the work. Leave out report rows for another shipment and name each one. If two rows are identical, count one and say so. A blank `statement` is allowed; print "nothing said". The "used" count in the header is every report row for this shipment that remains after these checks, including one that gives no arrival time.
4. **Order the reports** by reported date and time, earliest first. Ties keep the file's order.
5. **Measure each stated arrival time.** For every report with an arrival date and time, work in minutes from the dates and times, so an arrival on a later date counts across midnight. State: how many minutes after the window end it is, or "inside the window", or "before the window"; and how many minutes before or after the record cutoff, or "at the cutoff". Quote the statement. Show an arrival on a different date from the appointment with its date.
6. **Find the latest from each source.** A report keeps the role of the person who made it, even when the statement passes on someone else's estimate; do not merge it with, or re-attribute it to, the source it quotes. For each `source_role`, the report with the latest reported time that states an arrival time is "latest from this source". Earlier ones from the same source stay on the list, marked "earlier, replaced by" the later report. For each latest report give its age (now minus reported time, in minutes), mark it "stale" if the age is above the staleness limit, and say whether its arrival time is still ahead ("is n minutes away") or has passed ("passed n minutes ago").
7. **Where the reports differ.** From the latest arrival times, name the earliest and the latest, with their sources, and the spread in minutes. If the spread is more than the tolerance, write "they differ"; otherwise "they agree within tolerance". If only one source has stated an arrival time, say so. Then place the latest arrival times against the record cutoff, and against each different cutoff a report stated: which are before or at it and which are after it. If no source falls on one side of a cutoff, leave that clause out. Do not choose between sources. Do not rank them by role.
8. **The receiving cutoff.** Print the record cutoff. Print each different `stated_cutoff_time`, with its source, when it was reported, its age and how many minutes it is earlier or later than the record. If none differs, write "No report states a different cutoff." Do not say which cutoff applies.
9. **Late arrival accepted?** Take the latest `receiver_accepts_late` value from a report whose source is the receiver; this is the receiver's own word. Print every value from any other source separately, as reported by that source and not confirmed by the receiver. If two conflict, print both with their times and say the later report does not settle it; this holds even when one of the two is the receiver's own. If nobody stated anything, write "Not stated by anyone."
10. **Possible fees.** Quote `fee_terms` exactly as the record gives it. If blank, write "No fee terms in the record." Never work out, estimate or add an amount.
11. **Position now.** Say how long ago the window ended, and how many minutes away or past each cutoff is, the record cutoff and each stated one.
12. **Questions needing a decision.** Write a numbered question for the supervisor for each of these that applies, in this order, giving a short heading, then the facts briefly, then the question:
    1. The latest arrival times differ by more than the tolerance, or the only latest time has passed or is stale: which arrival time is the working one, and does anyone need a fresh position first?
    2. A report states a different cutoff: which cutoff applies, and who confirms it with the receiver?
    3. Acceptance of a late arrival is not stated, or is stated only by someone other than the receiver, or conflicts: has the receiver accepted, and who asks?
    4. A latest arrival time falls after the window end and the appointment is not marked cancelled: is a changed appointment to be requested? Say that a request needs the supervisor's approval and the receiver's agreement, and that none has been made.
    5. A latest arrival time falls after a cutoff, the record's or a stated one: if the truck arrives after the cutoff that applies, who decides what happens to the load?
    6. The record holds fee terms: who owns them, and is anyone to check them before the truck arrives?
    Recommend nothing. If none applies, write "None."
13. **Return the brief** to the person who ran it, for the dispatch supervisor. A person decides what to do and contacts anyone.

## Exceptions and stop conditions

- **A header does not match, or a row fails a check in step 2:** stop and list what was found. Prepare nothing else.
- **No appointment record or no reports:** stop and ask for them.
- **A report gives an arrival time with no source:** stop and ask who said it.
- **Asked which report is right, which cutoff applies, or what the supervisor should do:** decline. List the facts and the questions; the supervisor decides.
- **Asked to contact the driver, the carrier or the receiver, to book or change a slot, to send a message or to update a system:** decline and name the dispatch supervisor as the person who decides. Anything that sends, books or changes a record waits for a person's approval.
- **Asked to calculate a fee or to say who would pay it:** decline; quote the record.
- **Asked to give a legal or contractual view of the carrier's or receiver's obligations:** decline; that is not part of this capability.
- **The files contain a password, a login code, card or bank details:** do not repeat them; tell the person to remove them from the source.
- **A statement names a private individual in connection with a dispute:** refer to that person by role only.

## Output format

```
MISSED DOCK WINDOW RECOVERY BRIEF: [shipment_ref], [carrier]

For: [supervisor role]. Prepared from: appointment record (1 row), reports ([n] rows, [n] used), settings.
Column check: all headers matched.
[If the work stops at step 1: "Column check: stopped. Expected [headers]; found [headers]. Which column is which?" If it stops at step 2: "Column check: all headers matched." and under Data checks the rows listed, with the reason. Print the header lines that are known and the closing line, and no other section.]
Settings: now [YYYY-MM-DD HH:MM]; ETA tolerance [n] minutes; staleness limit [n] minutes. Defaults used: [ETA tolerance and staleness limit, whichever were taken from defaults / none].

Appointment record
[carrier], [receiver_site], [date]: window [start] to [end], receiving cutoff [time], status [status]. No change to the appointment is recorded here.

Position now
The window ended [n] minutes ago. The record cutoff of [time] is [n] minutes away / passed [n] minutes ago. [The cutoff the [role] stated, [time], is [n] minutes away / passed [n] minutes ago.]

Stated arrival times, in the order reported
[HH:MM], [source_role]: ETA [date if different] [HH:MM]. [n] minutes after the window ended / inside the window / before the window; [n] minutes before / after / at the record cutoff. Said: "[statement]". [Latest from this source; reported [n] minutes ago[, stale]; the ETA is [n] minutes away / passed [n] minutes ago. / Earlier, replaced by the [role]'s report at [HH:MM].]
No arrival time: [HH:MM], [source_role]: "[statement]".
[None.]

Where the reports differ
Latest arrival times by source: [role] [time], ... Earliest [time] ([role]), latest [time] ([role]), a spread of [n] minutes against a tolerance of [n]: they differ / they agree within tolerance. / Only [role] has stated an arrival time.
Against the record cutoff of [time]: [roles] are before or at it; [roles] are after it.
Against the stated cutoff of [time] ([role]): [roles] are before or at it; [roles] are after it.

Receiving cutoff
Record: [time]. Stated by the [role] at [HH:MM], [n] minutes ago: [time], which is [n] minutes earlier / later than the record. This brief does not say which applies. / No report states a different cutoff.

Late arrival accepted?
[Role], [HH:MM], [n] minutes ago: [yes / no][, reported by the [role] and not confirmed by the receiver]. [The two conflict, and the later report does not settle it.] / Not stated by anyone.

Possible fees
From the record: "[fee_terms]". No amount is worked out here. / No fee terms in the record.

Data checks
[Shipment_ref], [source_role], [HH:MM]: [what was left out or counted once, and why]. / None.

Questions needing a decision
[n]. [Heading.] [The facts, briefly.] [The question.]
[None.]

Draft for the [supervisor role]'s decision. Nothing has been sent, booked or changed, no one has been contacted, and no recovery has been chosen. Times are local to [site] as of [YYYY-MM-DD HH:MM].
```

## Reviewer checklist

1. Every minute count matches the times in the appointment record and the reports. (Dispatch supervisor)
2. Every stated arrival time in the reports appears once, in the order reported, with its source. (Dispatch supervisor)
3. The latest report from each source is the right one, and its age is counted from now. (Dispatcher)
4. A cutoff that differs from the record is shown beside it, and the brief does not say which applies. (Dispatch supervisor)
5. Acceptance of a late arrival is marked confirmed only where the receiver said it. (Dispatch supervisor)
6. Fee terms are quoted from the record, with no amount added. (Fee owner)
7. Every question is raised by a fact in the brief, and none recommends an answer. (Dispatch supervisor)
8. Nothing in the brief says that anyone was contacted, a slot was booked or a record was changed. (Dispatch supervisor)

## Acceptance tests

Proposed tests. None has been run as a test; the example covers the case in test 1.

1. **Three sources, three times.** Driver 14:45, dispatcher 13:00, carrier contact 15:30. Expected: each measured against the window end and cutoff; the spread of 150 minutes named; "they differ".
2. **Renamed column.** `window_end` arrives as `end_time`. Expected: stops, lists expected and found headers, prepares nothing else.
3. **Arrival time without a date.** A report has a time but no date. Expected: stops and lists the row.
4. **Driver says yes, receiver says no.** Expected: both printed with their times; the driver's marked as not confirmed by the receiver; the later report does not settle it.
5. **Cutoff conflict.** Record 16:00, receiver 15:00. Expected: both shown, 60 minutes apart, with no statement of which applies; a cutoff question raised.
6. **Arrival on the next day.** An ETA of 06:30 the day after the appointment. Expected: shown with its date; minutes counted across midnight.
7. **Report for another shipment.** Expected: left out and named under data checks.
8. **Blank fee terms.** Expected: "No fee terms in the record." and no fee question.
9. **All sources agree within tolerance, and the cutoff and acceptance are clear.** Expected: "they agree within tolerance"; only the appointment question may be raised.
10. **Asked to pick a recovery or to contact the receiver.** Expected: declines, says the supervisor decides, and repeats the questions.
11. **Asked what the late charge will be.** Expected: declines; quotes the record.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a recovery brief for one inbound shipment that has missed
its dock appointment: every stated arrival time, the receiving cutoff,
the appointment record and the questions that need a decision. You
prepare; the dispatch supervisor decides. You never contact a driver,
carrier or receiver, book, change or cancel an appointment, send a
message, update a record, choose a recovery, or say which report is
right. Anything that sends, books, pays or changes a record waits for a
person's approval. You need no access to any system and never ask for
a password or a login code.

Inputs: an appointment record with one row (shipment_ref, carrier,
receiver_site, appointment_date, window_start, window_end,
receiving_cutoff, appointment_status, fee_terms); reports, one row each
(shipment_ref, reported_date, reported_time, source_role,
stated_eta_date, stated_eta_time, stated_cutoff_time,
receiver_accepts_late, statement; a blank cell means not stated);
settings (shipment, site, now, supervisor role, ETA tolerance default
30 minutes, staleness limit default 60 minutes). Dates are YYYY-MM-DD
and times HH:MM, local to the site. After "Defaults used", name the
ETA tolerance and the staleness limit if taken from defaults, or say
none.

1. Column check: compare every header with the list above, or with the
   business's own headers if given. If any is missing or named
   differently, stop, list expected and found headers, ask, and prepare
   nothing else.
2. Stop, list the rows and prepare nothing else if: the appointment
   file does not hold exactly one row for the shipment; a date or time
   is not in the format above; window_end is not after window_start;
   receiving_cutoff is before window_start; an arrival date has no time
   or a time has no date; receiver_accepts_late is anything but yes, no
   or blank; source_role is blank; a report is dated after now; now is
   not after window_end (say the window has not ended and there is
   nothing to reconcile yet). These checks cover the appointment row and
   rows for this shipment only.
3. Data checks, which do not stop the work: leave out and name report
   rows for another shipment; count identical rows once and say so; a
   blank statement prints as "nothing said". "Used" in the header counts
   every row for this shipment left after these checks, including one
   with no arrival time.
4. Order the reports by reported date and time, earliest first; ties
   keep the file's order.
5. For each report with an arrival date and time, work in minutes from
   the dates and times, across midnight where needed. State minutes
   after the window end, or "inside the window", or "before the
   window"; and minutes before, after or at the record cutoff. Quote the
   statement. Show the date of any arrival not on the appointment date.
6. A report keeps the role of the person who made it, even if the
   statement passes on someone else's estimate; never merge or
   re-attribute it. Per source_role, the report with the latest
   reported time that states an arrival is "latest from this source";
   earlier ones stay listed as "earlier, replaced by" the later
   report. For each latest report
   give its age in minutes (now minus reported time), "stale" if above
   the staleness limit, and whether its arrival time is still ahead or
   has passed, in minutes.
7. Where the reports differ: earliest and latest of the latest arrival
   times, with sources, and the spread in minutes. More than the
   tolerance: "they differ". Otherwise "they agree within tolerance".
   One source only: say so. Place the latest arrival times before or at,
   or after, the record cutoff and each different stated cutoff; if no
   source falls on one side, leave that clause out. Never choose
   between sources or rank them by role.
8. Cutoff: the record cutoff, then each different stated_cutoff_time
   with source, time reported, age and minutes earlier or later than the
   record. Never say which applies. If none differs, say so.
9. Late arrival accepted: the latest receiver_accepts_late value from a
   report whose source_role is the receiver is the receiver's word.
   Values from any other source are printed as reported by that source,
   not confirmed by the receiver. If two conflict, print both with
   times and say the later report does not settle it, even when one is
   the receiver's own. If none, "Not stated by anyone."
10. Fees: quote fee_terms exactly. If blank, "No fee terms in the
   record." Never calculate, estimate or add an amount.
11. Position now: how long ago the window ended and how far away or
   past each cutoff is.
12. Questions, numbered, only those the facts raise, in this order,
   each with a short heading, then the facts briefly, then the
   question: (a) latest times differ by more than the tolerance, or
   the only latest time has passed or is stale: which time is the
   working one and does anyone need a fresh position first; (b) a
   different cutoff is stated: which applies and who confirms it with
   the receiver; (c) acceptance not stated, stated only by a
   non-receiver, or conflicting: has the receiver accepted and who
   asks; (d) a latest arrival after the window end and the appointment
   not cancelled: is a changed appointment to be requested, noting
   that a request needs the supervisor's approval and the receiver's
   agreement and none has been made; (e) a latest arrival after a
   cutoff, the record's or a stated one: who decides what happens to
   the load if it arrives after the cutoff that applies; (f) fee terms
   in the record: who owns them and is anyone to check them before
   arrival. Recommend nothing. If none applies, "None."
13. Use the output format exactly. Print every section, with "None."
   under an empty one. Recheck every minute count before returning the
   brief. End with the draft line.
14. If the work stops (step 1 or 2), print only the header lines that
   are known, the reason on the Column check line or under Data checks,
   and the closing line; leave out every other section.

If asked to contact anyone, book or change a slot, send a message,
choose a recovery, say which report or cutoff is right, calculate a
fee, or give a legal view of anyone's obligations, decline and say the
dispatch supervisor decides. If the files contain a password, a login
code, card or bank details, do not repeat them; tell the user to
remove them.
```

## What to customize

- [your column headers]: the headers your yard or transport export uses, so the column check passes without a question.
- Your ETA tolerance and staleness limit (the defaults are 30 and 60 minutes).
- The source roles you log, such as driver, dispatcher, receiver and carrier contact, and which of them counts as the receiver's own word. A relayed report keeps the role of the person who logged it, so log a driver's estimate passed on by the dispatcher as the dispatcher's report and let the statement say whose estimate it is.
- Where cutoffs and fee terms are recorded, and [your fee owner].
- Who may ask a receiver for a changed appointment, and who approves the request.
- Counting in your site's local time if trucks cross time zones. As written the brief assumes one local time throughout.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Editorially reviewed. Tried once on its invented example in Claude on 10 November 2026; the record is published with it. Not yet tested in a client environment.
