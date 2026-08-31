# Robin — Swiss real-estate search for Claude

Robin turns Claude into a Swiss real-estate specialist. Describe what you want in plain
language — property type, location, price, rooms, surface, commute, nearby amenities, even
visual preferences like a modern kitchen or a lake view — and Robin searches semantically
across supported Swiss listings, then renders them on an interactive map and carousel.

Built by [SwissBid GmbH](https://robinreal.ai).

## Install

```
/plugin marketplace add SwissBid/robin-claude-plugin
/plugin install robin@robinreal
```

Once installed, ask "What can Robin do?" to get started.

## What it bundles

A hosted MCP server connection plus six skills that encode the workflows which are easy to
get wrong.

| Skill | Purpose |
|---|---|
| `search-and-show-listings` | Search, then render the map and carousel |
| `show-recommended-listings` | Personalized matches from a saved search profile |
| `save-favorite-listing` | Add or remove a favorite, with safe OAuth recovery |
| `sign-in-to-robin` | Start or confirm Robin account linking |
| `apply-to-listing` | Send one contact request, only on explicit user action |
| `update-search-profile` | Persist a profile, only with explicit consent |
The server exposes eleven tools across search, listing detail, favorites, recommendations,
the personalized search profile, and applications.

## Scope and limits

Limited to the property categories exposed by the search tool schema:
apartments, houses, commercial and industrial property, parking, land, gastronomy and leisure,
agricultural property, secondary rooms, and allotment gardens. 

## Safety design

- **Applications are never automatic.** `apply_to_listing` contacts a real advertiser and
  cannot be recalled. It requires a fresh, explicit Apply action and never replays a draft.
- **The search profile is never written implicitly.** Robin offers a "Create and manage
  profile" card; ignoring it or choosing "Not now" writes nothing.

## Privacy Policy

Robin's privacy policy is at <https://robinreal.ai/datenschutz>.

The plugin sends your search criteria and, once signed in, your account identity to the Robin
MCP server at `mcp.hi-robin.ai` in order to return listings and manage favorites,
recommendations, the personalized search profile, and applications. It does not read your
conversation history, files, or other connectors. Widget images and map tiles load from the
CDNs declared in the server's content-security policy.

Terms of service: <https://robinreal.ai/AGBs> · Support: <https://robinreal.ai/kontakt>

## License

Proprietary. See [LICENSE](LICENSE).
