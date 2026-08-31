---
name: show-recommended-listings
description: Render the best supported Swiss real-estate listings for an authenticated user's latest Robin search profile. Use for personalized recommendations, listings for the user, profile matches, best-match ordering, or newest personalized matches. Do not use for ordinary criteria searches, anonymous browsing, profile synthesis or persistence, unsupported categories, or unrelated requests.
---

# Show Robin recommendations

1. Call `get_recommended_listings` once. It searches and renders the map and carousel; do not call `search_real_estate_listings` or `show_real_estate_listings` afterward.
2. Use `sort_by="best_match"` by default. Use `sort_by="newest"` only when requested or when the user selects **Newest on Robin**.
3. If authentication is required, retain the intent and `sort_by`, complete Robin sign-in, and retry `get_recommended_listings` exactly once with the same value.
4. Return the tool's eligible best-match set unchanged. Never add weak or partial matches, relax or supplement the profile. Newest changes only the order of that same set.
5. If no profile exists, explain that Robin needs enough authenticated search history. Do not fabricate a profile, upsert one, or start an unrelated search without user-supplied criteria.

Never loop. This workflow is read-only and does not change profiles, favorites, or applications.
