# Source Handling

## Source Precedence Hierarchy
When sources conflict, resolve using this hierarchy (most authoritative first):

1. **maya-corrections.md** — Explicit corrections to known errors in source material
2. **Operator corrections during review** — Maya's live corrections during review gates
3. **Operator notes** (sources/operator-notes/) — Direct from Maya, committed as source. Precedence depends on specificity and recency.
4. **System snapshots** (sources/system-snapshots/) — Gmail XML, n8n JSON, ClickUp API exports, .ics files. How systems actually behave.
5. **Signed contracts and dated documents** — Formal agreements with timestamps
6. **Website copy** — Authoritative for public positioning and brand voice; less reliable for operational truth
7. **Undated notes and drafts** — Useful but lowest confidence

## Conflict Resolution
- Apply precedence hierarchy first.
- If resolved: use the higher-precedence source, note the conflict in extraction.
- If unresolvable: tag `[CONFLICT: source A says X, source B says Y]` and escalate to Maya during review.
- For minor differences that don't affect automation: tag `[DISCREPANCY]` and move on.

## maya-corrections.md
- Check this file at the start of every session.
- Corrections override the source they correct, regardless of that source's precedence level.
- Format: date, source with error, what it says, what's actually true, when discovered.

## Source Type Handling

### System Snapshots
- Highest-fidelity technical source. Treat as ground truth for system configuration.
- Review for sensitive data (API keys, passwords) before committing — Maya handles sanitization.
- If a snapshot contradicts a narrative document, the snapshot wins (unless Maya corrects).

### Operator Notes
- Maya's in-head knowledge committed as source. Citable in fact records.
- May use suggested template (Topic, Facts, Examples, Uncertainties) or any format.
- Treat with high confidence for business operations and relationship context.
- Treat with moderate confidence for technical details (cross-check against snapshots when possible).

### Prior Work (Claude-produced)
- Handoff documents and audit reports from Claude conversations.
- High-value starting points but may contain errors — especially specific values, dates, or technical details.
- Every fact extracted from prior work still requires source-level verification or Maya confirmation.
- Check maya-corrections.md for known errors before citing prior work.

### Website Exports
- Authoritative for brand voice, positioning, public-facing messaging.
- Less reliable for operational truth (services pages may be aspirational or outdated).
- If SB runs over multiple weeks, consider re-exporting before Phase 5.

### Drive Files and Local Documents
- Vary widely in currency and reliability.
- Always check manifest status (current/outdated/irrelevant) before deep extraction.
- Dated documents outrank undated ones.
