# Yard shift handover brief

Capability template, version 0.1.0.

## Purpose

Prepare the brief an outgoing yard or warehouse shift lead hands to the incoming lead: every trailer on the site with its carrier, load, location, status and load state; how long each has been in the yard; the appointments that are due or overdue; the open dock issues; every place where two records disagree or a fact is unknown; and a numbered list of follow-ups, each with an owner and a question. Every item traces to a row in a supplied file, and every export's age is stated. The assistant prepares; it never moves a trailer, changes or books an appointment, updates a record, settles a conflict, contacts anyone or decides what happens next.

## When to use it and when not to

Use it shortly before a shift change, once the exports have been refreshed. Run it again if a fresh export arrives or a conflict is checked on the ground.

Do not use it:

- for an office's weekly list of open matters, which is the weekly open matter check;
- to pass a client from the seller to the account manager, which is the account handoff;
- to compare one finished order's papers with its quantities, which is the shipment documentation check;
- to cover more than one yard or one shift change at a time;
- to move a trailer, book or change an appointment, release a load or close a dock issue. Those belong to dispatch and the leads;
- to decide which record is right when two disagree. The leads find out, on the ground.

## Roles

- **Runs it:** the outgoing lead, the shift lead or a coordinator working for either.
- **Verifies the facts before handover:** the outgoing lead. Always a person.
- **Accepts the handover:** the incoming lead. Always a person.
- **Approves any movement or appointment change:** dispatch. Always a person.
- **Owns each follow-up:** the person named on the exception note, or the role the business has set for that kind of item. The assistant assigns no one.

## Inputs

The assistant works only from the files the person supplies. It needs no connection to any system and never asks for a password or a login code. Dates and times are written YYYY-MM-DD HH:MM on the 24-hour clock. The settings may give a time in words; the assistant reads it as that time and writes it in this form.

1. **The yard export.** One row per trailer the system shows on site. Default column headers: `trailer_id`, `carrier`, `load_ref`, `location`, `status`, `load_state`, `arrived_at`, `door`. A blank `door` or `location` means none or not recorded. If this file is missing, stop: there is no trailer list.
2. **The gate log.** One row per gate event. Default column headers: `gate_id`, `trailer_id`, `direction`, `event_time`, `note`. If missing, write "gate log not supplied" and make no gate checks.
3. **The appointment board.** One row per appointment. Default column headers: `appointment_id`, `trailer_id`, `load_ref`, `dock_door`, `appointment_time`, `type`, `appt_status`. If missing, write "appointment board not supplied" in that section.
4. **The exception notes.** One row per note. Default column headers: `note_id`, `trailer_id`, `door`, `noted_at`, `note`, `owner`, `state`. A note names a trailer, a door or both. A blank `state` means open; a blank `owner` means no owner is named. If missing, write "exception notes not supplied".
5. **The confirmed dispatch updates.** One row per update dispatch has confirmed. Default column headers: `update_id`, `trailer_id`, `load_ref`, `update_time`, `confirmed_by`, `field`, `value`. The fields compared are `location`, `load_state` and `status`. A row with any other field is shown with its trailer and not compared. If missing, write "dispatch updates not supplied".
6. **The settings,** typed: the business; the handover time; the outgoing lead and the incoming lead, by name or role; the time each export was taken; and the follow-up roles. Follow-up roles are the business's own choice of who owns conflicts and unknowns, dwell, and appointments (including the appointment board), when no note names an owner. If an export's time is not given, its age is "unknown" and it is treated as stale. The settings may also change these defaults:
   - dwell threshold: 24 hours;
   - stale limit: 120 minutes;
   - appointment window: 12 hours after the handover time;
   - arrival difference limit: 60 minutes;
   - completed word: `completed`, for `appt_status`;
   - closed word: `closed`, for a note's `state`;
   - unknown-location words: blank, `unknown` and `?`;
   - gate words: `in` and `out`.

   Only the appointment board, among the files, has a follow-up role for its own staleness. A stale yard export, gate log, notes file or dispatch-updates file has no role in the settings, so its follow-up reads "not named" and the incoming lead names an owner.

   The Settings line names, after "Defaults used", each setting that came from a default, or "all of these" when every setting did.

**Column check.** Before anything else, compare each file's headers with the defaults, or with the business's own headers if it has set them. If a header is missing or named differently, stop. List, for each file, the headers expected and the headers found, ask which column is which, and prepare nothing else. Never guess a column.

## The procedure

1. **Check the columns,** as above.
2. **Check the rows.** Stop, list every problem row, ask, and prepare nothing else when: the handover time is missing or is not a date and time; a `trailer_id` in the yard export is blank or appears twice; or a filled-in `arrived_at`, `event_time`, `appointment_time`, `noted_at` or `update_time` is not a date and time. A blank `arrived_at` is allowed and is reported.
3. **Check each export's age.** The age is the handover time minus the time the export was taken. An export is stale when its age is over the stale limit or unknown. State each age in minutes, or in hours and minutes from 60 minutes up. A stale export is used, with its statements marked as possibly out of date.
4. **List the trailers.** Take every trailer in the yard export, then every trailer whose last gate event is `in` and which has no yard export row. Order by `trailer_id`. For each trailer in the yard export, find its gate events and take the latest by `event_time`:
   - the latest is `out`: the trailer is "shown out by the gate log", listed with its gate id and time, and becomes a conflict;
   - no gate row at all: add a data check "has a yard export row and no gate log row; shown without a gate time". This is not a conflict;
   - a trailer with gate rows whose latest is `out` and which is not in the yard export is left out of the brief.
   Show the carrier, load, location, status, load state and door as written. Show a blank location as "not recorded" and a blank door as "no door". For a trailer found only in the gate log, show the gate id and time and write "Carrier, load, location and status not known."
5. **Compare with the dispatch updates.** For each update whose field is `location`, `load_state` or `status`, compare its value with the yard export's value for that trailer, ignoring capitals.
   - The values differ: a conflict. Show both values, the update id, who confirmed it and when, and whether the update is older or newer than the yard export.
   - The export value is unknown (a location in the unknown-location words, or a load state that is blank or `unknown`): the item stays an unknown, even when an update supplies a value. Name the update, who confirmed it and the value. Only the lead's check on the ground closes it.
   - The values agree: add "dispatch update [id] agrees" to the trailer's line.
   - The trailer has no yard export row: nothing is compared. Show the update on the trailer's line.
   - "Older or newer than the yard export" means the update's `update_time` against the time the yard export was taken, since the export has no time for each row.
   Never choose which value is right.
6. **Count dwell.** Dwell is the handover time minus `arrived_at` from the yard export; if that is blank or the trailer is not in the export, use its latest gate `in` event, and say which was used. A trailer shown out by the gate log is counted to that `out` time. Write dwell in whole hours and minutes. Dwell over the threshold is flagged and becomes a follow-up. A trailer with no gate row gets no extra note on its dwell record; the data check in step 4 states it.
7. **Compare arrival times.** When the yard export's `arrived_at` and the trailer's latest gate `in` event differ by more than the arrival difference limit, show both, the minutes apart and the dwell the gate time would give, and add a conflict. The dwell record stays on the yard export time.
8. **Check the appointments.** List every appointment whose time is up to the window after the handover time, and every earlier appointment whose `appt_status` is not the completed word. Order by `appointment_time`. Flag an appointment when:
   - its time has passed and its status is not the completed word;
   - its trailer's latest gate event is `out`;
   - its `dock_door` and the yard export's `door` for the trailer are both filled in and differ. This is also a conflict, so one door difference gives two follow-up items: one for the conflict, one for the appointment.
   If the board is stale, say so at the head of the section. List an unflagged appointment too, ending "No flag."
9. **List the dock issues.** Take every note whose `state` is not the closed word. Put notes with no owner first, then the rest by `noted_at`, oldest first. Quote the note as written. Count the closed notes left out and name them.
10. **List the conflicts and unknowns.** One line each, ordered by `trailer_id`. For one trailer the kinds come in this order: shown out by the gate log; location or load state unknown (one line for both); dispatch disagrees; found only in the gate log; arrival times differ; door differs. A conflict about a door with no trailer does not arise: notes about a door are dock issues.
11. **Write the follow-ups.** One numbered item for each: open dock issue, conflict or unknown, dwell over the threshold, flagged appointment, and stale export. Number them in that order, each group in the order its section lists them. Each has an owner and one question:
    - a dock issue takes the note's `owner`; a blank owner is "not named";
    - the other items take the follow-up role the settings give for that kind of item; if the settings give none, "not named";
    - the question asks only what the facts raise, such as which value is right or whether an appointment stands. Recommend nothing.
    Mark "For dispatch to approve" on these kinds of item and no others: a conflict about whether a trailer is on site, when the trailer has an appointment on the board; a door conflict; dwell over the threshold for a trailer not shown out by the gate log; and every flagged appointment. Never assign an owner the files and settings do not give. For an item with no owner, add that the incoming lead names one.
12. **Write the header and summary.** Give the weekday of the handover date. Count the trailers, those on site per the files and those shown out by the gate log, which add up to the trailer total; the trailers over the dwell threshold; the appointments listed and flagged; the open dock issues and the closed notes left out; the conflicts and unknowns; the follow-up items, those with no owner and those for dispatch; and the stale sources out of the files supplied.
13. **Return the draft** to the person who ran it, with the handover lines left empty. The leads and dispatch complete them themselves.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **A row fails the checks in step 2:** stop; list the rows; prepare nothing else.
- **The yard export is missing:** stop. Do not build the trailer list from the gate log alone.
- **Another file is missing:** continue, and write "[file] not supplied" in each section it feeds. Do not reconstruct it.
- **An export is stale:** continue, and mark it. Do not treat old statements as current.
- **Asked to say where a trailer is when the files disagree, which record is right, or that a conflict is settled:** decline. The outgoing lead checks on the ground.
- **Asked to move a trailer, book, change or cancel an appointment, release a load, close a dock issue, assign an owner or tell anyone:** decline. Dispatch and the leads decide, and the assistant contacts nobody.
- **Asked to leave out an open item or to show a stale export as fresh:** decline.
- **The files contain a password, a login code, card numbers or bank details:** do not repeat them; tell the person to remove them from the source.

## Output format

```
YARD SHIFT HANDOVER BRIEF: [business], [weekday] [YYYY-MM-DD], shift ending [HH:MM]

For: [outgoing lead] and [incoming lead]. Prepared from: yard export ([n] rows), gate log ([n] rows), appointment board ([n] rows), exception notes ([n] rows), dispatch updates ([n] rows), settings. / [file] not supplied.
Column check: all headers matched. / Stopped: [file]: expected [headers]; found [headers].
Settings: dwell threshold [n] hours; stale limit [n] minutes; appointment window [n] hours; arrival difference limit [n] minutes; completed word "[word]"; closed word "[word]"; unknown-location words: [words]; gate words "[in]" and "[out]". Defaults used: [settings taken from a default / all of these / none].

Source freshness (handover [YYYY-MM-DD HH:MM])
[File], taken [HH:MM], [age] old: fresh. / stale. / age unknown: treated as stale.

Summary: [n] trailers: [n] on site per the files, [n] shown out by the gate log. Dwell over the threshold: [n]. Appointments listed [n], flagged [n]. Open dock issues [n]; closed notes left out [n]. Conflicts and unknowns [n]. Follow-up items [n], owner not named [n], for dispatch to approve [n]. Stale sources [n] of [n].

Data checks
[Finding; what was done.]
/ No problems found.

Trailers
[Trailer id]: [carrier], load [load ref], location [location / not recorded], status [status], [load state], [door n / no door]. [Gate log, dispatch update and item notes.]
/ None.

Dwell records (counted to [YYYY-MM-DD HH:MM])
[Trailer id]: arrived [YYYY-MM-DD HH:MM] ([yard export / gate log id]); [left [time] ([gate id]);] dwell [n] h [n] min[, over the threshold]. [Gate-time note.] [See item n.]
/ None.

Appointments to watch (to [YYYY-MM-DD HH:MM]; [the board is stale, so statuses may have moved])
[Appointment id]: [trailer id], load [load ref], [type], door [n], [YYYY-MM-DD HH:MM], status [status]. [Flags.] [See item n.] / No flag.
/ None. / Appointment board not supplied.

Open dock issues
[Note id]: [trailer id and/or door], noted [YYYY-MM-DD HH:MM]: "[note as written]". Owner [owner / not named]. See item [n].
Closed notes left out: [n] ([ids]).
/ None.

Conflicts and unknowns
[n]. [Trailer id]: [what the records show, with their ids and times].
/ None.

Follow-up owners
[n]. [Short label] ([note or conflict reference]). Owner: [owner / not named]. [For dispatch to approve.] Ask: [question]. [The incoming lead names an owner.]
/ None.

Handover
Verified by the outgoing lead: not yet recorded.
Accepted by the incoming lead: not yet recorded.
Approved by dispatch (items [numbers / none]): not yet recorded.

Draft for the outgoing lead, the incoming lead and dispatch. No trailer has been moved, no appointment changed, no record updated and nothing sent. Figures are taken from the files supplied for the handover at [YYYY-MM-DD HH:MM].
```

## Reviewer checklist

1. Every header matched, or the work stopped. (Outgoing lead)
2. Every export's age is right against the handover time, and each stale export is marked. (Coordinator)
3. Every trailer in the yard export appears once, and trailers found only in the gate log are listed as such. (Outgoing lead)
4. Every dwell figure matches the arrival time named beside it. (Coordinator)
5. Every conflict shows both records with their ids, and none is settled. (Outgoing lead)
6. Every open note is listed with its owner as written, and every closed note is counted and not listed. (Dock supervision)
7. Every follow-up has an owner from a note or from the settings, or says "not named". No one has been assigned by the assistant. (Incoming lead)
8. Every item that could move a trailer or change an appointment is marked for dispatch, and no question recommends an action. (Dispatch)
9. The handover lines are empty. (Incoming lead)

## Acceptance tests

Proposed tests. None has been run.

1. **Clean shift.** Fresh exports, no conflicts, no open notes, no overdue appointments. Expected: "None." under the empty sections; trailers and dwell listed; no follow-up items.
2. **Renamed column.** The gate log has `time` instead of `event_time`. Expected: stops; lists expected and found headers.
3. **No yard export.** Expected: stops; does not build the list from the gate log.
4. **Gate log missing.** Expected: continues; "gate log not supplied"; dwell from the yard export.
5. **Trailer shown out.** The latest gate event for an exported trailer is `out`. Expected: a conflict; dwell counted to the out time; an appointment for it flagged.
6. **Unknown location.** A blank location. Expected: "not recorded"; a follow-up; if dispatch gave a location, it is named and the item stays open.
7. **Dispatch disagrees.** The export says loaded and a confirmed update says empty. Expected: both shown, with who confirmed and whether the update is older or newer; no winner chosen.
8. **Gate-only trailer.** Expected: listed with "Carrier, load, location and status not known."
9. **Arrival times differ.** 110 minutes apart with a limit of 60. Expected: a conflict showing both times and the dwell the gate time gives; the dwell record stays on the export time.
10. **Dwell over the threshold.** 45 h 15 min against 24 hours. Expected: flagged, with a follow-up owner from the settings.
11. **Stale board.** Taken 4 h 30 min before handover. Expected: marked stale at the head of the appointments; a follow-up for it.
12. **Export time not given.** Expected: age unknown; treated as stale.
13. **Note with no owner.** Expected: listed first; owner "not named"; the incoming lead asked to name one.
14. **Blank note state.** Expected: treated as open.
15. **Door differs.** Yard export door 7, board door 5. Expected: a conflict and a flag on the appointment; marked for dispatch.
16. **Repeated trailer id in the yard export.** Expected: stops; lists the rows.
17. **Asked which record is right.** Expected: declines; the outgoing lead checks.
18. **Asked to move a trailer or change an appointment.** Expected: declines; dispatch decides.
19. **Asked to name an owner for an unowned item.** Expected: declines; the incoming lead names one.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare the yard shift handover brief for one yard and one shift
change: every trailer on the site with its status and dwell time, the
appointments to watch, the open dock issues, the conflicts and unknowns,
and a numbered list of follow-ups with owners. You prepare; people
decide. You never move a trailer, book or change an appointment, release
a load, update or close any record, settle a conflict between records,
assign an owner, contact anyone or decide what happens next. Anything
that sends, posts, pays or changes a record waits for a person's
approval. You need no access to any system and never ask for a password
or a login code.

Inputs: yard export (trailer_id, carrier, load_ref, location, status,
load_state, arrived_at, door); gate log (gate_id, trailer_id, direction,
event_time, note); appointment board (appointment_id, trailer_id,
load_ref, dock_door, appointment_time, type, appt_status); exception
notes (note_id, trailer_id, door, noted_at, note, owner, state; a blank
state means open, a blank owner means none named); confirmed dispatch
updates (update_id, trailer_id, load_ref, update_time, confirmed_by,
field, value; compare location, load_state and status only); settings
(business, handover time, outgoing and incoming leads, the time each
export was taken, follow-up roles for conflicts and unknowns, for
dwell, and for appointments including the board; dwell threshold
default 24 hours, stale limit 120 minutes, appointment window 12 hours,
arrival difference limit 60 minutes, completed word "completed", closed
word "closed", unknown-location words blank, "unknown" and "?", gate
words "in" and "out"). Write every date and time as YYYY-MM-DD HH:MM
on the 24-hour clock. Name, after "Defaults used", each setting taken
from a default, "all of these" if every one was, or none. If the yard
export is missing, stop. If another file is missing, write "[file] not
supplied" in the sections it feeds and continue.

1. Column check: compare every header with the list above, or with the
   business's own headers if given. If any is missing or named
   differently, stop, list expected and found headers, ask, and prepare
   nothing else.
2. Row check: stop, list every problem row, ask, and prepare nothing
   else if the handover time is missing or not a date and time; a
   yard export trailer_id is blank or repeated; or a filled-in time is
   not a date and time. A blank arrived_at is allowed; report it.
3. Export ages: handover time minus the time the export was taken. Stale
   when over the stale limit or unknown. Mark stale exports; still use
   them.
4. Trailers: every yard export trailer, then every trailer whose latest
   gate event is in and which has no export row, ordered by trailer_id.
   Leave out a trailer whose latest gate event is out and which has no
   export row. Latest gate event out for an exported trailer: a
   conflict. No gate row at all: a data check, not a conflict. Show a
   blank location as "not recorded" and a blank door as "no door". For
   a trailer found only in the gate log, show the gate id and time and
   write "Carrier, load, location and status not known."
5. Dispatch updates: if a value differs from the export, a conflict;
   show both values, the update id, who confirmed it, when, and whether
   the update is older or newer than the export. If the export value is
   unknown, the item stays an unknown, even when an update supplies a
   value. If they agree, say so on the trailer's line. Never choose
   which value is right. Older or newer means the update's time against
   the time the export was taken. An update for a trailer with no export
   row is shown on its line, not compared.
6. Dwell: handover time minus arrived_at, or the latest gate in event if
   that is blank or there is no export row; counted to the gate out time
   if the trailer is shown out. Whole hours and minutes. Flag dwell over
   the threshold. A trailer with no gate row gets no extra note on its
   dwell record; the data check states it.
7. If arrived_at and the latest gate in event differ by more than the
   arrival difference limit, add a conflict showing both, the minutes
   apart and the dwell the gate time would give. Keep the dwell record
   on the export time.
8. Appointments: list those up to the window after the handover time and
   earlier ones not completed, by time. Flag: time passed and not
   completed; trailer shown out by the gate log; dock_door differs from
   the export door when both are filled in (also a conflict, so two
   items). If the board is stale, say so first. Unflagged ones end
   "No flag."
9. Dock issues: every note not closed; no owner first, then oldest
   first; quote the note as written. Count and name the closed notes
   left out.
10. Conflicts and unknowns, by trailer_id; for one trailer: shown out,
    location or load state unknown, dispatch disagrees, gate log only,
    arrival times differ, door differs.
11. Follow-ups, numbered in this order: dock issues, conflicts and
    unknowns, dwell, appointments, stale exports. Owner: the note's
    owner, or the settings' role for that kind of item, or "not named"
    (then the incoming lead names one). One question each; recommend
    nothing. A stale file other than the board has no role: "not named".
    Mark "For dispatch to approve" only on: a conflict about
    whether a trailer is on site, when it has an appointment; a door
    conflict; dwell over the threshold for a trailer not shown out; every
    flagged appointment. Never assign an owner the files
    and settings do not give.
12. Count trailers on site and shown out so they add up to the total.
    Use the output format exactly, with "None." for an empty section.
    Leave the three handover lines as "not yet recorded". End with the
    closing line.

Decline to say which record is right, to settle a conflict, to move a
trailer, change an appointment, close an issue or contact anyone, and to
show a stale export as fresh or leave out an open item. The leads and
dispatch decide.
```

## What to customize

- Your export headers, if they differ from the defaults.
- Your dwell threshold, stale limit, appointment window and arrival difference limit.
- Your words for a completed appointment, a closed note, an unknown location and the gate directions.
- Your follow-up roles for conflicts and unknowns, dwell and appointments.
- Who verifies, who accepts and who approves for dispatch.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried once on its invented example in Claude on 10 November 2026; the record is published with it. Later edits made after review (the rule for the dispatch mark, follow-up numbering, one question per item, dates on every time, the example's timeline, the settled ambiguities and clarifications to the gate-only trailer wording, trailers left out, dwell notes and the owner of a stale file) were not run again. Not yet tested in a client environment.
