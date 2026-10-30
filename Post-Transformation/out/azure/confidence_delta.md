# Mock confidence vs Azure confidence

The mock's numbers were chosen to make a teaching point. These were
produced by the service. When you present this lab, quote the right
column and say where it came from.

Fields in the mock: **95**  ·  returned by the service: **90**  ·  not returned: **5**

Mean confidence — mock **0.893**, service **0.990**.

| Doc | Label | Mock conf | Azure conf | Mock value | Azure value |
|---|---|---|---|---|---|
| APP-0001 | Claim Reference | 0.97 | 1.00 | `CLM-2026-4471` | `CLM-2026-4471` |
| APP-0001 | Policy Number | 0.96 | 1.00 | `MOT-4471902` | `MOT-4471902` |
| APP-0001 | Applicant Full Name | 0.95 | 0.95 | `[PERSON_01]` | `[PERSON_01]` |
| APP-0001 | Date of Birth | 0.94 | 1.00 | `1987-04-12` | `1987-04-12` |
| APP-0001 | Vehicle Registration | 0.96 | 1.00 | `KP19 TRX` | `KP19 TRX` |
| APP-0001 | Incident Date | 0.95 | 1.00 | `2026-03-14` | `2026-03-14` |
| APP-0001 | Sum Insured | 0.93 | 1.00 | `9000.00` | `9000.00` |
| APP-0001 | Excess | 0.94 | 1.00 | `350.00` | `350.00` |
| APP-0001 | Repair Estimate Total | 0.95 | 1.00 | `12400.00` | `12400.00` |
| APP-0002 | Claim Ref. | 0.96 | 0.99 | `CLM-2026-4482` | `CLM-2026-4482` |
| APP-0002 | Policy No | 0.95 | 1.00 | `MOT-4482901` | `MOT-4482901` |
| APP-0002 | Name of Applicant | 0.94 | 0.99 | `[PERSON_03]` | `[PERSON_03]` |
| APP-0002 | D.O.B. | 0.92 | 1.00 | `1991-09-30` | `1991-09-30` |
| APP-0002 | Reg No | 0.95 | 1.00 | `LT21 WNB` | `LT21 WNB` |
| APP-0002 | Date of Loss | 0.93 | 1.00 | `2026-04-02` | `2026-04-02` |
| APP-0002 | Sum Ins. | 0.91 | 0.99 | `9100.00` | `9100.00` |
| APP-0002 | Policy Excess | 0.93 | 1.00 | `250.00` | `250.00` |
| APP-0002 | Estimate Total | 0.94 | 1.00 | `6220.00` | `6220.00` |
| APP-0003 | Claim Reference | 0.88 | 0.96 | `CLM-2026-45O3` | `CLM-2026-45O3` |
| APP-0003 | Policy Number | 0.86 | 0.94 | `MOT-45O3901` | `MOT-45O3901` |
| APP-0003 | Applicant Full Name | 0.71 | 0.96 | `[PERSON_04]` | `[PERSON_04]` |
| APP-0003 | Date of Birth | 0.69 | 0.97 | `1979-11-O5` | `1979-11-O5` |
| APP-0003 | Vehicle Registration | 0.83 | 1.00 | `BD1B MHK` | `BD1B MHK` |
| APP-0003 | Incident Date | 0.90 | 1.00 | `2026-03-09` | `2026-03-09` |
| APP-0003 | Sum Insured | 0.74 | 0.99 | `775O.OO` | `775O.OO` |
| APP-0003 | Excess | 0.72 | 1.00 | `3OO.OO` | `3OO.OO` |
| APP-0003 | Repair Estimate Total | 0.79 | 0.91 | `341O.OO` | `341O.OO` |
| APP-0004 | Claim Reference | 0.96 | 1.00 | `CLM-2026-4517` | `CLM-2026-4517` |
| APP-0004 | Policy Number | 0.94 | 1.00 | `MOT-4517901` | `MOT-4517901` |
| APP-0004 | Applicant Full Name | 0.93 | 0.98 | `[PERSON_05]` | `[PERSON_05]` |
| APP-0004 | Vehicle Registration | 0.95 | 1.00 | `GF22 PLT` | `GF22 PLT` |
| APP-0004 | Incident Date | 0.92 | 0.99 | `2026-03-28` | `2026-03-28` |
| APP-0004 | Repair Estimate Total | 0.94 | 1.00 | `15900.00` | `15900.00` |
| APP-0005 | Claim Reference | 0.96 | 1.00 | `CLM-2026-4526` | `CLM-2026-4526` |
| APP-0005 | Policy Number | 0.95 | 1.00 | `MOT-4526901` | `MOT-4526901` |
| APP-0005 | Applicant Full Name | 0.94 | 0.98 | `[PERSON_06]` | `[PERSON_06]` |
| APP-0005 | Date of Birth | 0.93 | 1.00 | `1984-02-17` | `1984-02-17` |
| APP-0005 | Vehicle Registration | 0.95 | 1.00 | `HN20 XCE` | `HN20 XCE` |
| APP-0005 | Incident Date | 0.94 | 0.99 | `2026-04-03` | `2026-04-03` |
| APP-0005 | Sum Insured | 0.92 | 1.00 | `6400.00` | `6400.00` |
| APP-0005 | Excess | 0.93 | 1.00 | `250.00` | `250.00` |
| APP-0005 | Repair Estimate Total | 0.94 | 1.00 | `2150.00` | `2150.00` |
| APP-0005 | Repair Estimate Total | 0.91 | 1.00 | `2450.00` | `2150.00` |
| APP-0006 | Claim Reference | 0.96 | 1.00 | `CLM-2026-4534` | `CLM-2026-4534` |
| APP-0006 | Policy Number | 0.95 | 1.00 | `MOT-4534901` | `MOT-4534901` |
| APP-0006 | Applicant Full Name | 0.94 | 0.96 | `[PERSON_07]` | `[PERSON_07]` |
| APP-0006 | Date of Birth | 0.92 | 1.00 | `1996-06-21` | `1996-06-21` |
| APP-0006 | Vehicle Registration | 0.95 | 1.00 | `JW19 RQA` | `JW19 RQA` |
| APP-0006 | Incident Date | 0.93 | 1.00 | `2026-03-17` | `2026-03-17` |
| APP-0006 | Sum Insured | 0.92 | 1.00 | `10200.00` | `10200.00` |
| APP-0006 | Excess | 0.93 | 1.00 | `350.00` | `350.00` |
| APP-0006 | Repair Estimate Total | 0.94 | 1.00 | `11050.00` | `11050.00` |
| APP-0006 | I do NOT wish to claim for personal injury | 0.88 | 0.90 | `selected` | `selected` |
| APP-0007 | Claim Reference | 0.96 | 1.00 | `CLM-2026-4548` | `CLM-2026-4548` |
| APP-0007 | Policy Number | 0.95 | 1.00 | `MOT-4548901` | `MOT-4548901` |
| APP-0007 | Applicant Full Name | 0.94 | 0.98 | `[PERSON_08]` | `[PERSON_08]` |
| APP-0007 | Date of Birth | 0.93 | 1.00 | `1988-12-03` | `1988-12-03` |
| APP-0007 | Vehicle Registration | 0.95 | 0.98 | `MS21 TVB` | `MS21 TVB` |
| APP-0007 | Incident Date | 0.94 | 0.99 | `2026-03-25` | `2026-03-25` |
| APP-0007 | Sum Insured | 0.92 | 1.00 | `8900.00` | `8900.00` |
| APP-0007 | Excess | 0.93 | 1.00 | `300.00` | `300.00` |
| APP-0007 | Repair Estimate Total | 0.94 | 0.99 | `7630.00` | `7630.00` |
| APP-0007 | Driving Licence Number | 0.91 | — | `SMITH912035AB9CD` | *not returned* |
| APP-0007 | Licence Issue Date | 0.90 | — | `2019-08-14` | *not returned* |
| APP-0007 | Licence Address Line 1 | 0.87 | — | `14 Fernbank Road` | *not returned* |
| APP-0007 | Licence Postcode | 0.92 | — | `LS8 3QT` | *not returned* |
| APP-0008 | Claim Reference | 0.96 | 1.00 | `CLM-2026-4552` | `CLM-2026-4552` |
| APP-0008 | Policy Number | 0.95 | 1.00 | `MOT-4552901` | `MOT-4552901` |
| APP-0008 | Applicant Full Name | 0.93 | 0.95 | `[PERSON_09]` | `[PERSON_09]` |
| APP-0008 | Date of Birth | 0.92 | 1.00 | `1972-05-08` | `1972-05-08` |
| APP-0008 | Vehicle Registration | 0.94 | 1.00 | `PC17 KDN` | `PC17 KDN` |
| APP-0008 | Incident Date | 0.93 | 1.00 | `2026-03-12` | `2026-03-12` |
| APP-0008 | Sum Insured | 0.91 | 1.00 | `5600.00` | `5600.00` |
| APP-0008 | Excess | 0.92 | 1.00 | `250.00` | `250.00` |
| APP-0008 | Parts Subtotal | 0.93 | 1.00 | `2900.00` | `2900.00` |
| APP-0008 | Labour Subtotal | 0.92 | 1.00 | `1480.00` | `1480.00` |
| APP-0008 | Repair Estimate Total | 0.95 | 1.00 | `4880.00` | `4880.00` |
| APP-0009 | Claim Reference | 0.96 | 1.00 | `CLM-2026-4561` | `CLM-2026-4561` |
| APP-0009 | Policy Number | 0.95 | 1.00 | `MOT-4561901` | `MOT-4561901` |
| APP-0009 | Applicant Full Name | 0.94 | 0.96 | `[PERSON_10]` | `[PERSON_10]` |
| APP-0009 | Date of Birth | 0.90 | 1.00 | `12/07/1993` | `12/07/1993` |
| APP-0009 | Vehicle Registration | 0.95 | 1.00 | `QT19 LFS` | `QT19 LFS` |
| APP-0009 | Incident Date | 0.91 | 1.00 | `04/03/2026` | `04/03/2026` |
| APP-0009 | Sum Insured | 0.92 | 1.00 | `9800.00` | `9800.00` |
| APP-0009 | Excess | 0.93 | 1.00 | `400.00` | `400.00` |
| APP-0009 | Repair Estimate Total | 0.94 | 1.00 | `13200.00` | `13200.00` |
| APP-0010 | Claim Reference | 0.64 | 1.00 | `CLM-2026-4573` | `CLM-2026-4573` |
| APP-0010 | Policy Number | 0.61 | 1.00 | `MOT-4573901` | `MOT-4573901` |
| APP-0010 | Applicant Full Name | 0.58 | 0.94 | `[PERSON_11]` | `[PERSON_11]` |
| APP-0010 | Date of Birth | 0.55 | 1.00 | `1990-01-22` | `1990-01-22` |
| APP-0010 | Vehicle Registration | 0.67 | 1.00 | `ZB20 HRC` | `ZB20 HRC` |
| APP-0010 | Incident Date | 0.62 | 1.00 | `2026-04-06` | `2026-04-06` |
| APP-0010 | Sum Insured | 0.59 | 1.00 | `7100.00` | `7100.00` |
| APP-0010 | Excess | 0.60 | 1.00 | `350.00` | `350.00` |
| APP-0010 | Repair Estimate Total | 0.63 | — | `5940.00` | *not returned* |

## Read this before you draw a conclusion

**A field the service did not return is not a service failure.** Key-value pair extraction finds the pairs it recognises as pairs. A label the model does not read as a label produces no pair at all — which lands in `missing_required`, not in the review queue. Those are different failures and they need different handling.

**Check whether the page was read at all before you blame the extraction.** On a free-tier (F0) resource the service analyses the first two pages and stops — HTTP 200, no error, no warning, a `pages` array that just ends. Every field printed after page two then reports as *not returned*, which looks identical to a label the model failed to recognise and is nothing of the kind. The run prints a **PAGES THE SERVICE DID NOT READ** block when it detects this; if that block is present, the rows below for those documents are measuring the pricing tier, not the model.

**These PDFs are digitally generated.** The text is embedded, not scanned, so the service reads it far more confidently than it would read the forms this lab is modelling. Confidence measured here is a ceiling, not an estimate. To get a real number, run the client's own scans through the same pipeline — that is the first thing to ask for.

**The OCR-confusion values survive the round trip.** `CLM-2026-45O3` was rendered with the letter O and comes back with the letter O, at high confidence. That is the entire lesson holding up against the real service: nothing errored, nothing scored low, and only the pattern check knows the value is wrong.
