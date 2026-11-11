# Trial: Missed dock window recovery brief, run once on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs are the invented example in [example.md](example.md): the settings, the one-row appointment record and the six reports for shipment S-4471. No client data was used. The run did not read the published brief until its own was finished. It followed the instruction block and the output format in the member template, as written.

## What came out

The brief below is the full output of the run. The differences from the published example are listed under "What was observed".

```
MISSED DOCK WINDOW RECOVERY BRIEF: S-4471, Carrier A

For: the dispatch supervisor. Prepared from: appointment record (1 row), reports (6 rows, 5 used), settings.
Column check: all headers matched.
Settings: now 2026-11-10 14:20; ETA tolerance 30 minutes; staleness limit 60 minutes. Defaults used: ETA tolerance, staleness limit.

Appointment record
Carrier A, the Depot, 2026-11-10: window 10:00 to 11:00, receiving cutoff 16:00, status confirmed. No change to the appointment is recorded here.

Position now
The window ended 200 minutes ago. The record cutoff of 16:00 is 100 minutes away. The cutoff the receiver stated, 15:00, is 40 minutes away.

Stated arrival times, in the order reported
09:40, driver: ETA 11:30. 30 minutes after the window ended; 270 minutes before the record cutoff. Said: "Traffic on the ring road. Expects 11:30." Earlier, replaced by the driver's report at 12:50.
11:05, dispatcher: ETA 13:00. 120 minutes after the window ended; 180 minutes before the record cutoff. Said: "Driver called in about roadworks. Gave 13:00 as his estimate." Latest from this source; reported 195 minutes ago, stale; the ETA passed 80 minutes ago.
12:50, driver: ETA 14:45. 225 minutes after the window ended; 75 minutes before the record cutoff. Said: "Says the dock clerk told him by phone they will take him." Latest from this source; reported 90 minutes ago, stale; the ETA is 25 minutes away.
13:30, carrier contact: ETA 15:30. 270 minutes after the window ended; 30 minutes before the record cutoff. Said: "Last tracking ping 13:25 about 60 km from the Depot. Planner's ETA 15:30." Latest from this source; reported 50 minutes ago; the ETA is 70 minutes away.
No arrival time: 11:20, receiver: "Nothing is received after 15:00 today. Has not agreed to a late slot."

Where the reports differ
Latest arrival times by source: dispatcher 13:00, driver 14:45, carrier contact 15:30. Earliest 13:00 (dispatcher), latest 15:30 (carrier contact), a spread of 150 minutes against a tolerance of 30: they differ.
Against the record cutoff of 16:00: dispatcher, driver and carrier contact are before or at it.
Against the stated cutoff of 15:00 (receiver): dispatcher and driver are before or at it; carrier contact is after it.

Receiving cutoff
Record: 16:00. Stated by the receiver at 11:20, 180 minutes ago: 15:00, which is 60 minutes earlier than the record. This brief does not say which applies.

Late arrival accepted?
Receiver, 11:20, 180 minutes ago: no. Driver, 12:50, 90 minutes ago: yes, reported by the driver and not confirmed by the receiver. The two conflict, and the later report does not settle it.

Possible fees
From the record: "Late-arrival charge may apply after window end. Amount not stated." No amount is worked out here.

Data checks
S-4480, dispatcher, 12:10: a report for another shipment; left out.

Questions needing a decision
1. Which arrival time is the working one? The latest times differ by 150 minutes against a tolerance of 30. The dispatcher's 13:00 has passed (80 minutes ago) and is stale, the driver's 14:45 is stale, and only the carrier contact's 15:30 is within the staleness limit. Does anyone need a fresh position first?
2. Which cutoff applies? The record says 16:00; the receiver said 15:00 at 11:20, 60 minutes earlier. Who confirms it with the receiver?
3. Has the receiver accepted a late arrival? The receiver said no at 11:20; the driver said at 12:50 that the dock clerk would take him. Who asks?
4. Is a changed appointment to be requested? Every latest arrival time falls after the window ended at 11:00 and the appointment is recorded as confirmed. A request needs the supervisor's approval and the receiver's agreement; none has been made.
5. If the truck arrives after the cutoff that applies, who decides what happens to the load? The carrier contact's 15:30 is 30 minutes after the receiver's stated 15:00 cutoff.
6. Who owns the fee terms, and is anyone to check them before the truck arrives? The record says a late-arrival charge may apply and gives no amount.

Draft for the dispatch supervisor's decision. Nothing has been sent, booked or changed, no one has been contacted, and no recovery has been chosen. Times are local to the Depot as of 2026-11-10 14:20.
```

## What was observed

- Every required part was produced, in the order the output format sets, and nothing stopped the work. The column check passed, no row failed a step 2 check, and one row (S-4480) was left out under the data checks.
- Every minute count agrees with the published example: the window ended 200 minutes ago; the arrivals are 30, 120, 225 and 270 minutes after the window end; the ages are 195, 90 and 50 minutes; the spread is 150 minutes. Each count was worked from the times in the inputs.
- Differences from the published example are small. The example adds the sentence "The receiver has given no arrival time" under "Where the reports differ"; the template does not call for it. The example says "before it" where the format says "before or at it". The questions are worded differently. The example puts a short heading in front of each question ("Arrival time", "Cutoff") and states the facts first, then the question; the run put the question first, with the facts after it, and gave the staleness of each latest time in question 1. Question 1 in the example suggests a fresh position "from the driver or the carrier contact"; the run asked only whether anyone needs one.
- No fact in the run's output is missing from the inputs. In the published example, the same holds, apart from the two suggested sources of a fresh position in question 1, which is a suggestion and not a fact.
- No one was told to stop for anything, and no instruction asked for a decision the assistant could not make.

### Where the instructions were ambiguous or the run had to guess

1. **Which rows count as "used".** The header line asks for "[n] rows, [n] used". The template does not say whether a report with no arrival time (the receiver's) counts as used. The run counted it, giving 5 of 6, as the example does.
2. **Step 2 against step 3.** The row checks stop the work for a bad date, a blank source or a report dated after now, but the template does not say whether those checks apply to rows for another shipment, which step 3 leaves out. The run applied them to rows for this shipment only.
3. **"Defaults used".** The supervisor's role was typed as "not named, use the role". The template does not say whether that counts as a default to name. The run named only the two numeric settings.
4. **"Before or at" versus "before".** The format says "are before or at it", which the run kept; with no arrival exactly at a cutoff the words are harmless, but the template does not say what to print when only one of the two applies.
5. **A conflict between the receiver and a non-receiver.** Step 9 says that if two values conflict, the later report does not settle it. It does not say whether this applies when one value is the receiver's own word and the other is a different source's, as here. The run applied it, as the acceptance test 4 implies.
6. **The question wording.** Step 12 gives each question's trigger and topic but no wording, so the run chose its own; the facts-then-question order in step 12 and the output format ("[Heading.] [The facts, briefly.] [The question.]") was followed loosely in the run. The format asks for a heading, then facts, then the question; the run's version did not repeat this order exactly. A reviewer may want the format to say this more firmly.
7. **Question 5 when several cutoffs exist.** "A latest arrival time falls after a cutoff" does not say whether to ask when the arrival is after only the stated cutoff, not the record cutoff. The run asked, as the example does.
8. **Question 4 and several sources.** The trigger fires if any latest arrival is after the window end; the template does not say how to phrase this when all are, so the run said "every latest arrival time".
9. **The version notes are now out of date.** They say the template was "Not yet tried on its invented example". The acceptance tests are also marked "None has been run", and this trial ran only the example, not those eleven tests.

### Shortcomings of this trial

- It is one run by one model, on one invented example. It does not test the stop conditions, the declines, the renamed-column case, an arrival across midnight or blank fee terms.
- The run was not independent of the template's author in one respect: the model followed the template's own wording, so the check shows the template can be followed to the published result, not that every real dispatcher would reach it.
- Nothing was tried in a client environment.

### Changes made after this run

The run above is recorded as it happened and has not been repeated. After an independent review, on 10 November 2026, the member template and the published example were edited. The edits did not change the example's inputs or any figure in its brief. In the template: the version notes now say it was tried; the "used" count, the scope of the step 2 row checks, the "Defaults used" line, and a relayed report keeping its reporter's role are each settled in one line; the format no longer offers the "window opens in" and "window is open" variants, and the work stops if the window has not ended. In the example: the sentence about the receiver's missing arrival time was dropped, "before it" became "before or at it", and question 1 no longer suggests where a fresh position should come from. So the differences listed in the third observation above, apart from the wording of the questions, no longer apply to the current example. Ambiguities 1, 2, 3 and 9 are settled by those edits. These edited instructions have not themselves been run.

A second review, on the same day, asked for further one-line settlements in the member template, none of which changes a figure: what to print when no source falls on one side of a cutoff (ambiguity 4), that the conflict rule also holds when one value is the receiver's own (5), a short heading before the facts and the question in step 12 (6), that question 5 fires for a stated cutoff as well as the record cutoff (7), and a stopped form of the Column check line in the output format. The step 2 sentence about a window that has not ended was also split in two. Ambiguity 8 (the wording of question 4 when every latest time qualifies) is left as the run handled it. These edits have not been run either; the example's inputs and brief are unchanged, and a rerun is worth doing if a later round touches the template.
