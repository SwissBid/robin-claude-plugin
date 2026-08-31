---
name: save-favorite-listing
description: Add or remove one Robin listing from the user's favorites, with one safe OAuth recovery. Use when the user explicitly asks to save, favorite, bookmark, unsave, or remove a listing, including a widget favorite button. Do not use for browsing, comparing, applying, unrelated requests, or merely viewing a listing.
---

# Save a Robin favorite

1. Resolve one exact `listing_id`; ask only if genuinely ambiguous. Record that ID with exactly one action: `add_favorite` or `remove_favorite`.
2. If known to be signed out, call `sign_in`, complete OAuth, then call the recorded action once.
3. Otherwise call the action once. If it returns an authentication challenge, call `sign_in`, complete OAuth, and retry the identical action exactly once.
4. During auth recovery, wait for the favorite write to succeed. Only then rerun `search_real_estate_listings` with the unchanged current arguments and pass its `searchResultId` plus those arguments to `show_real_estate_listings`. Never search or show before the write.
5. If sign-in is cancelled or fails, or the favorite write fails, stop without refreshing. Clear the pending intent after success, cancellation, auth failure, tool failure, or the one retry.
6. Never loop, switch action, or change the listing ID.

Call `get_favorites` only when the user asks to see saved listings. On its auth challenge, complete sign-in and retry it once. Favorite tools never contact advertisers or call `apply_to_listing`.
