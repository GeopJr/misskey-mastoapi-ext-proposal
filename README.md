# Misskey <=> Mastodon API compat extensions

This is an attempt and proposal at a universal Misskey MastoAPI compat extension across the multiple forks that implement it. The goal is to help clients that are willing to implement features unique to Misskey without having them support a completely different API.

# Roadmap

- [ ] Drive
- [ ] Clips
- [ ] Antennas
- [ ] Pages
- [ ] Channels
- [ ] Gallery
- [ ] Groups
- [ ] Chat
- [ ] Admin API
- [ ] MastoAPI addons (timelines, entity properties...)

# Notes

- `Drive` is the most important one as the others depend on it, however, it should not replace the `/api/v2/media` API. MastoAPI should use that (ex. for statuses) and not Drive ids (unless they match).
- Be as abstract as possible to allow future extensions. For example, if there's a `md5` => String key, change it to `hash` => [] of {"type" => String}. That would allow future changes to it without changing the spec or having all forks agree on one: `"hash": [{"md5": "..."}, {"sha1": "..."}]`.
- `[] of Type` = Array of Type. `Type?` = Nullable type. `Type = Value` = default value for `Type` is `Value`.
- Error codes should follow Mastodon's.
- Use appropriate HTTP methods. (https://docs.joinmastodon.org/client/intro/#http)
- Support JSON, form-data and query strings for providing parameters. (https://docs.joinmastodon.org/client/intro/#parameters)
- The server should do most of the work. SSR statuses, pages, user profiles when possible.
