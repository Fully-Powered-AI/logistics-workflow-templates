# Carrier freight invoice check: an invented example

*Illustrative example with invented data.* The company, the carrier, the shipments, the lanes and every charge below are made up. Carrier A is an invented name, not a real carrier. The company is Alder Mill Home Goods, an invented company; roles are used instead of names. The settings are the invented company's: invoice INV-A-9142 from Carrier A, dated 2026-11-02, checked on 2026-11-04 by the freight auditor, run by the freight audit clerk, for the accounts payable lead. Currency is dollars. The tolerance is 0.00, so any difference is listed. The rate confirmation states 120 free waiting minutes.

## What the freight audit clerk supplies

Carrier invoice:

```
invoice,line,shipment_id,carrier,charge_type,amount
INV-A-9142,1,P201,Carrier A,linehaul,640.00
INV-A-9142,2,P201,Carrier A,fuel,96.00
INV-A-9142,3,P202,Carrier A,linehaul,640.00
INV-A-9142,4,P202,Carrier A,fuel,96.00
INV-A-9142,5,P202,Carrier A,linehaul,640.00
INV-A-9142,6,P203,Carrier A,linehaul,545.00
INV-A-9142,7,P203,Carrier A,fuel,78.00
INV-A-9142,8,P204,Carrier A,linehaul,520.00
INV-A-9142,9,P204,Carrier A,fuel,78.00
INV-A-9142,10,P204,Carrier A,detention,150.00
INV-A-9142,11,P205,Carrier A,linehaul,450.00
INV-A-9142,12,P205,Carrier A,fuel,67.50
INV-A-9142,13,P205,Carrier A,liftgate,45.00
INV-A-9142,14,P205,Carrier A,detention,150.00
INV-A-9142,15,P206,Carrier A,linehaul,450.00
INV-A-9142,16,P206,Carrier A,fuel,69.00
INV-A-9142,17,P299,Carrier A,linehaul,380.00
```

Shipment export:

```
shipment_id,carrier,ship_date,lane,delivered_date
P201,Carrier A,2026-10-12,Warehouse to Denver,2026-10-14
P202,Carrier A,2026-10-12,Warehouse to Denver,2026-10-15
P203,Carrier A,2026-10-13,Warehouse to Boise,2026-10-16
P204,Carrier A,2026-10-18,Warehouse to Boise,2026-10-20
P205,Carrier A,2026-10-20,Warehouse to Reno,2026-10-22
P206,Carrier A,2026-10-27,Warehouse to Reno,
```

Rate confirmation:

```
shipment_id,charge_type,confirmed_amount
P201,linehaul,640.00
P201,fuel,96.00
P202,linehaul,640.00
P202,fuel,96.00
P203,linehaul,520.00
P203,fuel,78.00
P204,linehaul,520.00
P204,fuel,78.00
P204,detention,150.00
P205,linehaul,450.00
P205,fuel,67.50
P205,liftgate,45.00
P206,linehaul,450.00
P206,fuel,67.50
```

Delivery and waiting-time records:

```
shipment_id,charge_type,record_type,arrival_time,departure_time,note
P204,detention,waiting,2026-10-20 08:30,2026-10-20 11:45,receiver log bay 3
P205,detention,waiting,2026-10-22 13:05,,driver note with no departure time
```

## What comes out

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
- Line 13, P205, liftgate, billed 45.00: Support missing. Confirmed at 45.00; no record was supplied for this shipment and charge type. In question: 45.00.
- Line 14, P205, detention, billed 150.00: Support missing (incomplete). The waiting record has no departure time. Also not on the rate confirmation. In question: 150.00.
- Line 16, P206, fuel, billed 69.00: Rate difference. Confirmed 67.50; billed 1.50 over. In question: 1.50.
- Line 17, P299, linehaul, billed 380.00: Shipment not found. P299 is not in the shipment export. In question: 380.00.

Matched lines: 1, 2, 3, 4, 7, 8, 9, 10, 11, 12, 15; 11 lines, 3,265.50.

Waiting-time facts
- Line 10, P204, detention billed 150.00: arrived 2026-10-20 08:30, left 2026-10-20 11:45, waited 195 minutes against 120 free minutes supplied: 75 minutes over.
- Line 14, P205, detention billed 150.00: arrived 2026-10-22 13:05, no departure time; minutes waited cannot be worked out.

Decisions for the accounts payable lead (5)
1. Matched lines: lines 1, 2, 3, 4, 7, 8, 9, 10, 11, 12 and 15 match the rate confirmation, 11 lines, 3,265.50. Line 10 is a detention line with 75 minutes over the 120 free minutes supplied, as the waiting-time facts show. Line 15 is on P206, which has no delivery date in the export. Whether to approve payment of these lines once the freight auditor has verified the match.
2. Duplicate: line 5 repeats line 3 (P202, linehaul), 640.00. Whether to dispute, hold or approve this line.
3. Rate difference: line 6 (P203, linehaul) is billed 545.00 against 520.00 confirmed, 25.00 over; line 16 (P206, fuel) is billed 69.00 against 67.50 confirmed, 1.50 over; 26.50 in question. Whether to dispute, hold or approve these lines.
4. Support missing: line 13 (P205, liftgate, 45.00) has no record supplied; line 14 (P205, detention, 150.00) has a waiting record with no departure time and is not on the rate confirmation; 195.00 in question. Whether to dispute, hold or approve these lines.
5. Shipment not found: line 17 (P299, linehaul), 380.00, is on a shipment that is not in the export. Whether to dispute, hold or approve this line.

Not supplied or not checked: earlier invoices were not supplied, so a charge already paid on an earlier invoice would not show as a repeat; the wording of the rate confirmation was not read, only its amounts and the free minutes in the settings; no delivery documents were supplied beyond the records listed.

Every figure traces to invoice INV-A-9142 and the shipment export, rate confirmation and records supplied on 2026-11-04. The check changes no records, contacts no carrier, pays nothing and sends nothing. A match is not authority to pay.
```

## How the figures were reached

The invoice has 17 lines. Line 17 is on P299, which is not in the export, so it is Shipment not found. Line 5 has the same shipment, charge type and amount as line 3, which comes first, so line 5 is the duplicate and line 3 stays in the comparison. Of the others, lines 6 and 16 differ from the confirmed amounts (545.00 against 520.00, and 69.00 against 67.50), giving differences of 25.00 and 1.50. Line 13, a liftgate charge, has no record for P205, and line 14, a detention charge, has a record with no departure time, so both are Support missing; line 14 is also not on the rate confirmation, which the line notes without changing its status. Line 10, detention on P204, has a complete record and matches its confirmed 150.00, so it is matched. The 11 matched lines are 640.00, 96.00, 640.00, 96.00, 78.00, 520.00, 78.00, 150.00, 450.00, 67.50 and 450.00, which add to 3,265.50. The invoice total is 3,265.50 + 640.00 + 614.00 + 195.00 + 380.00 = 5,094.50. The amount in question is 640.00 + 25.00 + 1.50 + 195.00 + 380.00 = 1,241.50, and 5,094.50 less 1,241.50 is 3,853.00. Detention on P204 is 11:45 less 08:30, which is 3 hours 15 minutes, or 195 minutes; 195 less 120 is 75. All 14 confirmed rows appear on the invoice, and all six shipments in the export are billed.
