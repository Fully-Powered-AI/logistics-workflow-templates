# Yard shift handover brief: one run on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example's own: the settings, the yard export, the gate log, the appointment board, the exception notes and the confirmed dispatch updates in `public/example.md`. No client data was used. This was one run, by an assistant that did not write the template, following the instruction block and the output format.

One caveat about how the run was done. The template and the example file were opened in a single step, and the display cut off partway through the example's brief. The assistant therefore saw the example's source-freshness lines, the trailer list, the dwell records and the start of the appointments before it produced its own output. The rest of the output was produced from the template and the inputs and compared afterwards. Treat the agreement on those first sections as weaker evidence than the agreement on the later ones.

## What came out

```
YARD SHIFT HANDOVER BRIEF: the Depot, Tuesday 2026-11-10, shift ending 14:00

For: the outgoing lead and the incoming lead. Prepared from: yard export (6 rows), gate log (7 rows), appointment board (4 rows), exception notes (4 rows), dispatch updates (2 rows), settings.
Column check: all headers matched.
Settings: dwell threshold 24 hours; stale limit 120 minutes; appointment window 12 hours; arrival difference limit 60 minutes; completed word "completed"; closed word "closed"; unknown-location words: blank, "unknown", "?"; gate words "in" and "out". Defaults used: all of these.

Source freshness (handover 2026-11-10 14:00)
Yard export, taken 13:40, 20 minutes old: fresh.
Gate log, taken 13:45, 15 minutes old: fresh.
Appointment board, taken 09:30, 4 h 30 min old: stale.
Exception notes, taken 13:50, 10 minutes old: fresh.
Dispatch updates, taken 13:55, 5 minutes old: fresh.

Summary: 7 trailers: 6 on site per the files, 1 shown as left in the gate log. Dwell over the threshold: 2. Appointments listed 4, flagged 3. Open dock issues 3; closed notes left out 1. Conflicts and unknowns 6. Follow-up items 15, owner not named 1, for dispatch to approve 6. Stale sources 1 of 5.

Data checks
TR-4101 has a yard export row and no gate log row; shown without a gate time.

Trailers
TR-4101: Carrier A, load LD-2201, location Door 4, status unloading, loaded, door 4.
TR-4102: Carrier B, load LD-2202, location Yard A-12, status waiting, loaded, door 6. Shown out by the gate log: G-907, 2026-11-10 13:30. See item 4.
TR-4103: Carrier C, load LD-2203, location Yard B-03, status waiting, empty, no door.
TR-4104: Carrier A, load LD-2204, location not recorded, status waiting, load state unknown, no door. Dispatch update U-51 (Dispatch A, 2026-11-10 13:10) gives the location as Yard B-07. See item 5.
TR-4105: Carrier D, load LD-2205, location Door 7, status loading, empty, door 7. See items 6 and 7.
TR-4106: Carrier B, load LD-2206, location Yard A-15, status waiting, loaded, no door. See item 8.
TR-4107: Gate log G-906 shows it in at 2026-11-10 13:05. Carrier, load, location and status not known. See item 9.

Dwell records (counted to 2026-11-10 14:00)
TR-4101: arrived 2026-11-10 06:15 (yard export); dwell 7 h 45 min.
TR-4102: arrived 2026-11-09 11:20 (yard export); left 2026-11-10 13:30 (G-907); dwell 26 h 10 min, over the threshold. See item 10.
TR-4103: arrived 2026-11-08 16:45 (yard export); dwell 45 h 15 min, over the threshold. See item 11.
TR-4104: arrived 2026-11-10 09:05 (yard export); dwell 4 h 55 min.
TR-4105: arrived 2026-11-10 10:30 (yard export); dwell 3 h 30 min. Gate time G-904 is 2026-11-10 08:40, which would give 5 h 20 min. See item 6.
TR-4106: arrived 2026-11-10 12:10 (yard export); dwell 1 h 50 min.
TR-4107: arrived 2026-11-10 13:05 (gate log G-906); dwell 0 h 55 min.

Appointments to watch (to 2026-11-11 02:00; the board is stale, so statuses may have moved)
A-71: TR-4101, load LD-2201, inbound, door 4, 2026-11-10 06:30, status in progress. Time has passed and the status is not "completed". See item 12.
A-73: TR-4105, load LD-2205, outbound, door 5, 2026-11-10 11:00, status loading. Time has passed and the status is not "completed". Door differs from the yard export (door 7). See items 7 and 14.
A-72: TR-4102, load LD-2202, inbound, door 6, 2026-11-10 15:00, status scheduled. The gate log shows the trailer out. See item 13.
A-74: TR-4106, load LD-2206, inbound, door 2, 2026-11-10 16:30, status scheduled. No flag.

Open dock issues
N-32: door 7, noted 2026-11-10 11:40: "Door 7 seal damaged; draft coming in". Owner not named. See item 1.
N-31: TR-4101, door 4, noted 2026-11-10 10:20: "Dock leveler sticking; unloading slowed". Owner Dock supervisor. See item 2.
N-34: TR-4104, noted 2026-11-10 11:15: "Seal number on the paperwork does not match the trailer". Owner Yard clerk. See item 3.
Closed notes left out: 1 (N-33).

Conflicts and unknowns
1. TR-4102: the yard export lists it on site; gate log G-907 shows it out at 2026-11-10 13:30.
2. TR-4104: location not recorded and load state unknown in the yard export. Dispatch update U-51 (Dispatch A, 2026-11-10 13:10) gives the location as Yard B-07; this stays unknown until the lead checks on the ground.
3. TR-4105: arrival is 2026-11-10 10:30 in the yard export and 2026-11-10 08:40 in G-904, 110 minutes apart.
4. TR-4105: door is 7 in the yard export and 5 on the appointment board (A-73).
5. TR-4106: load state is loaded in the yard export; dispatch update U-52 (Dispatch A, 2026-11-10 13:20) says empty. The update is older than the yard export (taken 13:40).
6. TR-4107: on site per gate log G-906, with no yard export row.

Follow-up owners
1. Door 7 seal damaged (N-32). Owner: not named. Ask: who owns this, and is the door in use? The incoming lead names an owner.
2. Dock leveler at door 4 (N-31). Owner: Dock supervisor. Ask: is unloading of TR-4101 still slowed?
3. Seal number mismatch on TR-4104 (N-34). Owner: Yard clerk. Ask: which seal number is on the trailer?
4. TR-4102 listed on site and shown out (conflict 1). Owner: Yard control. For dispatch to approve. Ask: is the trailer in the yard or gone?
5. TR-4104 location and load state (conflict 2). Owner: Yard control. Ask: where is the trailer, and is it loaded or empty?
6. TR-4105 arrival time (conflict 3). Owner: Yard control. Ask: which arrival time is right?
7. TR-4105 door (conflict 4). Owner: Yard control. For dispatch to approve. Ask: is the trailer at door 7 or door 5?
8. TR-4106 load state (conflict 5). Owner: Yard control. Ask: is the trailer loaded or empty?
9. TR-4107 not in the yard export (conflict 6). Owner: Yard control. Ask: where is it, and what does it carry?
10. TR-4102 dwell 26 h 10 min. Owner: Dock supervision. Ask: is the dwell, counted to the gate out time, right?
11. TR-4103 dwell 45 h 15 min. Owner: Dock supervision. For dispatch to approve. Ask: what is the trailer waiting for?
12. A-71, time passed, status in progress. Owner: Dispatch. For dispatch to approve. Ask: is the appointment complete?
13. A-72, trailer shown out by the gate log. Owner: Dispatch. For dispatch to approve. Ask: does the appointment stand?
14. A-73, time passed, status loading, door differs. Owner: Dispatch. For dispatch to approve. Ask: is the appointment complete, and which door is right?
15. Appointment board 4 h 30 min old. Owner: Dispatch. Ask: can a fresh export be supplied?

Handover
Verified by the outgoing lead: not yet recorded.
Accepted by the incoming lead: not yet recorded.
Approved by dispatch (items 4, 7, 11, 12, 13, 14): not yet recorded.

Draft for the outgoing lead, the incoming lead and dispatch. No trailer has been moved, no appointment changed, no record updated and nothing sent. Figures are taken from the files supplied for the handover at 2026-11-10 14:00.
```

## What was observed

- **Every required part was produced,** in the order the format gives. The column and row checks passed, so nothing stopped. Nothing in the run called for a refusal.
- **Counts and figures matched the published example:** the freshness lines, all seven dwell figures, the arrival difference of 110 minutes, the appointment order and flags, the three open and one closed note, the six conflicts and unknowns in the same order, and 15 follow-up items. See the caveat above for the sections the assistant had already seen.
- **One real difference.** This run marked 6 items "For dispatch to approve" (4, 7, 11, 12, 13, 14); the example marks 5 and leaves out item 4, the trailer listed on site and shown out. The template says to mark every item whose answer could move a trailer or change an appointment. Appointment A-72 is booked for that trailer, so this run marked it. Both readings are defensible, which is a defect in the template (below).
- **Wording differences only, otherwise.** Questions are phrased differently (for example item 3: "which seal number is on the trailer?" against "has the seal number been checked?"). Conflict 2 and conflict 5 carry slightly different detail. The example's dwell item 11 and its dispatch question add "does dispatch want any movement or appointment for it?"; this run kept to one question.
- **Facts not in the inputs:** none found in either output. Both derive the weekday (Tuesday) from the date, which is arithmetic, not a new fact.
- **Told to stop for anything?** No.

### Where the template was ambiguous, or this run had to guess

1. **Which items are "for dispatch to approve."** The rule is "could move a trailer or change an appointment". Whether a conflict about a trailer's presence, a seal repair at a door with a trailer loading (N-32), or a load-state question counts is left to judgement. This run and the example differ on one item, and N-32 was left unmarked here.
2. **"Older or newer than the yard export."** The yard export has one taken-at time and no per-row time. This run compared the update time with the export's taken time. The template does not say so.
3. **The summary line "shown as left in the gate log."** The format's wording, the step 12 wording ("those shown out by the gate log") and the step 4 wording ("shown out by the gate log") differ. A trailer shown out is counted among the 7 trailers and not among those on site, but the template never says the two numbers add to the total.
4. **Overlap between a door conflict and a flagged appointment.** The door difference appears both as a conflict (item 7) and as a flag on the appointment (item 14). The template asks for both, so one fact produces two follow-ups. It does not say whether that is intended.
5. **Gate-only trailers and the dispatch comparison.** Step 4 and step 5 do not say what to do if a dispatch update names a trailer that has no yard export row (there was none in this example).
6. **A trailer that appears in the yard export with no gate row.** The data check wording is clear, but whether the dwell record should say "no gate time to compare" is not stated; this run said nothing.
7. **The "Defaults used" line.** The settings said "use the defaults" for everything, so "all of these" was used. The template does not give wording for that case.

### Shortcomings of the run

This was one run on one example, by one model, and the assistant saw part of the example's output first. It shows the instructions can be followed to a complete and consistent brief on these inputs. It does not show that the template works on a real yard's exports, with different headers, larger files or messier times. No acceptance test beyond this example was run, and the template has not been tested in a client environment.

### After the trial

The run above is recorded as it came out. After it, the template and the example were edited to settle the ambiguities listed here (which items go to dispatch, what older and newer are measured against, the summary counts, a door difference giving two items, an update for a gate-only trailer, and the "Defaults used" wording) and to correct the example's follow-up numbering, one-question items, dates on every time and request time. Later, after review, small clarifications were added (the wording for a trailer found only in the gate log, trailers left out, no extra dwell note for a trailer with no gate row, the owner of a stale file other than the board) and the example's TR-4106 line now names dispatch update U-52. The edited instructions and example were not run again, so the published example no longer matches this record line for line: it marks 6 items for dispatch, as this run did, where the example of that time marked 5, and its item 11 now asks one question as this run did; this record's follow-ups 13 and 14 (A-72, A-73) are in the opposite order to its own appointment list (A-73, A-72), and the example's are in list order; and this record's TR-4106 line does not name U-52. The ambiguity listed as 6 above is now settled in the template, but not by a run. The trial saw part of the example's output first (see the caveat at the top) and has not been repeated.
