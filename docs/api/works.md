---
layout: page
---

# API Reference: Works Resource

The `works` resource represents movies and series in the Holiday Flicks API catalogue. This reference provides detailed information on the available endpoints, parameters, request and response formats, and the data model for `works`.

## Endpoints Overview

- **GET `/works`** - Retrieve a list of all works.
- **GET `/works/{id}`** - Retrieve details of a specific work by ID.
- **POST `/works`** - Create a new work entry.
- **PUT `/works/{id}`** - Update an existing work.
- **DELETE `/works/{id}`** - Delete a work entry.

## Authentication

All requests to the `works` resource require an API key included in the `Authorization` header.

**Header Format**

```makefile
Authorization: Bearer YOUR_API_KEY
```

## Endpoint Details

### 1. GET `/works`

Retrieves a list of all works in the catalogue.

**Query Parameters (Optional)**

- `genre` (string): Filter works by genre.
- `release_year` (integer): Filter works by release year (e.g., `2021`).
- `platform` (string): Filter works by platform (e.g., `Netflix`).
- `loc_id` (integer): Filter works by location ID.

**Example Request**

```bash
GET /works?genre=Thriller&platform=Netflix
```

**Example cURL**

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
"https://api.holidayflicks.com/v1/works?genre=Thriller&platform=Netflix"
```

**Example Response**

```json
[
  {
    "id": 3,
    "title": "Stillwater",
    "source": "original script",
    "release_date": "2021",
    "platform": "Netflix,Prime",
    "genre": "Thriller",
    "loc_id": 3
  }
]
```

### 2. GET `/works/{id}`

Retrieves detailed information about a specific work by its ID.

**Path Parameters**

- `id` (integer): The unique identifier of the work.

**Example Request**

```bash
GET /works/2
```

**Example cURL**

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
"https://api.holidayflicks.com/v1/works/2"
```

**Example Response**

```json
{
  "id": 2,
  "title": "The Count of Monte Cristo",
  "source": "The Count of Monte Cristo (novel)",
  "release_date": "2024",
  "platform": "coming soon",
  "genre": "Adventure",
  "loc_id": 4
}
```

### 3. POST `/works`

Creates a new work entry in the catalogue.

**Request Headers**

- `Content-Type`: application/json
- `Authorization`: Bearer YOUR_API_KEY

**Request Body (JSON)**

| Field         | Type    | Required | Description                                 |
|---------------|---------|----------|---------------------------------------------|
| `title`       | string  | Yes      | Title of the work.                          |
| `source`      | string  | Yes      | Origin of the work (e.g., novel, script).   |
| `release_date`| string  | Yes      | Release year (YYYY format).                 |
| `platform`    | string  | Yes      | Platforms where the work is available.      |
| `genre`       | string  | Yes      | Genre of the work.                          |
| `loc_id`      | integer | Yes      | ID of the associated location (locations.id). |

**Example Request**

```json
{
  "title": "New Movie Title",
  "source": "Original Script",
  "release_date": "2025",
  "platform": "Netflix",
  "genre": "Drama",
  "loc_id": 5
}
```

**Example cURL**

```bash
curl -X POST -H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "title": "New Movie Title",
  "source": "Original Script",
  "release_date": "2025",
  "platform": "Netflix",
  "genre": "Drama",
  "loc_id": 5
}' \
"https://api.holidayflicks.com/v1/works"
```

**Example Response**

_Status Code: 201 Created_

```json
{
  "id": 5,
  "title": "New Movie Title",
  "source": "Original Script",
  "release_date": "2025",
  "platform": "Netflix",
  "genre": "Drama",
  "loc_id": 5
}
```

### 4. PUT `/works/{id}`

Updates an existing work entry.

**Path Parameters**

- `id` (integer): The unique identifier of the work to update.

**Request Headers**

- `Content-Type`: application/json
- `Authorization`: Bearer YOUR_API_KEY

**Request Body (JSON)**

Include only the fields you wish to update.

**Example Request**

```json
{
  "platform": "Netflix, Prime Video",
  "release_date": "2021"
}
```

**Example cURL**

```bash
curl -X PUT -H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "platform": "Netflix, Prime Video",
  "release_date": "2021"
}' \
"https://api.holidayflicks.com/v1/works/3"
```

**Example Response**

_Status Code: 200 OK_

```json
{
  "id": 3,
  "title": "Stillwater",
  "source": "original script",
  "release_date": "2021",
  "platform": "Netflix, Prime Video",
  "genre": "Thriller",
  "loc_id": 3
}
```

### 5. DELETE `/works/{id}`

Deletes a work entry from the catalogue.

**Path Parameters**

- `id` (integer): The unique identifier of the work to delete.

**Example Request**

```bash
DELETE /works/5
```

**Example cURL**

```bash
curl -X DELETE -H "Authorization: Bearer YOUR_API_KEY" \
"https://api.holidayflicks.com/v1/works/5"
```

**Example Response**

_Status Code: 204 No Content_

No body is returned.

---

## Data Model: Work Object

The Work object represents a movie or series in the catalogue.

| Field         | Type    | Description                                         |
|---------------|---------|-----------------------------------------------------|
| `id`          | integer | Unique identifier for the work.                     |
| `title`       | string  | Title of the movie or series.                       |
| `source`      | string  | Origin (e.g., original script, novel).              |
| `release_date`| string  | Release year in YYYY format.                        |
| `platform`    | string  | Platforms where the work is available.              |
| `genre`       | string  | Genre of the work (e.g., Thriller, Adventure).      |
| `loc_id`      | integer | ID of the associated location (locations.id).       |

## Common Response Codes

- **200 OK**: Request succeeded.
- **201 Created**: Resource successfully created.
- **204 No Content**: Resource successfully deleted.
- **400 Bad Request**: Invalid request parameters.
- **401 Unauthorized**: Authentication failed or not provided.
- **404 Not Found**: Resource not found.
- **500 Internal Server Error**: Server encountered an error.

## Error Handling

Errors are returned in JSON format with an error object.

**Error Response Format**

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Detailed error message."
  }
}
```

**Example of a 404 Error**

```json
{
  "error": {
    "code": "NOT_FOUND",
    "message": "The requested work with id 999 does not exist."
  }
}
```

---

## Notes

- **Pagination**: If the number of works is large, pagination parameters such as `page` and `limit` may be supported (check the API for details).
- **Data Validation**: All required fields should be provided and correctly formatted when creating or updating resources.
- **Rate Limiting**: Be aware of any rate limits applied to the API to prevent exceeding allowed usage.

---

## Examples in Different Programming Languages

### Fetching All Works Using Python

```python
import requests

headers = {
    'Authorization': 'Bearer YOUR_API_KEY'
}

response = requests.get('https://api.holidayflicks.com/v1/works', headers=headers)
works = response.json()

for work in works:
    print(f"{work['title']} ({work['release_date']}) - Genre: {work['genre']}")
```

### Fetching a Specific Work Using JavaScript (Fetch API)

```javascript
fetch('https://api.holidayflicks.com/v1/works/2', {
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY'
  }
})
.then(response => response.json())
.then(work => {
  console.log(`${work.title} (${work.release_date}) - Genre: ${work.genre}`);
})
.catch(error => console.error('Error:', error));
```