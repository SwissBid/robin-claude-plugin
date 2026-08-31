---
name: apply-to-listing
description: Send one authenticated contact request for an exact RobinReal or eligible Comparis listing. Use only after the user explicitly asks to apply, send, or contact, including the widget Apply button. This is a destructive external action; do not use for browsing, comparing, favoriting, vague interest, unsupported providers, or unrelated requests.
---

# Apply to a Robin listing

`apply_to_listing` contacts an external advertiser. Never infer consent from interest.

1. Resolve one exact `listing_id` and retain the draft fields.
2. Require an explicit Apply or Send action. Opening a form, searching, viewing, comparing, or favoriting is not consent.
3. Supply only fields requested by the tool. RobinReal uses the verified profile name and email; phone and message are optional. Comparis also requires email, phone, address, city, postal code, message, and verified first and last name.
4. If signed out, retain the listing ID and draft, call `sign_in`, and complete OAuth. Do not submit automatically after sign-in; require a new explicit Apply or Send action, mention to the user to re-initiate the application.
5. After that post-login action and validation, call `apply_to_listing` once.
6. Never retry automatically after a timeout, provider error, ambiguous response, or receipt error: the advertiser may already have received it. Treat `alreadySubmitted=true` as success.
7. On cancellation or failure, clear the pending application. If direct contact is unsupported, direct the user to the original listing page.

Report only the delivery status confirmed by the tool.
