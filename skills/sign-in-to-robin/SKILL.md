---
name: sign-in-to-robin
description: Start or confirm Robin account linking with `sign_in`. Use when the Robin plugin is active and the user explicitly asks to sign in, connect, link, or access Robin, including its direct sign-in button. Do not use for unrelated sign-in requests; favorite and application skills own their authentication recovery.
---

# Sign in to Robin

1. Call `sign_in` directly and let its OAuth challenge open the host linking flow when needed.
2. Accept `signedIn=true` with a verified token even when optional profile claims are unavailable.
3. Do not invoke search, favorite, profile, or application tools unless the originating user request requires them.
4. On cancellation or failure, stop; never loop or infer that authentication succeeded.

Signing in never contacts an advertiser or changes listings, favorites, applications, or saved search-profile content. Widget route, selection, map, fullscreen, and responsive behavior are owned by the widget and host, not the model.
