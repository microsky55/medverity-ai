# V1 Roadmap

## Milestone 0 — Public specification
- [x] Define V1 scope and non-goals.
- [x] Document source-access labeling and medical safety boundaries.
- [x] Define architecture, API shape, and adversarial test plan.
- [ ] Review specifications with clinical and bilingual terminology reviewers.

## Milestone 1 — PubMed ingestion
- [ ] Parse PMID and PubMed URLs.
- [ ] Integrate NCBI E-utilities with timeouts, retries, and rate-limit compliance.
- [ ] Capture source metadata, abstract, PMID, DOI when present, and retrieval timestamp.
- [ ] Detect and label abstract-only versus retrieved PMC full text.
- [ ] Add fixtures and integration tests.
**Exit criteria:** metadata is source-grounded; retrieval failures are explicit; access level is truthful.

## Milestone 2 — Structured evidence extraction
- [ ] Define strict Pydantic evidence schemas.
- [ ] Implement configurable LLM provider adapter.
- [ ] Extract study design, population, intervention/exposure, comparator, endpoints, findings, limitations, and claim provenance.
- [ ] Reject malformed output and unsupported claims.
**Exit criteria:** each material claim traces to retrieved text or is marked unavailable/unsupported.

## Milestone 3 — Statistical and terminology verification
- [ ] Add distinct typed fields for RR, OR, HR, RRR, ARR, and NNT.
- [ ] Implement deterministic formulas with input/provenance requirements.
- [ ] Create a versioned, reviewable English–Simplified Chinese glossary.
- [ ] Add AE/ADR/side-effect and RRR/ARR regression tests.
**Exit criteria:** no measure conflation; calculations reproducible from recorded inputs.

## Milestone 4 — Bilingual generation and parity
- [ ] Generate both drafts from the same verified evidence record.
- [ ] Preserve citations, caveats, and uncertainty.
- [ ] Compare numbers, units, effect direction, study context, and terminology.
- [ ] Return `needs_human_review` when ambiguity remains.
**Exit criteria:** seeded adversarial examples pass or are blocked with actionable reasons.

## Milestone 5 — Local demo
- [ ] Expose POST /v1/summarize through FastAPI.
- [ ] Add deterministic mocked tests that need no paid model calls.
- [ ] Document setup and sample request/response.
- [ ] Demonstrate abstract-only and full-text-available cases with truthful access labels.
**Exit criteria:** a developer can run the API and reproduce tests locally.

## Deferred to V2+
Frontend, accounts, cloud hosting, payments, social scheduling, infographics, and image generation.
