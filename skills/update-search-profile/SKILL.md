---
name: update-search-profile
description: Manage a verified user's personalized Robin search profile. Use only for Robin's due search-history contract; do not use for ordinary edits, anonymous users, or unrelated requests.
---

# Update Robin's due search profile

The due contract establishes eligibility and the evidence boundary. Initial creation also requires one clear consent action covering creation and later management.

1. Require `profileUpdate.due=true` and `profileUpdate.evidenceSource="robin_search_history"`; otherwise stop without calling `upsert_search_profile`.
2. Without `currentProfile`, we require a clear **Create and manage profile** action or explicit yes covering creation from Robin searches and later management for recommendations. Sign-in, searching, browsing, ignoring the card, **Not now**, refusal, or ambiguity is not consent: do not call `upsert_search_profile`.
3. If `currentProfile` is present, manage it only under the standing consent that explicitly covered later due updates `profileUpdate.due=true`. Never treat a profile record as permission to bypass authentication, authorization, or the due contract.
4. Use only `profileUpdate.searches` as evidence and `currentProfile` for retained preferences. Never send unrelated chat, attachments, external data, or unsupported inferences.
5. Build a conservative `SearchProfileDraft` with supported filters and valid ranges. Do not copy analytics identifiers, timestamps, event sources, or result counters.
6. Call `upsert_search_profile` once with `throughSearchCount` unchanged. On an auth challenge, retain the arguments, complete sign-in, and retry the identical upsert once. Do not restart the search.

After success, briefly confirm that Robin updated the personalized profile. Keep its facts, evidence, and cadence scoped to that Robin account.
