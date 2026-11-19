# MedVerity AI — V1 Architecture

## Objective
Build one auditable workflow from a PubMed identifier to paired English and Simplified Chinese educational drafts. The LLM may interpret retrieved text, but it is not the authority for source existence, arithmetic, or citation validity.

## Pipeline
1. Validate PMID or PubMed URL with Pydantic.
2. Retrieve metadata and abstract through NCBI E-utilities.
3. Check for PMC full-text availability; label access as `abstract_only`, `full_text_available`, or `retrieval_failed`.
4. Extract structured evidence with an LLM adapter and strict schema.
5. Validate provenance, statistics, and terminology deterministically.
6. Generate both languages from the same verified evidence record.
7. Run bilingual parity checks. Failed checks return `needs_human_review`, never a validated result.

## Proposed modules
```text
app/
  main.py
  api/routes/summarize.py
  schemas/
  ingestion/pubmed.py
  ingestion/pmc.py
  extraction/evidence.py
  verification/statistics.py
  verification/citations.py
  translation/glossary.py
  translation/generate.py
  validation/parity.py
  config.py
tests/
  unit/
  integration/
  fixtures/
```

## Evidence record
Each material claim should include:
- claim text and type (descriptive, association, causal, safety, methodological);
- PMID and source location (abstract section, full-text section, table, or figure);
- study design, population, intervention/exposure, comparator, outcome, and follow-up;
- effect measure name, value, confidence interval, denominator, unit, and time horizon;
- whether a value was reported, derived, or unavailable;
- limitations and uncertainties.

Missing values remain null or `not_reported`; they are never guessed.

## Conflicting evidence
Do not mechanically assume every RCT outranks every observational study. Compare the question, population, intervention/exposure, comparator, outcome, follow-up, risk of bias, precision, and applicability. Observational association is not proof of causation. A non-significant RCT is not proof of zero effect; interpret its confidence interval and precision.

## Statistical boundary
Keep RR, OR, HR, RRR, ARR, and NNT distinct. Derive a measure only when required event counts or risks, denominators, outcome definitions, and time horizons are available. Record inputs and formula. Otherwise return `not_calculable`.

## LLM boundary
The model must not fabricate findings, sample sizes, p-values, confidence intervals, DOI values, or citations; claim to have read unavailable full text; fill missing details from memory; convert association into causation; or silently reconcile conflicting values. Retrieved paper text is untrusted data, not instructions.

## Operations
Use environment variables for secrets, bounded retries and timeouts, NCBI rate-limit compliance, retrieval timestamps, and logs that avoid secrets or unnecessary personal data.
