# Bill of lading field check: an invented example

*Illustrative example with invented data.* The forwarder, the shipper, the consignee, the notify party, the carrier, the vessel, the booking, the container and seal numbers, the quantities and every date below are invented. The ports are real places used only as labels. The forwarder is an invented small freight forwarder, called the Forwarder here. Its documentation specialist asks for the check on Tuesday 10 November 2026, when the carrier's draft arrives for one booking of two containers.

The inputs come first, in full, so the template can be run on them. The check follows.

## The inputs

### 1. Settings (typed by the documentation specialist)

```
Business: the Forwarder
Today: 2026-11-10
Documentation specialist: the documentation specialist
All other settings: use the defaults
```

### 2. Draft header

```
field,value
shipper,Shipper A Ltd
consignee,Consignee B GmbH
notify_party,Notify Party C BV
carrier,Carrier D Line
place_of_receipt,Ningbo
port_of_loading,Ningbo
port_of_discharge,Antwerp
place_of_delivery,Rotterdam
vessel_voyage,MV Example Star 042E
freight_terms,as arranged
total_packages,340
total_gross_weight_kg,9180.0
```

### 3. Draft cargo lines

```
line,container_no,seal_no,description,packages,gross_weight_kg
1,ABCU1234567,SL-55001,Steel storage racks,120,4100.0
2,ABCU1234567,SL-55001,Rack fittings,60,820.0
3,DEFU7654321,SL-55002,Steel storage racks,150,4260.0
```

### 4. Booking

```
field,value
booking_reference,BK-20418
shipper,Shipper A Ltd
consignee,Consignee B GmbH
notify_party,Consignee B GmbH
carrier,Carrier D Line
place_of_receipt,Ningbo
port_of_loading,Ningbo
port_of_discharge,Rotterdam
place_of_delivery,Rotterdam
vessel_voyage,MV Example Star 042E
freight_terms,prepaid
container_count,2
```

### 5. Shipper's instructions

```
field,value
shipper,Shipper A Ltd
consignee,Consignee B GmbH
notify_party,Notify Party C BV
freight_terms,prepaid
```

### 6. Packing list

```
line,container_no,seal_no,description,packages,gross_weight_kg
1,ABCU 1234567,SL-55001,Steel storage racks,120,4100.0
2,ABCU 1234567,SL-55001,Rack fittings,60,820.0
3,DEFU7654321,SL-55020,Steel storage racks,150,4300.0
```

## The check

```
BILL OF LADING FIELD CHECK: the Forwarder, booking BK-20418, Tuesday 2026-11-10

For: the documentation specialist. Prepared from: draft header (12 rows), draft cargo lines (3 rows), booking (12 rows), shipper's instructions (4 rows), packing list (3 rows), settings.
Column check: all headers matched.
Settings: weight tolerance 0 kg; freight terms accepted "prepaid, collect". Defaults used: weight tolerance, freight terms words.
Summary: Header fields 10: match 7, different 3, not on draft 0, no source 0. Containers: 2 on the draft, 2 on the packing list, 2 on the booking; 1 with a difference. Totals checked 3: different 2. Differences 7. Open items 2. Questions for the specialist 5.

Data checks
1. Packing list lines 1 and 2 write the container number "ABCU 1234567" with a space; read as ABCU1234567.

Header fields
shipper: draft "Shipper A Ltd"; booking "Shipper A Ltd"; instructions "Shipper A Ltd". MATCH.
consignee: draft "Consignee B GmbH"; booking "Consignee B GmbH"; instructions "Consignee B GmbH". MATCH.
notify_party: draft "Notify Party C BV"; booking "Consignee B GmbH"; instructions "Notify Party C BV". DIFFERENT from the booking. See difference 1 and open item 1.
carrier: draft "Carrier D Line"; booking "Carrier D Line"; instructions not stated. MATCH.
place_of_receipt: draft "Ningbo"; booking "Ningbo"; instructions not stated. MATCH.
port_of_loading: draft "Ningbo"; booking "Ningbo"; instructions not stated. MATCH.
port_of_discharge: draft "Antwerp"; booking "Rotterdam"; instructions not stated. DIFFERENT from the booking. See difference 2.
place_of_delivery: draft "Rotterdam"; booking "Rotterdam"; instructions not stated. MATCH.
vessel_voyage: draft "MV Example Star 042E"; booking "MV Example Star 042E"; instructions not stated. MATCH.
freight_terms: draft "as arranged"; booking "prepaid"; instructions "prepaid". DIFFERENT from the booking and the instructions. See difference 3 and open item 2.

Containers
ABCU1234567: draft lines 1-2; packing list lines 1-2. Seal: draft SL-55001, packing list SL-55001, MATCH. Packages: draft 180, packing list 180, MATCH. Gross weight: draft 4920.0 kg, packing list 4920.0 kg, MATCH. Descriptions: MATCH. No difference.
DEFU7654321: draft line 3; packing list line 3. Seal: draft SL-55002, packing list SL-55020, DIFFERENT. Packages: draft 150, packing list 150, MATCH. Gross weight: draft 4260.0 kg, packing list 4300.0 kg, DIFFERENT (draft 40.0 kg lower). Descriptions: MATCH. See differences 4 and 5.

Totals
Packages: draft total 340; draft lines add to 330; packing list adds to 330. DIFFERENT (draft total 10 higher than its own lines and the packing list). See difference 6.
Gross weight: draft total 9180.0 kg; draft lines add to 9180.0 kg; packing list adds to 9220.0 kg. DIFFERENT (draft total and lines agree; packing list is 40.0 kg higher). See difference 7.
Containers: booking 2; draft 2; packing list 2. MATCH.

Open items
1. notify_party: the booking gives "Consignee B GmbH" and the shipper's instructions give "Notify Party C BV"; the two sources disagree with each other. The draft follows the instructions.
2. freight_terms: the draft's "as arranged" is neither prepaid nor collect.

Differences
1. Header, notify_party: draft "Notify Party C BV"; booking "Consignee B GmbH". The draft agrees with the shipper's instructions.
2. Header, port_of_discharge: draft "Antwerp"; booking "Rotterdam".
3. Header, freight_terms: draft "as arranged"; booking "prepaid"; instructions "prepaid".
4. Container DEFU7654321, seal: draft SL-55002; packing list SL-55020.
5. Container DEFU7654321, gross weight: draft 4260.0 kg; packing list 4300.0 kg; 40.0 kg lower on the draft.
6. Totals, packages: draft total 340; draft lines 330; packing list 330.
7. Totals, gross weight: draft total 9180.0 kg; draft lines 9180.0 kg; packing list 9220.0 kg; 40.0 kg lower on the draft (the same 40.0 kg as difference 5).

Questions for the documentation specialist
1. Notify party. The draft and the shipper's instructions give Notify Party C BV; the booking gives Consignee B GmbH. Which is right?
2. Port of discharge. The draft shows Antwerp; the booking shows Rotterdam, and the place of delivery on both is Rotterdam. Which is right?
3. Freight terms. The draft says "as arranged"; the booking and the instructions say prepaid. Is there a record of the terms outside these files?
4. Container DEFU7654321. The draft seal is SL-55002 and the packing list seal is SL-55020; the draft weight is 4260.0 kg and the packing list weight is 4300.0 kg. Which seal is on the container, and which weight is right?
5. Totals. The draft total of 340 packages is 10 more than its lines and the packing list (330). Its total weight is 40.0 kg lower than the packing list. Is a line missing, or which figures are right?

Draft for the documentation specialist. Nothing has been issued, corrected, sent or changed, and no customs, duty or export-control judgment has been made. Counts are taken from the files supplied on 2026-11-10.
```
