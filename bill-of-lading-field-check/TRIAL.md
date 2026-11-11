# Bill of lading field check: tried on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in `public/example.md`: an invented forwarder, shipper, consignee, booking and containers. No client data was used. The run followed the instruction block and output format in `member/template.md` exactly, and was made before the example's own output was read. The assistant that ran it had not written the template. The example's output was revised after the run, and the template's wording was clarified on the two points noted below; the output recorded here is exactly what the run produced.

## Inputs used

The six inputs listed in `public/example.md` under "The inputs": the settings, the draft header (12 rows), the draft cargo lines (3 rows), the booking (12 rows), the shipper's instructions (4 rows) and the packing list (3 rows). Nothing was added or changed.

## What came out

```
BILL OF LADING FIELD CHECK: the Forwarder, booking BK-20418, Tuesday 2026-11-10

For: the documentation specialist. Prepared from: draft header (12 rows), draft cargo lines (3 rows), booking (12 rows), shipper's instructions (4 rows), packing list (3 rows), settings.
Column check: all headers matched.
Settings: weight tolerance 0 kg; freight terms accepted "prepaid", "collect". Defaults used: weight tolerance, freight terms words.
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
Packages: draft total 340; draft lines add to 330; packing list adds to 330. DIFFERENT (draft total is 10 higher than its lines and the packing list). See difference 6.
Gross weight: draft total 9180.0 kg; draft lines add to 9180.0 kg; packing list adds to 9220.0 kg. DIFFERENT (draft total and lines agree; packing list is 40.0 kg higher). See difference 7.
Containers: booking 2; draft 2; packing list 2. MATCH.

Open items
1. notify_party: the booking gives "Consignee B GmbH" and the shipper's instructions give "Notify Party C BV"; the two sources disagree. The draft follows the instructions. Not settled from the files.
2. freight_terms: the draft's "as arranged" is neither prepaid nor collect.

Differences
1. Header, notify_party: draft "Notify Party C BV"; booking "Consignee B GmbH".
2. Header, port_of_discharge: draft "Antwerp"; booking "Rotterdam".
3. Header, freight_terms: draft "as arranged"; booking "prepaid"; instructions "prepaid".
4. Container DEFU7654321, seal: draft SL-55002; packing list SL-55020.
5. Container DEFU7654321, gross weight: draft 4260.0 kg; packing list 4300.0 kg; draft 40.0 kg lower.
6. Totals, packages: draft total 340; draft lines 330; packing list 330.
7. Totals, gross weight: draft total 9180.0 kg; draft lines 9180.0 kg; packing list 9220.0 kg; 40.0 kg difference, the same as difference 5.

Questions for the documentation specialist
1. Notify party. The draft and the shipper's instructions give "Notify Party C BV"; the booking gives "Consignee B GmbH". Which is right?
2. Port of discharge. The draft shows Antwerp; the booking shows Rotterdam (the place of delivery on both is Rotterdam). Which is right?
3. Freight terms. The draft says "as arranged"; the booking and the instructions say prepaid. Is there a record of the terms outside these files?
4. Container DEFU7654321. Seal: draft SL-55002, packing list SL-55020. Weight: draft 4260.0 kg, packing list 4300.0 kg. Which seal and which weight are right?
5. Totals. The draft's package total (340) is 10 above its lines and the packing list (330). Its weight total (9180.0 kg) equals its own lines but is 40.0 kg below the packing list (9220.0 kg). Is a line missing, or which figures are right?

Draft for the documentation specialist. Nothing has been issued, corrected, sent or changed, and no customs, duty or export-control judgment has been made. Counts are taken from the files supplied on 2026-11-10.
```

## What was observed

- Every required part was produced: the header, ten header lines, a Containers entry for each of the two containers, three Totals lines, and the four numbered lists. Nothing in the run made the assistant stop. The headers matched, no row failed the row check, and the booking and packing list were present.
- Compared with the published example output, the findings were the same: 7 matches and 3 differences in the header, one container with a difference, two totals differing, 7 differences, 2 open items and 5 questions. The numbers, values and files named in each finding agreed.
- The differences in wording were small. At the time of the run, the example's wording differed from this run's in small ways: it printed "0.0 kg" for the tolerance, named the default "freight terms", and asked whether the totals should be "corrected to the lines" and whether the booking record needed correcting, which come close to recommending an action. This run asked which figures are right, to follow the rule that questions recommend nothing. The example was revised after the run and no longer differs on these points, apart from the list of freight terms words, which the example prints as "prepaid, collect" and this run printed as `"prepaid", "collect"`.
- Every fact in the output is in the inputs. The weekday, Tuesday, is worked out from the date, and the example also gives it.
- Where the instructions left room to guess:
  - The Settings line has no rule for how to print the tolerance (0 or 0.0) or the list of freight terms words, so two runs can differ in wording.
  - It does not say how to name defaults on the "Defaults used" line when a setting has two parts (the freight terms words). This run named the setting as the template does ("freight terms words"); the template now says to use those names.
  - The Data checks rule says to list a spaced container number "once for each file where it happens", but not whether to name the lines. This run named them; the template now says to name the lines.
  - Sums were printed to one decimal place because the inputs use one. The template does not set a number format.
  - A draft that agrees with one of two disagreeing sources is called DIFFERENT only from the other source. This follows step 4, but a reader may expect the open item to be the main finding.
- Nothing in the template was wrong or contradictory in this run. It was tried once on one example that contains one case of each kind of finding. It has not been run on a missing weight, a wrong-shaped container number, a stop condition or a refusal, and it has not been tried in any other AI product.
