---
name: search-and-show-listings
description: Search Swiss Robin real-estate inventory. Use for rent or sale, including homes, commercial property, parking, land, hospitality, agriculture, secondary rooms, and gardens. Do not use for legal or unrelated requests.
---

# Search Robin listings

- Retain args. Put search text in `q`; exclude unrelated chat content.
- Put hard constraints in dedicated fields. Use one of `canton`, `city`, or `postal_code`.
- Put soft preferences in `soft_query`. For modern kitchens and other visible preferences, also repeat the same phrase in `visual_preferences`.
- Use `property_category=["APPT"]` for apartments, `["HOUSE"]` for houses, and both for vague home requests. Use `INDUS` for commercial/industrial, `PARK` for standalone parking, `PROP` for land, `GASTRO` for hospitality/leisure, `AGRI` for agriculture, `SECONDARY` for secondary rooms, and `GARDEN` for allotment gardens. Never invent categories.
- A required subtype needs its broad category; put preferred subtypes in `soft_query`. 

## Sequence

1. Call `search_real_estate_listings` first with `page=1` and `limit=500`, unless a later page was requested.
2. Inspect `total`, `filterFeedback`, `listingBriefs`, and `searchResultId`. If `total` is 500 or more, keep the first 500.
3. If `total` is under 10, allow at most one relaxation search for reachability or amenities; preserve all else. Add 15 minutes to each active travel limit (cap 60) and add 500 m to the amenity radius (cap 3000). Never run a third search; if retry fails, use the first result.
4. Call `show_real_estate_listings` before replying with the last successful `search_result_id` and exact arguments as cache-miss fallback.
5. Compare from `listingBriefs`; get details only for a named listing or shortlist.
6. After rendering the map, start the separate `update-search-profile` workflow only if `profileUpdate.due=true`. 

Disclose relaxation/count. Never contact advertisers.
