# Missed dock window recovery brief: an invented example

*Illustrative example with invented data.* The site, the carrier, the shipment, the times and every statement below are invented. The site is an invented distribution depot, called the Depot here. The carrier is Carrier A. People are referred to by role. The dispatch supervisor asks for the brief at 14:20 on Tuesday 10 November 2026, after a truck has missed its appointment.

The inputs come first, in full, so the template can be run on them. The brief follows.

## The inputs

### 1. Settings (typed by the dispatcher)

```
Shipment: S-4471
Site: the Depot
Now: 2026-11-10 14:20
Dispatch supervisor: not named, use the role
All other settings: use the defaults
```

### 2. Appointment record

```
shipment_ref,carrier,receiver_site,appointment_date,window_start,window_end,receiving_cutoff,appointment_status,fee_terms
S-4471,Carrier A,the Depot,2026-11-10,10:00,11:00,16:00,confirmed,Late-arrival charge may apply after window end. Amount not stated.
```

### 3. Reports

```
shipment_ref,reported_date,reported_time,source_role,stated_eta_date,stated_eta_time,stated_cutoff_time,receiver_accepts_late,statement
S-4471,2026-11-10,09:40,driver,2026-11-10,11:30,,,Traffic on the ring road. Expects 11:30.
S-4471,2026-11-10,11:05,dispatcher,2026-11-10,13:00,,,Driver called in about roadworks. Gave 13:00 as his estimate.
S-4471,2026-11-10,11:20,receiver,,,15:00,no,Nothing is received after 15:00 today. Has not agreed to a late slot.
S-4480,2026-11-10,12:10,dispatcher,2026-11-10,12:45,,,Other load. Running 20 minutes behind.
S-4471,2026-11-10,12:50,driver,2026-11-10,14:45,,yes,Says the dock clerk told him by phone they will take him.
S-4471,2026-11-10,13:30,carrier contact,2026-11-10,15:30,,,Last tracking ping 13:25 about 60 km from the Depot. Planner's ETA 15:30.
```

## The brief

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
1. Arrival time. The latest times differ by 150 minutes against a tolerance of 30: dispatcher 13:00 (passed 80 minutes ago, with no later report from that source), driver 14:45 (reported 90 minutes ago), carrier contact 15:30 (reported 50 minutes ago). Which arrival time is the working one, and does anyone need a fresh position first?
2. Cutoff. The record says 16:00; the receiver said 15:00 at 11:20, 60 minutes earlier. Which cutoff applies, and who confirms it with the receiver?
3. Late arrival. The receiver said it has not agreed to a late slot (11:20); the driver said the dock clerk would take the truck (12:50). Has the receiver accepted a late arrival, and who asks?
4. Appointment. Every latest arrival time falls after the window ended at 11:00, and the appointment is recorded as confirmed with no change. Is a changed appointment to be requested? Any request needs the supervisor's approval and the receiver's agreement; none has been made.
5. After the cutoff. The carrier contact's 15:30 is 30 minutes after the receiver's stated 15:00 cutoff, though before the record's 16:00. If the truck arrives after the cutoff that applies, who decides what happens to the load?
6. Fees. The record says a late-arrival charge may apply and gives no amount. Who owns the fee terms, and is anyone to check them before the truck arrives?

Draft for the dispatch supervisor's decision. Nothing has been sent, booked or changed, no one has been contacted, and no recovery has been chosen. Times are local to the Depot as of 2026-11-10 14:20.
```
