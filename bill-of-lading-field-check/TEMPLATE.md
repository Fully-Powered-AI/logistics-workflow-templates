# Bill of lading field check

Workflow template, version 0.1.0.

## Purpose

Prepare the check a documentation specialist makes when a draft bill of lading arrives and before it is issued. The draft's party, routing and freight-terms fields are compared with the booking and the shipper's instructions, each container's packages, gross weight and seal are compared with the packing list, and the draft's own totals are added up and compared. Every difference is marked, every point the files cannot settle is listed as an open item, and each point that needs a decision becomes a numbered question for the specialist. Every finding traces to a row in a supplied file. The assistant prepares; it never issues, amends or approves a bill of lading, contacts a carrier, agent or shipper, changes a record, decides which source is right, or makes any customs classification, duty or export-control determination.

## When to use it and when not to

Use it when a draft bill of lading has arrived and its booking, the shipper's instructions and the packing list are to hand, before the document is approved for issue. Run it again on each new draft after corrections are requested.

Do not use it:

- to check a finished order's certificates, inspection records and packing, which is the shipment documentation check;
- to review supplier bills or prepare a payment run, which is the supplier bill review and payment run preparation;
- to judge how a carrier has performed, which is the carrier performance review;
- to classify goods, work out duty or decide whether an export is allowed. Commodity and tariff codes are not read or compared here;
- to decide which of two disagreeing sources is correct. The specialist and the shipper decide;
- to check more than one bill of lading at a time. One run covers one draft and its booking.

## Roles

- **Runs it:** the documentation specialist, or a coordinator working for them.
- **Confirms which corrections to request:** the documentation specialist. Always a person.
- **Supplies the approved instructions:** the shipper.
- **Issues the bill of lading:** the authorized carrier or agent. The assistant never does.
- **Owns each source document:** the role that keeps it. The assistant corrects and replaces none.

## Inputs

The assistant works only from the files the person supplies. It needs no connection to any system and never asks for a password or a login code. Dates are written YYYY-MM-DD. The settings may give today's date in words; the assistant reads it as that date and writes it as YYYY-MM-DD. One run covers one draft.

1. **The draft header.** One row per field. Default column headers: `field`, `value`. Recognised fields: `shipper`, `consignee`, `notify_party`, `carrier`, `place_of_receipt`, `port_of_loading`, `port_of_discharge`, `place_of_delivery`, `vessel_voyage`, `freight_terms`, `total_packages`, `total_gross_weight_kg`.
2. **The draft cargo lines.** One row per line. Default column headers: `line`, `container_no`, `seal_no`, `description`, `packages`, `gross_weight_kg`. Weights are in kilograms.
3. **The booking.** One row per field. Default column headers: `field`, `value`. Recognised fields: `booking_reference`, `container_count`, and the ten party, routing and freight-terms fields listed for the draft header (from `shipper` to `freight_terms`).
4. **The shipper's instructions.** One row per field. Default column headers: `field`, `value`. It uses the same ten party, routing and freight-terms field names, and any of them may be left out. A field that is left out is "not stated".
5. **The packing list.** One row per line. Default column headers: `line`, `container_no`, `seal_no`, `description`, `packages`, `gross_weight_kg`.
6. **The settings,** typed: the business; today's date; the documentation specialist, by name or role; and, when they differ from the defaults, the weight tolerance and the freight terms words. Defaults:
   - weight tolerance: 0 kg. A weight is a difference when the two figures are further apart than this;
   - freight terms words: `prepaid` and `collect`. A draft value that is neither is an open item.

   The Settings line names, after "Defaults used", each setting that came from a default, by the names above: `weight tolerance`, `freight terms words`.

**Column check.** Before anything else, compare each file's headers with the defaults, or with the business's own headers, if it has set them. If a header is missing or named differently, stop. List, for each file, the headers expected and the headers found, ask which column is which, and prepare nothing else. Never guess a column.

**How values are compared.** Capitals, repeated spaces and a full stop, comma or semicolon at the end of a value are ignored. In a container number, spaces and hyphens are ignored too and letters are read as capitals; in a seal number, spaces are ignored and letters are read as capitals. Anything else is compared exactly: "Ltd" and "Limited" are different, and so are two port names spelled differently. The specialist decides whether a difference in wording matters.

## The procedure

1. **Check the columns,** as above.
2. **Check the rows.** Stop, list every problem row, ask, and prepare nothing else when: a field name appears twice in one header or field file; a `line` is blank or appears twice in one cargo file; a `container_no` is blank on a cargo row; a `packages`, `gross_weight_kg`, `total_packages`, `total_gross_weight_kg` or `container_count` that is filled in is negative or not a number, or a package count is not a whole number. A blank package count or weight is allowed and becomes an open item.
3. **Run the data checks.** These do not stop the work. List each under Data checks and say what was done:
   - a field name in a header or field file that is not recognised is left out and listed;
   - a column in a cargo file beyond the defaults, such as a commodity or tariff code, is not read and is listed as "not read";
   - a container number or seal number written with spaces, hyphens or different capitals is read as the comparison rules say, and listed once for each file where it happens, naming the lines.
4. **Compare each header field.** For the ten fields from `shipper` to `freight_terms`, take the draft's value, the booking's value and the instructions' value. Give one result:
   - **MATCH:** the draft's value equals every source that states the field, and the draft states it;
   - **DIFFERENT:** the draft's value differs from at least one source that states the field; name each source it differs from;
   - **NOT ON DRAFT:** the draft has no value and at least one source states one;
   - **NO SOURCE:** neither source states the field, whether the draft states a value or is blank. List it as an open item.
   Print the fields in the order shipper, consignee, notify_party, carrier, place_of_receipt, port_of_loading, port_of_discharge, place_of_delivery, vessel_voyage, freight_terms. Where the booking and the instructions both state a field and differ from each other, list it as an open item whatever the draft says, naming both values. Do not choose between them.
5. **Check the freight terms.** If the draft's `freight_terms` is blank, or not one of the freight terms words after the comparison rules are applied, list it as an open item with the value as written. If the sources state terms and the draft differs, it is also a difference in step 4.
6. **Compare each container with the packing list.** Group the draft's cargo lines and the packing list's lines by container number. Take the draft's containers in the order they first appear, then any container found only in the packing list. For each container:
   - **Seal:** the set of seal numbers given on its lines in each file. A difference when the sets differ. If either file gives no seal for the container, do not compare; list "seal not stated in [file]" as an open item;
   - **Packages:** the sum over its lines in each file. A difference when the sums differ. If any line in either file has a blank package count, do not compare; list it as an open item naming the line;
   - **Gross weight:** the sum over its lines in each file. A difference when the sums are further apart than the weight tolerance; state by how much and which file is lower. If any line has a blank weight, do not compare; list "missing weight" as an open item naming the line, and never treat a blank as zero;
   - **Descriptions:** the set of descriptions on its lines in each file. A difference when the sets differ;
   - a container on the draft and not on the packing list, or on the packing list and not on the draft, is a difference by itself, and its other figures are shown but not compared.
7. **Check the container numbers.** A container number that is not four letters followed by seven digits, after the comparison rules, is listed as an open item. Do not check the digits further.
8. **Check the totals.** Three checks, in this order:
   - packages: the draft's `total_packages`, the sum of the draft's lines and the sum of the packing list. A difference when the three are not equal;
   - gross weight: the draft's `total_gross_weight_kg`, the sum of the draft's lines and the sum of the packing list. A difference when any two are further apart than the weight tolerance. State which figures agree and by how much the others differ;
   - containers: the booking's `container_count`, the number of containers on the draft and the number on the packing list. A difference when the three are not equal.
   If a total is blank in the draft, say so and compare the other two. If a sum cannot be formed because a line has a blank figure, do not compare it and say why.
9. **List the open items,** numbered: source conflicts (step 4), freight terms (step 5), fields stated by no source, seals, package counts and weights that are missing, and container numbers of the wrong shape. An item may also appear among the differences; each list is counted on its own.
10. **List the differences,** numbered, each stated once: header fields in field order, then containers in the order of step 6 (seal, packages, weight, description, containers on one side only), then the totals in the order of step 8. Each names the values and the file each comes from. A difference that follows from another, such as a total that moves because a container weight differs, is listed and says which difference it repeats.
11. **Write the questions.** One numbered question or group of questions for each header field with a difference or open item, each container with a difference or open item, and the totals, in the order the findings appear. Give the values and the files, then ask only what the facts raise: which value is right, whether a record exists outside the files, whether a line is missing. Recommend nothing and never say a draft is ready or must be sent back.
12. **Write the header and summary.** Give the weekday of today's date. Count the header fields by result; the containers on the draft, the packing list and the booking, and those with a difference; the totals checked and those that differ; the differences; the open items; and the questions.
13. **Return the draft** to the person who ran it. A person decides each action and takes it.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **A row fails the checks in step 2:** stop; list the rows; prepare nothing else.
- **The booking or the packing list is missing:** stop. The check needs both. A missing shipper's instructions file is allowed: every field is then "not stated" there.
- **A file holds more than one booking or more than one bill of lading:** stop and ask for one at a time.
- **Only a document's title is known, or a file could not be read:** the check covers the fields in the files. Do not describe what an unseen document says.
- **Asked to say the draft is correct or ready to issue, to issue, approve or amend it, or to tell the carrier or agent anything:** decline. Say the documentation specialist decides and the authorized carrier or agent issues.
- **Asked to pick the correct value when sources disagree, or to change a value so the files agree:** decline; list the values and ask the specialist.
- **Asked for a customs classification, a duty amount, an export licence or sanctions judgment, or whether goods may be shipped:** decline. Those belong to the people the business names, such as its broker.
- **The files contain a password, a login code, card numbers or bank details:** do not repeat them; tell the person to remove them from the source.

## Output format

```
BILL OF LADING FIELD CHECK: [business], booking [booking_reference], [weekday] [YYYY-MM-DD]

For: [documentation specialist]. Prepared from: draft header ([n] rows), draft cargo lines ([n] rows), booking ([n] rows), shipper's instructions ([n] rows), packing list ([n] rows), settings.
Column check: all headers matched. / Stopped: [file]: expected [headers]; found [headers].
Settings: weight tolerance [n] kg; freight terms accepted "[words]". Defaults used: [settings taken from a default / none].
Summary: Header fields 10: match [n], different [n], not on draft [n], no source [n]. Containers: [n] on the draft, [n] on the packing list, [n] on the booking; [n] with a difference. Totals checked 3: different [n]. Differences [n]. Open items [n]. Questions for the specialist [n].

Data checks
[n]. [Finding; what was done.]
/ No problems found.

Header fields
[field]: draft "[value]"; booking "[value]" / not stated; instructions "[value]" / not stated. MATCH. / DIFFERENT from the [booking / instructions / booking and the instructions]. See difference [n][ and open item [n]]. / NOT ON DRAFT. / NO SOURCE. See open item [n].
(ten lines, in the order shipper, consignee, notify_party, carrier, place_of_receipt, port_of_loading, port_of_discharge, place_of_delivery, vessel_voyage, freight_terms)

Containers
[Container number]: draft lines [n-n]; packing list lines [n-n]. Seal: draft [seal], packing list [seal], MATCH / DIFFERENT. Packages: draft [n], packing list [n], MATCH / DIFFERENT. Gross weight: draft [n] kg, packing list [n] kg, MATCH / DIFFERENT ([draft / packing list] [n] kg lower). Descriptions: MATCH / DIFFERENT. No difference. / See difference [n][ and [n]].
[A not-compared figure: "Seal: not compared, see open item [n]." in place of the comparison.]
/ None.

Totals
Packages: draft total [n]; draft lines add to [n]; packing list adds to [n]. MATCH / DIFFERENT ([how]). See difference [n].
Gross weight: draft total [n] kg; draft lines add to [n] kg; packing list adds to [n] kg. MATCH / DIFFERENT ([how]). See difference [n].
Containers: booking [n]; draft [n]; packing list [n]. MATCH / DIFFERENT. See difference [n].

Open items
[n]. [Field, container or total; what the files give; why it cannot be settled from them.]
/ None.

Differences
[n]. [Where; the value in each file; by how much.]
/ None.

Questions for the documentation specialist
[n]. [The facts, with the files; one to three questions.]
/ None.

Draft for the documentation specialist. Nothing has been issued, corrected, sent or changed, and no customs, duty or export-control judgment has been made. Counts are taken from the files supplied on [YYYY-MM-DD].
```

Print the weight tolerance as a plain number, as set or the default (0), and each sum with the decimal places the files use. Print one Containers entry for every container. Print all ten Header fields lines and all three Totals lines whether or not they differ. If the work stops, print the header lines that are known, the reason on the Column check line or under Data checks, and the closing line, and leave out the other sections.

## Reviewer checklist

1. Every header matched, or the work stopped. (Documentation specialist)
2. Each of the ten header fields appears once, with the right value from each file. (Documentation specialist)
3. Every container and every line on the draft and the packing list is accounted for, and each sum can be rebuilt from the files. (Documentation specialist)
4. Where the booking and the instructions disagree, the open item names both and chooses neither. (Documentation specialist)
5. Nothing says or implies that the draft is correct, ready to issue or should be returned, and nothing is said about classification, duty or export control. (Documentation specialist)
6. Each question states values and files and recommends nothing. (Documentation specialist)
7. No blank weight or count has been treated as zero. (Documentation specialist)

## Acceptance tests

Proposed tests. None has been run.

1. **Clean draft.** Every field matches; containers and totals agree. Expected: every line MATCH, "None." under Open items, Differences and Questions.
2. **Renamed column.** The packing list has `weight` instead of `gross_weight_kg`. Expected: stops; lists expected and found headers.
3. **No packing list.** Expected: stops.
4. **Wording difference.** Draft "Shipper A Limited", booking "Shipper A Ltd". Expected: DIFFERENT; no judgment about whether it matters.
5. **Sources disagree.** Booking and instructions give different notify parties. Expected: an open item naming both; nothing chosen.
6. **Vague freight terms.** Draft "as arranged". Expected: an open item and a difference if a source states terms.
7. **Seal transposed.** Draft SL-55002, packing list SL-55020. Expected: seal DIFFERENT.
8. **Weight within tolerance.** A 2 kg difference with a tolerance of 5. Expected: MATCH.
9. **Weight beyond tolerance.** Expected: DIFFERENT with the amount and which file is lower.
10. **Missing weight.** A blank weight on a packing list line. Expected: an open item; no weight comparison for that container; never zero.
11. **Container number with a space.** Expected: read as one number and listed under Data checks.
12. **Container on one side only.** Expected: a difference by itself.
13. **Draft total disagrees with its own lines.** Expected: totals DIFFERENT, with both figures.
14. **Two bills in one file.** Expected: stops.
15. **Asked whether it is ready to issue.** Expected: declines; the specialist decides.
16. **Asked for the right value.** Expected: declines; lists the values.
17. **Asked for a tariff code or an export decision.** Expected: declines.
18. **Unrecognised field.** Expected: left out and listed under Data checks.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above. The block's ten steps fold the procedure's thirteen: block steps 1 to 5 are procedure steps 1 to 5, block step 6 is procedure steps 6 and 7 (the container-number shape check is the last sentence), block step 7 is procedure step 8, block step 8 is procedure steps 9 and 10, block step 9 is procedure step 11 and block step 10 is procedure steps 12 and 13.

```
You prepare the bill of lading field check for one draft bill of lading
before it is issued: a comparison of its party, routing and
freight-terms fields with the booking and the shipper's instructions,
of each container's packages, gross weight and seal with the packing
list, and of its own totals, with every difference marked and every
open point listed. You prepare; people decide. You never issue, amend
or approve a bill of lading, contact a carrier, agent or shipper,
change any record, choose between sources that disagree, or make any
customs classification, duty or export-control determination. Anything
that sends, posts, pays or changes a record waits for a person's
approval. You need no access to any system and never ask for a password
or a login code.

Inputs: draft header (field, value; shipper, consignee, notify_party,
carrier, place_of_receipt, port_of_loading, port_of_discharge,
place_of_delivery, vessel_voyage, freight_terms, total_packages,
total_gross_weight_kg); draft cargo lines (line, container_no, seal_no,
description, packages, gross_weight_kg); booking (field, value; the ten
fields from shipper to freight_terms, booking_reference,
container_count); shipper's instructions (field, value; any of the ten
fields, a missing field is "not stated"); packing list (same columns as
the cargo lines); settings (business, today, documentation specialist,
weight tolerance default 0 kg, freight terms words default prepaid and
collect). Dates are YYYY-MM-DD. Name, after "Defaults used", each
setting taken from a default, as "weight tolerance" or "freight terms
words", or say none. Ignore capitals, repeated
spaces and a closing full stop, comma or semicolon; in container
numbers also ignore spaces and hyphens; in seal numbers also ignore
spaces. Everything else is compared exactly.

1. Column check: compare every header with the list above, or with the
   business's own headers if given. If any is missing or named
   differently, stop, list expected and found headers, ask, and prepare
   nothing else.
2. Row check: stop, list the rows, ask, and prepare nothing else if a
   field name repeats in one field file; a line is blank or repeated in
   a cargo file; a container_no is blank; or a filled-in count, weight
   or total is negative or not a number (counts must be whole). A blank
   count or weight is allowed and becomes an open item. Stop if the
   booking or the packing list is missing, or a file holds more than one
   booking or bill.
3. Data checks (do not stop): list and leave out unrecognised field
   names; list extra columns as not read; list, once for each file,
   the lines where a container or seal number needed the comparison
   rules.
4. For each of the ten fields from shipper to freight_terms, give one
   result: MATCH (draft equals every source that states it);
   DIFFERENT (draft differs from at least one source; name each);
   NOT ON DRAFT (draft blank, a source states it); NO SOURCE (no source
   states it, whether the draft does or is blank; open item). Where booking and
   instructions both state a field and differ, list an open item
   naming both values; choose neither.
5. A draft freight_terms that is blank or not one of the freight terms
   words is an open item, with the value as written.
6. Group draft and packing list lines by container number. For each
   container compare the seal sets, the package sums, the gross weight
   sums (a difference only beyond the tolerance; say how much and which
   file is lower) and the description sets. Never treat a blank count,
   weight or seal as zero: do not compare that figure, and list it as an
   open item naming the line. A container on one side only is a
   difference. A container number that is not four letters then seven
   digits is an open item.
7. Totals: packages (draft total, draft lines, packing list); gross
   weight (draft total, draft lines, packing list); containers (booking
   count, draft, packing list). Show all three figures each time. A
   total is DIFFERENT when its three figures are not equal; for weight,
   when any two are further apart than the tolerance. Say which figures
   agree and by how much the others differ.
8. Open items numbered; differences numbered, once each, in the order:
   header fields, containers (seal, packages, weight, descriptions,
   one-sided containers), totals. A difference that follows from another
   says which it repeats. An item may be in both lists.
9. One numbered question or group of questions for each field,
   container or total with a difference or open item: the values and
   the files, then one to three questions on which value is right or
   whether a record exists elsewhere. Recommend nothing. Never say the
   draft is ready, correct, or should be returned.
10. Use the output format exactly, including the weekday of today's
   date. Print all ten header fields and all three totals, one entry
   for every container, and "None." under an empty section.

If a document is known only by its title, do not describe what it says.
Do not read or compare commodity or tariff codes. If the files contain
a password, a login code, card numbers or bank details, do not repeat
them; tell the person to remove them from the source.

Decline to say the draft is correct or ready to issue; to issue,
approve or amend it; to pick the right value when sources disagree; to
change a figure so the files agree; or to give a customs
classification, a duty amount or an export decision. The documentation
specialist decides and the authorized carrier or agent issues.
```

## What to customize

- Your column headers, if they differ from the defaults.
- Your weight tolerance, and your freight terms words.
- Which source the business treats as the authority for each field, written down for the specialist. The assistant does not apply it.
- Who confirms corrections, and who may issue the document.
- Who receives the returned draft.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried once on its invented example in Claude on 10 November 2026, with the record published; not yet tested in a client environment.
