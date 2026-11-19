# V1 API Specification (Draft)

## POST /v1/summarize

Accepts one PubMed identifier or PubMed URL and returns paired educational drafts plus source and validation metadata.

### Request
```json
{
  "pmid": "12345678",
  "language_pair": ["en", "zh-CN"],
  "reading_level": "plain_language",
  "include_full_text_if_available": true
}
```
Exactly one of `pmid` or `pubmed_url` is required. V1 language pair is fixed to English and Simplified Chinese.

### Response (illustrative schema)
```json
{
  "status": "validated | needs_human_review | failed",
  "source": {
    "pmid": "12345678",
    "doi": null,
    "title": "Source-provided title",
    "access_level": "abstract_only | full_text_available | retrieval_failed",
    "retrieved_at": "ISO-8601 timestamp",
    "url": "https://pubmed.ncbi.nlm.nih.gov/12345678/"
  },
  "evidence": {
    "study_design": "not_reported",
    "population": "not_reported",
    "intervention_or_exposure": "not_reported",
    "comparator": "not_reported",
    "outcomes": [],
    "claims": [],
    "limitations": [],
    "uncertainties": []
  },
  "summaries": {
    "en": "Educational draft...",
    "zh-CN": "科普初稿……"
  },
  "validation": {
    "numeric_parity": "pass | fail | not_checked",
    "terminology_parity": "pass | fail | not_checked",
    "citation_traceability": "pass | fail | not_checked",
    "issues": []
  },
  "disclaimer": "Educational summary; not individualized medical advice."
}
```

The example is illustrative, not a promise that every field can be extracted from every abstract. Unavailable information must be explicitly marked.

## Error behavior
- 400: malformed identifier or mutually supplied PMID and URL.
- 404: PubMed record not found.
- 429: upstream rate limit reached.
- 502/503: upstream retrieval/provider unavailable.
- 200 with `needs_human_review`: source retrieved but one or more safety/parity checks failed.

Never return a fabricated DOI, source value, or citation to fill a missing field.
