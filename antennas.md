# Antennas

## Entities

### Antenna

| name | description | type |
| --- | --- | --- |
| `id` | Antenna ID | String |
| `created_at` | Creation date | String (ISO 8601 Datetime) |
| `name` | Antenna name | String |
| `src` | Antenna source | String ("home" "all" "users" "list" "instances") |
| `list_id` | Antenna source list | String? (only if src is set to "list") |
| `keywords` | Keywords to listen to | [] of String |
| `exclude_keywords` | Keywords to ignore | [] of String |
| `users` | Users to listen to | [] of String or null (only if src is set to "users") |
| `instances` | Instances to listen to | [] of String or null (only if src is set to "instances") |
| `case_sensitive` | Whether the keywords are case sensitive | Bool |
| `notify` | Whether to send notifications on new statuses | Bool |
| `with_replies` | Whether to listen to replies | Bool |
| `only_files` | Whether to only listen to statuses with files | Bool |
| `has_unread_status` | Whether the antenna has new posts | Bool |

## Methods

### `GET` `/api/v1/antennas/` - Get all antennas

- Auth: ✅

| code | returns |
| --- | --- |
| 200 | [] of Antenna |
| 401 | `{ "error": "The access token is invalid" }` |

### `GET` `/api/v1/antennas/:id` - Get antennas with id

- Auth: ✅
- id: Antenna ID

| code | returns |
| --- | --- |
| 200 | Antenna |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `GET` `/api/v1/timelines/antennas/:id` - Get the antenna timeline with id

<!-- This follows the exact same properties as other Mastodon timelines, including ws -->

- Auth: ✅
- id: Antenna ID

| code | returns |
| --- | --- |
| 200 | [] of Status |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `POST` `/api/v1/antennas/` - Create a new antenna

- Auth: ✅

| name | description | type | required |
| --- | --- | --- | --- |
| name | The antenna name | String | ✅ |
| src | The antenna source | String ("home" "all" "users" "list" "instances") | ✅ |
| list_id | The antenna source list (only if src is set to "list") | String | ❌ |
| instances | The antenna source instances (only if src is set to "instances") | [] of String | ❌ |
| users | The antenna source users (only if src is set to "users") | [] of String | ❌ |
| keywords | The antenna keywords to listen to | [] of String = [] | ❌ |
| exclude_keywords | The antenna keywords to listen to | [] of String = [] | ❌ |
| case_sensitive | Whether the keywords are case sensitive | Bool = false | ❌ |
| notify | Whether to send notifications on new statuses | Bool = false | ❌ |
| with_replies | Whether to listen to replies | Bool = false | ❌ |
| only_files | Whether to only listen to statuses with files | Bool = false | ❌ |

| code | returns |
| --- | --- |
| 200 | Antenna |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "List does not exist" }` |
| 404 | `{ "error": "User <user_handle> does not exist" }` |
| 422 | `{ "error": "Validation failed: name can't be blank" }` |
| 422 | `{ "error": "Validation failed: src can't be blank" }` |
| 422 | `{ "error": "Validation failed: unknown src" }` |

### `PUT` `/api/v1/antennas/:id` - Update antenna with id

- Auth: ✅
- id: Antenna ID

| name | description | type | required |
| --- | --- | --- | --- |
| name | The antenna name | String | ✅ |
| src | The antenna source | String ("home" "all" "users" "list" "instances") | ❌ |
| list_id | The antenna source list (only if src is set to "list") | String | ❌ |
| instances | The antenna source instances (only if src is set to "instances") | [] of String | ❌ |
| users | The antenna source users (only if src is set to "users") | [] of String | ❌ |
| keywords | The antenna keywords to listen to | [] of String = [] | ❌ |
| exclude_keywords | The antenna keywords to listen to | [] of String = [] | ❌ |
| case_sensitive | Whether the keywords are case sensitive | Bool = false | ❌ |
| notify | Whether to send notifications on new statuses | Bool = false | ❌ |
| with_replies | Whether to listen to replies | Bool = false | ❌ |
| only_files | Whether to only listen to statuses with files | Bool = false | ❌ |

| code | returns |
| --- | --- |
| 200 | Antenna |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "List does not exist" }` |
| 404 | `{ "error": "User <user_handle> does not exist" }` |
| 422 | `{ "error": "Validation failed: name can't be blank" }` |
| 422 | `{ "error": "Validation failed: unknown src" }` |

### `DELETE` `/api/v1/antennas/:id` - Delete antenna with id

- Auth: ✅
- id: Antenna ID

| code | returns |
| --- | --- |
| 204 |  | <!-- should this be `200 | {}` ? -->
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |
