# Yard shift handover brief: an invented example

*Illustrative example with invented data.* The business, the carriers, the trailers, the loads, the people and every time below are invented. The business is an invented regional distributor, called the Depot here. The outgoing lead asks for the brief at 13:58 on Tuesday 10 November 2026, for the shift change at 14:00. Carriers are named by letter and people by role.

The inputs come first, in full, so the template can be run on them. The brief follows.

## The inputs

### 1. Settings (typed by the outgoing lead)

```
Business: the Depot
Handover time: 2026-11-10 14:00
Outgoing lead: the outgoing lead
Incoming lead: the incoming lead
Export times: yard export 2026-11-10 13:40; gate log 2026-11-10 13:45; appointment board 2026-11-10 09:30; exception notes 2026-11-10 13:50; dispatch updates 2026-11-10 13:55
Follow-up roles: conflicts and unknowns, Yard control; dwell, Dock supervision; appointments and the appointment board, Dispatch
All other settings: use the defaults
```

### 2. Yard export

```
trailer_id,carrier,load_ref,location,status,load_state,arrived_at,door
TR-4101,Carrier A,LD-2201,Door 4,unloading,loaded,2026-11-10 06:15,4
TR-4102,Carrier B,LD-2202,Yard A-12,waiting,loaded,2026-11-09 11:20,6
TR-4103,Carrier C,LD-2203,Yard B-03,waiting,empty,2026-11-08 16:45,
TR-4104,Carrier A,LD-2204,,waiting,unknown,2026-11-10 09:05,
TR-4105,Carrier D,LD-2205,Door 7,loading,empty,2026-11-10 10:30,7
TR-4106,Carrier B,LD-2206,Yard A-15,waiting,loaded,2026-11-10 12:10,
```

### 3. Gate log

```
gate_id,trailer_id,direction,event_time,note
G-901,TR-4103,in,2026-11-08 16:50,
G-902,TR-4102,in,2026-11-09 11:20,
G-903,TR-4104,in,2026-11-10 09:05,
G-904,TR-4105,in,2026-11-10 08:40,
G-905,TR-4106,in,2026-11-10 12:10,
G-906,TR-4107,in,2026-11-10 13:05,
G-907,TR-4102,out,2026-11-10 13:30,
```

### 4. Appointment board

```
appointment_id,trailer_id,load_ref,dock_door,appointment_time,type,appt_status
A-71,TR-4101,LD-2201,4,2026-11-10 06:30,inbound,in progress
A-72,TR-4102,LD-2202,6,2026-11-10 15:00,inbound,scheduled
A-73,TR-4105,LD-2205,5,2026-11-10 11:00,outbound,loading
A-74,TR-4106,LD-2206,2,2026-11-10 16:30,inbound,scheduled
```

### 5. Exception notes

```
note_id,trailer_id,door,noted_at,note,owner,state
N-31,TR-4101,4,2026-11-10 10:20,Dock leveler sticking; unloading slowed,Dock supervisor,open
N-32,,7,2026-11-10 11:40,Door 7 seal damaged; draft coming in,,
N-33,TR-4103,,2026-11-09 17:30,Carrier C asked to collect the empty; no pickup time given,Dispatch,closed
N-34,TR-4104,,2026-11-10 11:15,Seal number on the paperwork does not match the trailer,Yard clerk,open
```

### 6. Confirmed dispatch updates

```
update_id,trailer_id,load_ref,update_time,confirmed_by,field,value
U-51,TR-4104,LD-2204,2026-11-10 13:10,Dispatch A,location,Yard B-07
U-52,TR-4106,LD-2206,2026-11-10 13:20,Dispatch A,load_state,empty
```

## The brief

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

Summary: 7 trailers: 6 on site per the files, 1 shown out by the gate log. Dwell over the threshold: 2. Appointments listed 4, flagged 3. Open dock issues 3; closed notes left out 1. Conflicts and unknowns 6. Follow-up items 15, owner not named 1, for dispatch to approve 6. Stale sources 1 of 5.

Data checks
TR-4101 has a yard export row and no gate log row; shown without a gate time.

Trailers
TR-4101: Carrier A, load LD-2201, location Door 4, status unloading, loaded, door 4.
TR-4102: Carrier B, load LD-2202, location Yard A-12, status waiting, loaded, door 6. Gate log G-907 shows it out at 2026-11-10 13:30. See item 4.
TR-4103: Carrier C, load LD-2203, location Yard B-03, status waiting, empty, no door.
TR-4104: Carrier A, load LD-2204, location not recorded, status waiting, load state unknown, no door. Dispatch update U-51 (Dispatch A, 2026-11-10 13:10) gives the location as Yard B-07. See item 5.
TR-4105: Carrier D, load LD-2205, location Door 7, status loading, empty, door 7. See items 6 and 7.
TR-4106: Carrier B, load LD-2206, location Yard A-15, status waiting, loaded, no door. Dispatch update U-52 (Dispatch A, 2026-11-10 13:20) gives the load state as empty. See item 8.
TR-4107: not in the yard export. Gate log G-906 shows it in at 2026-11-10 13:05. Carrier, load, location and status not known. See item 9.

Dwell records (counted to 2026-11-10 14:00)
TR-4101: arrived 2026-11-10 06:15 (yard export); dwell 7 h 45 min.
TR-4102: arrived 2026-11-09 11:20 (yard export); left 2026-11-10 13:30 (G-907); dwell 26 h 10 min, over the threshold. See item 10.
TR-4103: arrived 2026-11-08 16:45 (yard export); dwell 45 h 15 min, over the threshold. See item 11.
TR-4104: arrived 2026-11-10 09:05 (yard export); dwell 4 h 55 min.
TR-4105: arrived 2026-11-10 10:30 (yard export); dwell 3 h 30 min. Gate log G-904 shows 2026-11-10 08:40, which would give 5 h 20 min. See item 6.
TR-4106: arrived 2026-11-10 12:10 (yard export); dwell 1 h 50 min.
TR-4107: arrived 2026-11-10 13:05 (gate log G-906, no yard export row); dwell 0 h 55 min.

Appointments to watch (to 2026-11-11 02:00; the board is stale, so statuses may have moved)
A-71: TR-4101, load LD-2201, inbound, door 4, 2026-11-10 06:30, status in progress. Time has passed and the status is not "completed". See item 12.
A-73: TR-4105, load LD-2205, outbound, door 5, 2026-11-10 11:00, status loading. Time has passed and the status is not "completed". Door differs from the yard export. See items 7 and 13.
A-72: TR-4102, load LD-2202, inbound, door 6, 2026-11-10 15:00, status scheduled. Gate log shows the trailer out. See item 14.
A-74: TR-4106, load LD-2206, inbound, door 2, 2026-11-10 16:30, status scheduled. No flag.

Open dock issues
N-32: door 7, noted 2026-11-10 11:40: "Door 7 seal damaged; draft coming in". Owner not named. See item 1.
N-31: TR-4101, door 4, noted 2026-11-10 10:20: "Dock leveler sticking; unloading slowed". Owner Dock supervisor. See item 2.
N-34: TR-4104, noted 2026-11-10 11:15: "Seal number on the paperwork does not match the trailer". Owner Yard clerk. See item 3.
Closed notes left out: 1 (N-33).

Conflicts and unknowns
1. TR-4102: the yard export lists it on site; gate log G-907 shows it out at 2026-11-10 13:30.
2. TR-4104: location is not recorded and the load state is unknown. Dispatch update U-51 (Dispatch A, 2026-11-10 13:10) gives the location as Yard B-07; the yard export does not. Still open until checked.
3. TR-4105: arrival is 2026-11-10 10:30 in the yard export and 2026-11-10 08:40 in G-904, 110 minutes apart.
4. TR-4105: door is 7 in the yard export and 5 on the appointment board (A-73).
5. TR-4106: load state is loaded in the yard export; dispatch update U-52 (Dispatch A, 2026-11-10 13:20, older than the export) says empty.
6. TR-4107: on site per gate log G-906, with no yard export row.

Follow-up owners
1. Door 7 seal damaged (N-32). Owner: not named. Ask: who owns the repair of the door 7 seal? The incoming lead names an owner.
2. Dock leveler at door 4 (N-31, TR-4101). Owner: Dock supervisor. Ask: is the leveler still slowing unloading?
3. Seal mismatch on TR-4104 (N-34). Owner: Yard clerk. Ask: has the seal number been checked against the trailer?
4. TR-4102 shown on site and out (conflict 1). Owner: Yard control. For dispatch to approve. Ask: is the trailer in the yard or gone?
5. TR-4104 location and load state (conflict 2). Owner: Yard control. Ask: what are the trailer's location and load state?
6. TR-4105 arrival time (conflict 3). Owner: Yard control. Ask: which arrival time is right?
7. TR-4105 door (conflict 4). Owner: Yard control. For dispatch to approve. Ask: is the trailer at door 7 or door 5?
8. TR-4106 load state (conflict 5). Owner: Yard control. Ask: is the trailer loaded or empty?
9. TR-4107 not in the yard export (conflict 6). Owner: Yard control. Ask: where is it parked and what does it carry?
10. TR-4102 dwell 26 h 10 min. Owner: Dock supervision. Ask: is the dwell count to the gate-out time right?
11. TR-4103 dwell 45 h 15 min. Owner: Dock supervision. For dispatch to approve. Ask: what is waiting on this trailer?
12. A-71 time passed, status in progress. Owner: Dispatch. For dispatch to approve. Ask: is the appointment complete?
13. A-73 time passed, status loading. Owner: Dispatch. For dispatch to approve. Ask: is the appointment complete?
14. A-72 booked for a trailer the gate log shows out. Owner: Dispatch. For dispatch to approve. Ask: does the appointment stand?
15. Appointment board is 4 h 30 min old. Owner: Dispatch. Ask: can a fresh export be supplied?

Handover
Verified by the outgoing lead: not yet recorded.
Accepted by the incoming lead: not yet recorded.
Approved by dispatch (items 4, 7, 11, 12, 13, 14): not yet recorded.

Draft for the outgoing lead, the incoming lead and dispatch. No trailer has been moved, no appointment changed, no record updated and nothing sent. Figures are taken from the files supplied for the handover at 2026-11-10 14:00.
```
