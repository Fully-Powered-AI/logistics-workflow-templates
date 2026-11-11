# Freight shortage record packet: an invented example

*Illustrative example with invented data.* The business, the customer, the item codes, the document numbers, the quantities and every date below are invented. The business is an invented regional distributor, called the Distributor here. On the morning of Tuesday 10 November 2026 its claims coordinator asks for the packet on one delivered shipment, SH-2210, after the receiving lead at Customer A reported a shortage and damage on the day after delivery. People are referred to by role.

The inputs come first, in full, so the template can be run on them. The packet follows.

## The inputs

### 1. Settings (typed by the claims coordinator)

```
Company: the Distributor
Today: 2026-11-10
Claims coordinator: the claims coordinator
All other settings: use the defaults
```

### 2. Customer report

```
report_id,shipment_ref,item_code,issue,qty_affected,unit,reported_date,reported_by,note
R-1,SH-2210,CHR-110,short,6,each,2026-11-06,Customer A receiving lead,Six chairs missing from pallet
R-2,SH-2210,TBL-220,damaged,2,each,2026-11-06,Customer A receiving lead,Two table tops damaged
```

### 3. Dispatch lines

```
shipment_ref,line,item_code,description,qty_dispatched,unit,dispatch_date
SH-2210,1,CHR-110,Folding chair,40,each,2026-11-03
SH-2210,2,TBL-220,Trestle table,12,each,2026-11-03
SH-2210,3,CRT-330,Storage crate,60,each,2026-11-03
```

### 4. Warehouse scans

```
scan_id,shipment_ref,item_code,event,qty,scan_time,location
S-01,SH-2210,CHR-110,picked,25,2026-11-03 07:40,Aisle 4
S-02,SH-2210,CHR-110,picked,15,2026-11-03 07:52,Aisle 4
S-03,SH-2210,CHR-110,loaded,40,2026-11-03 09:10,Dock 2
S-04,SH-2210,TBL-220,picked,12,2026-11-03 08:05,Aisle 9
S-05,SH-2210,TBL-220,loaded,12,2026-11-03 09:12,Dock 2
S-06,SH-2210,CRT-330,picked,60,2026-11-03 08:20,Aisle 2
```

### 5. Bill of lading

```
bol_number,shipment_ref,item_code,qty_stated,unit,remark
BOL-9051,SH-2210,CHR-110,40,each,Shipper load and count
BOL-9051,SH-2210,TBL-220,12,each,Shipper load and count
BOL-9051,SH-2210,CRT-330,54,each,Shipper load and count
```

### 6. Proof of delivery

```
pod_id,shipment_ref,item_code,qty_signed,unit,delivery_date,signed,exception_note
POD-77,SH-2210,CHR-110,34,each,2026-11-05,yes,6 chairs not on pallet
POD-77,SH-2210,TBL-220,12,each,2026-11-05,yes,
POD-77,SH-2210,CRT-330,54,each,2026-11-05,yes,
```

### 7. Photo log

```
photo_id,shipment_ref,item_code,taken_date,taken_by,caption
PH-1,SH-2210,TBL-220,2026-11-06,Customer A receiving,Table top corner chipped
PH-2,SH-2210,TBL-220,2026-11-06,Customer A receiving,Second table top cracked edge
PH-3,SH-2210,,2026-11-06,Customer A receiving,Pallet wrapping torn on one side
```

## The packet

```
FREIGHT SHORTAGE RECORD PACKET: the Distributor, shipment SH-2210, Tuesday 2026-11-10

For: the claims coordinator. Prepared from: customer report (2 rows), dispatch lines (3 rows), warehouse scans (6 rows), bill of lading (3 rows), proof of delivery (3 rows), photo log (3 rows), settings.
Column check: all headers matched.
Settings: quantity tolerance 0 units; issue words "short" and "damaged"; scan words "picked" and "loaded"; signed word "yes". Defaults used: all.
Summary: Reported lines 2 (short 1, damaged 1, other 0). Reports for the whole shipment 0. Other lines: 1 with a missing record, conflicting figure or unit difference, 0 agreeing at every stage. Missing records 1. Conflicting figures 3, on 2 lines. Photos 3: 2 tied to a line, 1 not. Questions 3.

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
1. CRT-330, line 3: no loaded scan (60 picked, S-06).

Conflicting figures
1. CHR-110, line 1: proof of delivery signed 34 (POD-77); dispatched 40 (line 1); 6 fewer.
2. CRT-330, line 3: bill of lading states 54 (BOL-9051); dispatched 60 (line 3); 6 fewer.
3. CRT-330, line 3: proof of delivery signed 54 (POD-77); dispatched 60 (line 3); 6 fewer.

Questions for the claims coordinator
1. CHR-110, report R-1 (short 6). Dispatch line 1, the picked scans S-01 and S-02 (together 40), the loaded scan S-03 and BOL-9051 all show 40. POD-77 shows 34 signed, with the remark "6 chairs not on pallet". Who wrote that remark, and when? Is there another record of the count, at pickup or at delivery, outside the files supplied?
2. TBL-220, report R-2 (damaged 2). Every stage shows 12 and POD-77 has no remark for this line. PH-1 and PH-2 are tied to this line and dated 2026-11-06, 1 day after delivery. Is there any record of the freight's condition at delivery other than POD-77? Does PH-3 belong with this line? Are the original images available?
3. CRT-330, not reported. Dispatched 60 and picked 60 (S-06); no loaded scan; BOL-9051 states 54 and POD-77 shows 54 signed. Is a loaded scan for this line recorded elsewhere? Is the 54 on BOL-9051 a count taken from the load or an entry difference? Is the 6-unit difference known to the customer?

Draft for the claims coordinator. Nothing has been sent, filed, changed or decided, no fault or liability has been assigned, and no claim position has been taken. Counts are taken from the files supplied on 2026-11-10.
```
