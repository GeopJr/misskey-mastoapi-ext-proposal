# Drive

## Entities

### DriveStats

| name | description | type |
| --- | --- | --- |
| `folders_count` | Amount of folders in the root `/` | Int |
| `files_count` | Amount of files in the root `/` | Int |
| `total_folders_count` | Total amount of folders in the drive | Int |
| `total_files_count` | Total amount of files in the drive | Int |
| `used_space` | Amount of space used in bytes | Int |
| `total_space` | Amount of total space in bytes | Int |

### FileProperties

| name | description | type |
| --- | --- | --- |
| `width` | Image width | Int |
| `height` | Image height | Int |

### FileHash

| name | description | type |
| --- | --- | --- |
| `type` | Hash function (like md5) | String |
| `value` | File hash | String |

### File

| name | description | type |
| --- | --- | --- |
| `id` | File ID | String |
| `created_at` | Creation date | String (ISO 8601 Datetime) |
| `name` | File name (with extension) | String |
| `type` | File mime type | String |
| `comment` | File comment or alt text for images | String? |
| `url` | File url | String |
| `thumbnail` | Thumbnail url for images | String? |
| `properties` | File properties for image | FileProperties? |
| `blurhash` | Image blurhash | String? |
| `size` | File size in bytes | Int |
| `sensitive` | Whether the file is marked as NSFW| Bool |
| `hash` | File hash | [] of FileHash |

### Folder

| name | description | type |
| --- | --- | --- |
| `id` | Folder ID | String |
| `created_at` | Creation date | String (ISO 8601 Datetime) |
| `name` | Folder name | String |
| `parent_id` | Folder parent id or null if it's / | String? |
| `folders_count` | Amount of direct child folders | Int |
| `files_count` | Amount of folder child files | Int |

<!-- Should total amount of space taken be listed? -->

## Methods

### `GET` `/api/v1/drive/` - Get stats about your drive

- Auth: ✅

| code | returns |
| --- | --- |
| 200 | `DriveStats` |
| 401 | `{ "error": "The access token is invalid" }` |


### `GET` `/api/v1/drive/folders` - Get all the folders in /

- Auth: ✅

| code | returns |
| --- | --- |
| 200 | [] of `Folder` |
| 401 | `{ "error": "The access token is invalid" }` |

### `GET` `/api/v1/drive/folders/:id` - Get all the folders in folder with `id`

- Auth: ✅
- id: Folder ID

| code | returns |
| --- | --- |
| 200 | [] of `Folder` |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `GET` `/api/v1/drive/files` - Get all the files in /

- Auth: ✅

| code | returns |
| --- | --- |
| 200 | [] of `File` |
| 401 | `{ "error": "The access token is invalid" }` |

### `GET` `/api/v1/drive/files/:id` - Get all the files in folder with `id`

- Auth: ✅
- id: Folder ID

| code | returns |
| --- | --- |
| 200 | [] of `File` |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `POST` `/api/v1/drive/files/` - Upload a file

- Auth: ✅

| name | description | type | required |
| --- | --- | --- | --- |
| file | The file to be uploaded. It MUST have a mime type | multipart/form-data | ✅ |
| folder_id | The folder ID the file should be uploaded to If empty, assume `/`. | String? = null | ❌ |
| sensitive | Whether the file is sensitive / NSFW | Bool = false | ❌ |
| name | File name WITH extension. If null, it will use the one from `file` | String? = null | ❌ |
| description | File comment or alt text for images | String? = null | ❌ |

| code | returns |
| --- | --- |
| 200 | `File` |
| 401 | `{ "error": "The access token is invalid" }` |
| 422 | `{ "error": "Validation failed: File content type is invalid, File is invalid" }` |
| 500 | `{ "error": "Error processing thumbnail for uploaded media" }` |

### `POST` `/api/v1/drive/folders/` - Create a folder

- Auth: ✅

| name | description | type | required |
| --- | --- | --- | --- |
| name | The folder name | String | ✅ |

| code | returns |
| --- | --- |
| 200 | `File` |
| 401 | `{ "error": "The access token is invalid" }` |
| 422 | `{ "error": "Validation failed: File content type is invalid, File is invalid" }` |
| 500 | `{ "error": "Error processing thumbnail for uploaded media" }` |

### `PUT` `/api/v1/drive/files/` - Update a file's metadata

- Auth: ✅

| name | description | type | required |
| --- | --- | --- | --- |
| file_id | The file ID to be updated | multipart/form-data | ✅ |
| folder_id | The folder ID the file should move to. Null to move to `/`. | String? = null | ❌ |
| name |The new file name. Null to leave unchanged | String? = null | ❌ |
| sensitive |The new file sensitivity status. Null to leave unchanged | Bool? = null | ❌ |
| description |The new file comment / alt text. Null to leave unchanged | String? = null | ❌ |

| code | returns |
| --- | --- |
| 200 | `File` |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `PUT` `/api/v1/drive/folder/` - Update a folder's metadata

- Auth: ✅

| name | description | type | required |
| --- | --- | --- | --- |
| folder_id | The folder ID to be updated | multipart/form-data | ✅ |
| name |The new folder name. Null to leave unchanged | String? = null | ❌ |

| code | returns |
| --- | --- |
| 200 | `Folder` |
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `DELETE` `/api/v1/drive/files/:id` - Delete a file

- Auth: ✅
- id: File ID

| code | returns |
| --- | --- |
| 204 |  | <!-- should this be `200 | {}` ? -->
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |

### `DELETE` `/api/v1/drive/folders/:id` - Delete a file

- Auth: ✅
- id: Folder ID to be deleted

| name | description | type | required |
| --- | --- | --- | --- |
| force | Whether to remove non-empty folders | Bool = false | ❌ |

| code | returns |
| --- | --- |
| 204 |  | <!-- should this be `200 | {}` ? -->
| 401 | `{ "error": "The access token is invalid" }` |
| 404 | `{ "error": "Record not found" }` |
| 409 | `{ "error": "Folder is not empty" }` |
