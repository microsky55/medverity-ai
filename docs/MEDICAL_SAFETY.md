# Medical Safety and Evidence Integrity

## Intended use
MedVerity AI creates educational drafts from biomedical literature. It is not a medical device, diagnostic system, triage service, or source of patient-specific treatment advice. Human review is required before publication or clinical use.

## Source transparency
- Label abstract-only versus full-text analysis.
- Do not imply full-text review when only an abstract was retrieved.
- Attach PMID/DOI/URL only when present in verified source metadata.
- Identify unavailable or ambiguous information instead of filling gaps.

## Evidence interpretation
- Distinguish association from causation.
- Evaluate confounding, selection bias, reverse causation, immortal time bias, and other biases only when relevant and supported by study methods.
- A non-significant result does not establish no effect. Consider confidence intervals, precision, power, and clinical importance.
- Treat post-hoc or exploratory subgroup analyses as hypothesis-generating; note multiplicity and prespecification when known.
- Compare populations, interventions/exposures, comparators, outcomes, and follow-up before calling studies contradictory.
- Do not collapse conflicting evidence into a confident single verdict.

## Terminology policy
Maintain a versioned bilingual glossary with definitions, contexts, prohibited conflations, source authority, and reviewer status.

| English | Preferred Chinese | Safety note |
|---|---|---|
| Adverse event (AE) | 不良事件 | Does not itself establish causality. |
| Adverse drug reaction (ADR) | 药品不良反应 | Preserve the source and pharmacovigilance definition. |
| Side effect | 副作用 | Context-dependent; not a universal synonym for AE/ADR. |
| Relative risk reduction (RRR) | 相对风险降低 | Relative change against a stated baseline/control risk. |
| Absolute risk reduction (ARR) | 绝对风险降低 | Absolute difference in event risks over a stated period. |
| Odds ratio (OR) | 比值比 | Not interchangeable with risk ratio. |
| Hazard ratio (HR) | 风险比（瞬时风险比） | Time-to-event relative measure, not an absolute risk reduction. |

Preserve the English term in parentheses when ambiguity matters. Translation must follow clinical context, not literal word substitution.

## Statistical integrity
- Preserve the reported measure and value.
- Never translate a 25% relative reduction as a 25-percentage-point absolute reduction.
- ARR cannot be recovered from RRR without valid baseline/control risk and comparable outcome/time horizon.
- NNT requires a valid absolute risk difference and specified time horizon.
- Do not treat OR as RR or HR as ARR.
- Preserve numerator, denominator, units, confidence interval, and follow-up.
- Record formula and source inputs for every derived value.
- If inputs are incomplete or inconsistent, mark the measure `not_calculable`.

## Bilingual parity
Generate both languages from one verified evidence record. Compare numbers, units, denominators, effect direction, population, sample size, outcome, follow-up, statistical measure, confidence intervals, terminology, citations, and uncertainty wording. Failed checks block validated status and require regeneration or human review.

## Incident response
For a material error: mark or withdraw the affected output, preserve its version and provenance, document the failure, add a regression test, correct both languages, and disclose the correction where distributed.
