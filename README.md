# ClaimGuard — Safe Field Extraction for Motor Claims Intake

> A Forward Deployed Engineering (FDE) proof of concept. This repository contains both the **pre-transformation** (before) and **post-transformation** (after) states of the solution, so the impact of the work can be seen side by side.

---

## 1. Overview

| Item | Details |
|------|---------|
| **POC Name** | ClaimGuard — Safe Field Extraction for Motor Claims Intake |
| **Scenario / Customer** | Illustrative motor-insurance claims team that receives case application PDFs and keys them into a decision system (synthetic data, no real customer) |
| **Owner** | adiraj2503@gmail.com |
| **Status** | Completed (mock and Azure runs produced; offline self-test result not recorded here) |
| **Program** | FDE Program — Sprint 1, Day 14 lab (Assignment 3) |

**One-line summary:** A confidence threshold alone lets wrong values through OCR extraction; adding pattern and cross-field checks removed every wrong acceptance in the test set, while tighter thresholds removed none.

---

## 2. Problem Statement

Ten synthetic case application PDFs must be turned into structured decision profiles (key-value pairs mapped to a fixed schema). The brief says "accept a field if OCR confidence is above 0.85, otherwise flag it". That rule looks safe and is not.

- **Confidence is not correctness.** It is the model's certainty about what it saw, not whether the value is right. A letter `O` read for a zero can score 0.86 and pass.
- **Failures are silent.** Wrong values still produce well-formed records, and nothing errors.
- **Real services fail quietly too.** Missing feature flags, free-tier page truncation and punctuation spacing all return HTTP 200 with fewer fields than expected.
- **Wrong data is costly.** A wrongly accepted policy number or total means rework, a complaint or a regulatory finding, discovered only downstream.

---

## 3. Pre-Transformation (Before)

The starting state is the policy the brief asks for: `flat_0.85`. It accepts any field above 0.85 confidence and flags the rest, using confidence and nothing else.

| Aspect | Current State |
|--------|---------------|
| Process | Accept if confidence ≥ 0.85, otherwise flag. No validation of the value itself. |
| Model / Tooling | Document Intelligence output (mock responses, or Azure `prebuilt-layout`), label map, single flat threshold |
| Cost | Lowest review load — 15 flagged fields on the mock run, 0 on the Azure run |
| Latency / Performance | Deterministic, instant on mock; Azure cost is the OCR call only |
| Accuracy / Quality | **5 wrong values accepted** (mock), **6** (Azure). Unparseable values are stored as raw strings and accepted. |
| Pain points | Wrong values pass with no warning, e.g. APP-0003 `policy_number` `MOT-45O3901` (letter O for zero) at confidence 0.86 |

**Location in repo:** [Pre-Transformation/](Pre-Transformation/)

---

## 4. Post-Transformation (After)

The end state adds validation to the same pipeline and compares it with per-field tuning. Three policies are run over the same ten documents and scored against ground truth.

| Aspect | New State |
|--------|-----------|
| Process | Pattern checks, OCR-character repair, cross-field checks (totals, dates, plausibility), conflict surfacing, ambiguous-date refusal, and an identity-document scope gate. Anything suspicious is flagged for a human. |
| Model / Tooling | `flat_0.85_checked` (same threshold plus checks) and `tiered` (per-field thresholds plus checks). Provider seam lets the same logic run on mock or Azure. Azure client retries on HTTP 429. |
| Cost | More fields go to review: 26 flagged under `flat_0.85_checked`, 42 under `tiered` (mock) |
| Latency / Performance | Extraction is deterministic and free to re-run; Azure raw responses are cached so only the first read is paid |
| Accuracy / Quality | **0 wrong accepted** under both checked policies on the mock run; 1 on the Azure run |
| Benefits | Wrong values are caught by what a valid value looks like, not by the model's confidence |

**Location in repo:** [Post-Transformation/](Post-Transformation/)

---

## 5. Before vs. After

Mock run, 10 documents (source: [extraction_report.md](Post-Transformation/out/mock/extraction_report.md)).

| Metric | Pre-Transformation (`flat_0.85`) | Post-Transformation (`flat_0.85_checked`) | Change |
|--------|----------------------------------|-------------------------------------------|--------|
| Wrong accepted | 5 | 0 | −5 (−100%) |
| Fields accepted | 75 | 64 | −11 |
| Accepted and correct | 60 | 56 | −4 |
| Flagged for review | 15 | 26 | +11 |
| Missing required | 3 | 3 | no change |

| Policy | Accepted | Correct | **Wrong accepted** | Flagged | Missing |
|---|---|---|---|---|---|
| `flat_0.85` (mock) | 75 | 60 | **5** | 15 | 3 |
| `flat_0.85_checked` (mock) | 64 | 56 | **0** | 26 | 3 |
| `tiered` (mock) | 48 | 40 | **0** | 42 | 3 |
| `flat_0.85` (Azure, F0 tier) | 89 | 71 | **6** | 0 | 4 |
| `flat_0.85_checked` (Azure, F0 tier) | 78 | 67 | **1** | 11 | 4 |
| `tiered` (Azure, F0 tier) | 77 | 66 | **1** | 12 | 4 |

Tiered thresholds on top of the checks removed **zero** further wrong values and added 16 fields to the review queue. Mean confidence was 0.893 on the mock and 0.990 on the Azure service, so on clean digital PDFs the real service gave thresholds almost nothing to separate. Full detail: [confidence_delta.md](Post-Transformation/out/azure/confidence_delta.md).

---

## 6. Approach

1. **Discover** – Read the brief ("accept above 0.85, otherwise flag") and list what real forms do: invented labels, handwriting, missing fields, conflicting pages, ambiguous dates, attached ID documents.
2. **Baseline** – Run the brief's policy, `flat_0.85`, and count wrong acceptances against ground truth.
3. **Evaluate** – Compare three policies (flat, flat plus checks, tiered plus checks) on wrong accepted first, flagged second.
4. **Build** – Pattern and cross-field validators, a label map held as data, a provider seam between business logic and the OCR vendor, and a REST adapter for Azure Document Intelligence.
5. **Measure** – Run on mock data and on a real Azure resource, then compare confidences and read what changed.
6. **Hand off** – Generated report with six open questions for an ADR, plus a learner guide ([Day14_DocInt_Interpreting_Your_Results.docx](Post-Transformation/Day14_DocInt_Interpreting_Your_Results.docx)) and a full repository analysis ([project_analysis.md](Post-Transformation/project_analysis.md)).

### Decision Criteria

| Criterion | Weight | Why |
|---|---|---|
| Wrong values accepted | Highest (judged first) | The only outcome that can hurt a customer, and it is invisible until downstream |
| Review-queue size (flag rate) | Second | A flag costs roughly thirty seconds of handler time (a lab assumption, not measured) |
| Missing required fields | Third | Shows whether the extractor, or the input pages, are the problem |

Weights are ordering, not percentages; the lab does not assign numeric weights.

---

## 7. Repository Structure

```
Assignment3/
├── README.md                    # this file
├── README_TEMPLATE.md           # template this README was filled from
├── Pre-Transformation/          # "Before" state
│   ├── run_lab.py               # CLI entry point
│   ├── docint_lab/              # extract, provider, config, mock + azure adapters, selftest
│   ├── build/                   # builds the learner guide
│   └── README.md
└── Post-Transformation/         # "After" state
    ├── run_lab.py
    ├── docint_lab/              # same modules; azure_docint.py adds 429 retry
    ├── docs/                    # APP-0001..0010.pdf rendered for the Azure path
    ├── out/mock/                # report, field_results.csv, profiles/
    ├── out/azure/               # same, plus di_raw/ and confidence_delta.md
    ├── project_analysis.md      # full repository analysis
    ├── Day14_DocInt_Interpreting_Your_Results.docx
    └── README.md                # detailed lab guide
```

The code in the two folders is otherwise identical; the post folder adds the generated outputs, the rendered PDFs and the analysis. The before/after difference is in how the pipeline is run and judged: `flat_0.85` versus the checked policies.

---

## 8. Getting Started

### Prerequisites

- Python 3.9 or newer. Standard library only — no `pip install`, no `requirements.txt`.
- Azure only (optional): an Azure AI Document Intelligence resource, its endpoint and key. Use the **S0** tier; F0 reads only the first two pages of each document.

### Setup

```powershell
cd Post-Transformation
copy .env.example .env
```

The mock path needs nothing in `.env`. For Azure, set `AZURE_DOCINT_ENDPOINT` and `AZURE_DOCINT_KEY`. `.env` holds a live key — do not commit or share it.

### Run

```powershell
python run_lab.py --policy flat_0.85      # the brief's policy: see what gets through
python run_lab.py --show APP-0003         # trace the O-for-zero policy number
python run_lab.py --compare               # all three policies with the summary
python run_lab.py --selftest              # 141 offline checks of the Azure adapter

python run_lab.py --make-pdfs             # render docs/APP-XXXX.pdf (once, for Azure)
python run_lab.py --provider azure --compare
```

Outputs are written to `out/<provider>/`. On Windows use `python` or `py` rather than `python3`.

---

## 9. Results & Learnings

- **Key result:** On the mock data, the brief's 0.85 threshold accepted 5 wrong values. Adding checks removed all 5. Tiered thresholds removed none more and added 16 flagged fields.
- **What worked:** Pattern checks, cross-field arithmetic and date checks, refusing ambiguous dates, surfacing conflicts instead of picking one, and dropping identity-document data before it reaches the profile.
- **What didn't:** Tiered thresholds bought no extra safety here. Identifier repair replaces letters across the whole string (including the `MOT` prefix), so policy numbers and registrations with OCR errors are flagged rather than repaired. Money parsing mishandles European formats such as `1.234,50`.
- **Recommendations:** Ship validation first; add per-field thresholds only if the extra review cost is accepted. Cache the paid OCR step and re-run the deterministic extraction freely. Use S0, not F0, for any Azure measurement.

> Caveats: Data is synthetic and only ten documents. Mock confidences were chosen to make a teaching point, not measured. The Azure run used the F0 tier, which truncates documents to two pages, so APP-0005's conflict, APP-0007's identity-document page and part of APP-0010 never reached the pipeline; the Azure "1 wrong accepted" is likely a measurement artefact of that. The Azure PDFs are digitally generated, so confidence there is a ceiling, and handwriting is not simulated. The offline self-test (`--selftest`) result has not been recorded in this repository.

---

## 10. Next Steps

- [ ] Re-run the Azure comparison on an S0 resource with `out/azure/di_raw/` cleared
- [ ] Fix identifier repair to change only positions that must be digits, and add unit tests for `extract.py`
- [ ] Wrap `extract()` as an Azure Function with Blob Storage for the original document and managed identity
- [ ] Re-tune thresholds on a sample of the client's real scanned forms

---

## 11. Contact

adiraj2503@gmail.com
