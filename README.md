# MedVerity AI

**Evidence-aware bilingual medical literature summaries.**

MedVerity AI is an early-stage prototype specification for turning biomedical literature into traceable, plain-language English and Simplified Chinese educational drafts. Its central requirement is that translation must preserve the evidence—not just the words.

> **Status:** planning and specification stage. This repository currently contains product and safety specifications, not a clinically validated or production-ready medical system.

## V1 goal

Given a PubMed identifier or PubMed URL, produce:

- an English educational summary;
- a Simplified Chinese summary with equivalent clinical meaning;
- structured study details and traceable source metadata;
- explicit limitations, uncertainty, and safety notes;
- validated statistical values where the source provides sufficient inputs.

V1 prioritizes a single end-to-end literature workflow over a polished UI, social graphics, user accounts, or automated publishing.

## V1 scope

1. **Ingest:** accept a PMID or PubMed URL; retrieve bibliographic metadata and abstract through NCBI E-utilities.
2. **Access labeling:** distinguish abstract-only analysis from verified full-text analysis. Never imply that full text was read when only an abstract is available.
3. **Evidence extraction:** structure study design, population, intervention/exposure, comparator, outcomes, findings, limitations, and source locations.
4. **Verification:** preserve original reported values; compute derived measures only from sufficient source inputs using deterministic code.
5. **Bilingual generation:** generate English and Simplified Chinese from one shared, verified evidence record and a versioned medical glossary.
6. **Validation:** block or flag output when numerical, terminology, citation, or meaning checks fail.

## Non-goals for V1

- diagnosis, triage, treatment recommendations, or individualized medical advice;
- replacing clinician, pharmacist, translator, or systematic-reviewer judgment;
- claiming comprehensive evidence synthesis from one paper;
- social-media image generation, infographic generation, authentication, billing, or production deployment.

## Proposed stack

- Python 3.11+
- FastAPI for the HTTP API
- Pydantic for validated data contracts
- NCBI E-utilities for PubMed metadata and abstracts
- A configurable LLM provider behind an adapter interface
- Deterministic Python functions for arithmetic and consistency checks
- Pytest for unit, integration, and adversarial regression tests

## Repository map

```text
.
├── README.md
├── docs/
│   ├── ARCHITECTURE.md
│   ├── API_SPEC.md
│   ├── MEDICAL_SAFETY.md
│   └── ROADMAP.md
└── tests/
    └── ADVERSARIAL_TEST_CASES.md
```

## Development principles

1. **Source transparency:** identify exactly which source text was available and analyzed.
2. **Evidence integrity:** never invent study details, effect estimates, citations, DOI values, or missing denominators.
3. **Causal discipline:** distinguish association from causation and explain plausible bias.
4. **Statistical fidelity:** do not conflate RR, OR, HR, RRR, ARR, or percentage points.
5. **Bilingual parity:** both languages must preserve the same claims, numbers, caveats, and uncertainty.
6. **Fail safely:** unresolved ambiguity or failed validation must be visible, not silently repaired.
7. **Human review:** generated material is an educational draft requiring qualified review before publication or clinical use.

## Local development (planned)

Implementation instructions will be added with the first working backend. Do not add real API keys to this repository. Use environment variables and a local `.env` file excluded from version control.

## Disclaimer

MedVerity AI is an educational research-assistance prototype. It is not a medical device, does not provide patient-specific advice, and must not be used to make diagnosis or treatment decisions. Source papers may be incomplete, biased, or wrong; a summary cannot improve the underlying evidence quality.
