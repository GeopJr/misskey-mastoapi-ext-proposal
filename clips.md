# Clips

## Entities

### Clip

| name | description | type |
| --- | --- | --- |
| `id` | Clip ID | String |
| `created_at` | Creation date | String (ISO 8601 Datetime) |
| `account` | Author's account | Account |
| `name` | Clip name | String |
| `description` | Clip description | String? |
| `public` | Whether the clip is public | Bool |

## Methods

### `GET` `/api/v1/clips/` - Get all clips

- Auth: ✅

| code | returns |
| --- | --- |
| 200 | [] of Clip |
| 401 | `{ "error": "The access token is invalid" }` |

### `GET` `/api/v1/clips/:id` - Get clip with id

- Auth: ✅
- id: Clip ID

| code | returns |
| --- | --- |
| 200 | Clip |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `GET` `/api/v1/clips/:id/statuses` - Get statuses in clip with id

- Auth: ✅
- id: Clip ID

| code | returns |
| --- | --- |
| 200 | [] of Status |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `POST` `/api/v1/clips/` - Create a new clip

- Auth: ✅

| name | description | type | required |
| --- | --- | --- | --- |
| name | The clip name | String | ✅ |
| description | The clip description | String? = null | ❌ |
| public | Whether the clip is public | Bool? = false | ❌ |

| code | returns |
| --- | --- |
| 200 | `Clip` |
| 401 | `{ "error": "The access token is invalid" }` |
| 422 | `{ "error": "Validation failed: Name can't be blank" }` |

### `POST` `/api/v1/clips/:id/statuses` - Add statuses to clip with id

- Auth: ✅
- id: Clip ID

| name | description | type | required |
| --- | --- | --- | --- |
| status_ids | Array of statuses to add to clip | [] of String | ✅ |

| code | returns |
| --- | --- |
| 204 |  | <!-- should this be `200 | {}` ? -->
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |
| 422 | `{ "error": "Validation failed: Status already in clip" }` |

### `PUT` `/api/v1/clips/:id` - Update clip with id

- Auth: ✅
- id: Clip ID

| name | description | type | required |
| --- | --- | --- | --- |
| name | The new clip name | String | ✅ |
| description | The new clip description | String? = null | ❌ |
| public | Whether the clip is now public | Bool? = false | ❌ |

| code | returns |
| --- | --- |
| 200 | Clip |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `DELETE` `/api/v1/clips/:id` - Delete clip with id

- Auth: ✅
- id: Clip ID

| code | returns |
| --- | --- |
| 204 |  | <!-- should this be `200 | {}` ? -->
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |


### `DELETE` `/api/v1/clips/:id/statuses` - Remove statuses from clip with id

- Auth: ✅
- id: Clip ID

| name | description | type | required |
| --- | --- | --- | --- |
| status_ids | Array of statuses to remove from clip | [] of String | ✅ |

| code | returns |
| --- | --- |
| 204 |  | <!-- should this be `200 | {}` ? -->
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |
