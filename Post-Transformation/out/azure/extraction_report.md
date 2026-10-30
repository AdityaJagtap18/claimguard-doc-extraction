# Document Intelligence extraction report — DecisionStream AI

Documents processed: **10**
Source: **azure** (Azure AI Document Intelligence — measured confidences; see `confidence_delta.md`)

## Policy comparison

| Policy | Accepted | Correct | **Wrong accepted** | Flagged | Missing |
|---|---|---|---|---|---|
| flat_0.85 | 89 | 71 | **6** | 0 | 4 |
| flat_0.85_checked | 78 | 67 | **1** | 11 | 4 |
| tiered | 77 | 66 | **1** | 12 | 4 |

### How to read this table

**Wrong accepted** is the only column that can hurt a customer. Those are values the pipeline passed through as correct, with no warning attached, that were not correct.

Flagged is not failure. A flagged field costs a handler thirty seconds. A wrongly accepted identifier costs a rework cycle, a complaint, or a regulatory finding — and nobody knows it happened until someone notices downstream.

## Per-document notes

| Document | Pages | What makes it hard |
|---|---|---|
| APP-0001 | 2 | clean baseline |
| APP-0002 | 2 | non-standard field labels |
| APP-0003 | 2 | handwritten form, OCR character confusion |
| APP-0004 | 1 | incomplete form, two fields absent |
| APP-0005 | 3 | field appears twice with different values |
| APP-0006 | 2 | checkbox semantics |
| APP-0007 | 3 | identity document attached — scope question |
| APP-0008 | 2 | line items do not reconcile to total |
| APP-0009 | 2 | ambiguous date format |
| APP-0010 | 4 | poor scan, low confidence across the board |

## Questions to answer before this goes in the ADR

1. What is your accept threshold for an IDENTIFIER, and why is it different from your threshold for a name?
2. APP-0003 returned a claim reference with a letter O in place of a zero, at confidence 0.88. What caught it — the threshold, or the pattern check? What does that tell you about relying on confidence?
3. Your pipeline repairs some OCR errors automatically. Should a repaired value ever be auto-accepted? Who decided?
4. APP-0007 contained driving licence data. Your pipeline dropped it. Was that the right call, and where is that decision recorded?
5. What is the handler cost of your flag rate at 4,000 documents a month, and does the business know that number?
6. What is your review trigger for re-tuning these thresholds?
