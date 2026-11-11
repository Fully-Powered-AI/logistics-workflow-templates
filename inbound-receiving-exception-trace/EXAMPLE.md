# Inbound receiving exception trace: an invented example

*Illustrative example with invented data.* The business, the supplier, the item codes, the lot numbers, the pallets, the quantities and every date below are invented. The business is an invented small distributor of garden and hardware goods, called the Depot here. On the morning of Tuesday 10 November 2026 a delivery from Supplier A has been unloaded and scanned, and the receiving supervisor sees that the counts do not match the advance shipment notice. People are referred to by role.

The inputs come first, in full, so the template can be run on them. The trace follows.

## The inputs

### 1. Settings (typed by the receiving clerk)

```
Business: the Depot
Receiving date: 2026-11-10
Receiving supervisor: the receiving supervisor
Inventory controller: the inventory controller
All other settings: use the defaults
```

### 2. Advance shipment notice

```
asn_number,line,sku,lot,qty_expected,unit
ASN-4410,1,HT-100,,240,each
ASN-4410,2,GL-210,,500,pair
ASN-4410,3,PT-330,B2611,576,each
ASN-4410,4,SD-450,,400,each
ASN-4410,5,WH-520,,80,each
ASN-4410,6,TP-640,,150,each
```

### 3. Packing list

```
packing_list_number,sku,lot,qty_packed,unit
PL-8830,HT-100,,240,each
PL-8830,GL-210,,500,pair
PL-8830,PT-330,B2611,576,each
PL-8830,SD-450,,420,each
PL-8830,WH-520,W-77,80,each
PL-8830,TP-640,,150,each
```

### 4. Receiving scan export (this delivery only)

```
scan_id,scan_time,pallet_id,sku,lot,qty_scanned,unit
S-001,2026-11-10 08:05,PAL-01,HT-100,,19,carton
S-002,2026-11-10 08:12,PAL-02,GL-210,,250,pair
S-002,2026-11-10 08:12,PAL-02,GL-210,,250,pair
S-003,2026-11-10 08:20,PAL-03,GL-210,,250,pair
S-004,2026-11-10 08:31,PAL-04,PT-330,B2611,288,each
S-005,2026-11-10 08:40,PAL-05,PT-330,B2611,144,each
S-006,2026-11-10 08:41,PAL-05,PT-330,B2612,144,each
S-007,2026-11-10 08:55,PAL-06,SD-450,,420,each
S-008,2026-11-10 09:02,PAL-07,WH-520,W-77,80,each
S-009,2026-11-10 09:10,PAL-08,TP-640,,10,bundle
S-010,2026-11-10 09:15,PAL-09,XK-999,,12,each
```

### 5. Item master

```
sku,description,base_unit,units_per_carton,units_per_pallet,lot_controlled
HT-100,Hand trowel,each,12,,no
GL-210,Work gloves,pair,10,,no
PT-330,Plant food 1 kg,each,6,288,yes
SD-450,Seed tray,each,20,,no
WH-520,Garden hose 15 m,each,4,,yes
TP-640,Tomato cage,each,,,no
```

## The trace

```
INBOUND RECEIVING EXCEPTION TRACE: the Depot, notice ASN-4410, Tuesday 2026-11-10

For: the receiving supervisor and the inventory controller. Prepared from: notice (6 rows), packing list (6 rows), scan export (11 rows), item master (6 rows), settings.
Column check: all headers matched.
Settings: quantity tolerance 0 base units. Defaults used: quantity tolerance, unit words.
Summary: 8 comparison lines: agree 1, differ 4, not on the notice 2, not scanned 0, not compared 1. Missing references 3. Data checks 3. Questions 7, on 7 items.

Data checks
1. Scan id S-002 appears twice (PAL-02, GL-210, 250 pair, 2026-11-10 08:12). Both rows are counted in the scanned total; line 2 also shows the total with the repeated row set aside. Nothing was removed.
2. Scan S-009 (PAL-08, TP-640) is in "bundle". The item master gives no bundle size and "bundle" is not a unit word. The row was not converted and line 6 is not compared.
3. Pallet PAL-05 shows two lots of PT-330: B2611, 144 (S-005) and B2612, 144 (S-006). The lots are used as scanned.

Comparison (quantities in base units)
1. HT-100 Hand trowel (notice line 1): notice 240; packing list 240; scanned 228 (S-001, 19 cartons × 12 = 228). Differs: scanned 12 fewer than the notice; packing list agrees with the notice. Notice and packing list agree; the difference is on the receiving side. See question 1.
2. GL-210 Work gloves (notice line 2): notice 500; packing list 500; scanned 750 (S-002 twice, S-003). Differs: scanned 250 more than the notice; packing list agrees with the notice. Notice and packing list agree; the difference is on the receiving side. Scanned 500 with the repeated S-002 row set aside. See question 2.
3. PT-330 Plant food 1 kg, lot B2611 (notice line 3): notice 576; packing list 576; scanned 432 (S-004 288, S-005 144). Differs: scanned 144 fewer than the notice; packing list agrees with the notice. Notice and packing list agree; the difference is on the receiving side. Pairs with line 7: the same quantity under another lot. See question 3.
4. SD-450 Seed tray (notice line 4): notice 400; packing list 420; scanned 420 (S-007). Differs: scanned 20 more than the notice; packing list 20 more than the notice. Scans match the packing list, not the notice. See question 4.
5. WH-520 Garden hose 15 m, compared as a whole item because the notice has no lot (notice line 5): notice 80; packing list 80; scanned 80 (S-008). Agrees. See question 5.
6. TP-640 Tomato cage (notice line 6): notice 150; packing list 150; scanned not converted (S-009, 10 bundle). Not compared, unit unknown. See question 6.
7. PT-330 Plant food 1 kg, lot B2612 (not on the notice): notice none; packing list none; scanned 144 (S-006). Not on the notice. Pairs with line 3: the same quantity under another lot. See question 3.
8. XK-999 (not in the item master) (not on the notice): notice none; packing list none; scanned 12 (S-010, "each" as written). Not on the notice. See question 7.

Missing references
1. WH-520, notice line 5: no lot on the notice, and the item master marks the item as lot-controlled. The packing list and the scan S-008 show lot W-77.
2. PT-330, lot B2612: scanned (S-006) with no notice line and no packing list line.
3. XK-999: scanned (S-010) with no notice line, no packing list line and no entry in the item master.

Questions for the receiving supervisor and the inventory controller
1. HT-100 Hand trowel. The notice and the packing list both say 240; the scan S-001 on PAL-01 gives 19 cartons of 12, which is 228, 12 fewer than 240 and one carton fewer. Does a count on the dock show 19 or 20 cartons on PAL-01? Is a carton of this item still elsewhere, unscanned?
2. GL-210 Work gloves. The notice and the packing list both say 500 pair; the export holds 750, because scan id S-002 (PAL-02, 250 pair) appears twice. With one S-002 row the total is 500. Was PAL-02 scanned twice, or do two different pallets share the scan id? Does a count on the dock of PAL-02 and PAL-03 show 500 pair?
3. PT-330 Plant food 1 kg. The notice and the packing list say 576 of lot B2611; the scans give 432 of B2611 and 144 of lot B2612, which is on neither document. PAL-05 shows both lots (S-005, S-006). What lot does the label on PAL-05 show, and does the pallet physically hold both? Which lot is printed on the units scanned in S-006?
4. SD-450 Seed tray. The notice says 400; the packing list says 420; the scan S-007 on PAL-06 says 420. Is there a revised notice? Does a count on the dock of PAL-06 show 420?
5. WH-520 Garden hose 15 m. The notice has no lot, the item is lot-controlled, and the packing list and the scan show W-77; the quantities all agree at 80. Is W-77 the lot the supplier meant for notice line 5?
6. TP-640 Tomato cage. The notice and the packing list say 150; the scan S-009 on PAL-08 gives 10 bundle. How many of this item are in a bundle, and does the count on the dock of PAL-08 agree with the notice and the packing list? Is "bundle" a unit the item master should hold?
7. XK-999. The scan S-010 on PAL-09 shows 12 of a code that is on no notice line, no packing list line and not in the item master. What code is printed on the carton labels of PAL-09? Is it a mistyped code for an item on the notice?

Draft for the receiving supervisor and the inventory controller. Nothing has been adjusted, corrected, sent or changed, no supplier has been contacted and no fault has been assigned. Counts are taken from the files supplied on 2026-11-10.
```
