---
layout: page
---

# API Reference: Locations Resource

The `locations` resource represents filming locations featured in the Holiday Flicks API catalogue. This reference provides detailed information on the available endpoints, parameters, request and response formats, and the data model for `locations`.

## Endpoints Overview

- [**GET `/locations`**](#get-locations) - Retrieve a list of all locations.
- [**GET `/locations/{id}`**](#get-locationsid) - Retrieve details of a specific location by ID.
- [**POST `/locations`**](#post-locations) - Create a new location entry.
- [**PUT `/locations/{id}`**](#put-locationsid) - Update an existing location.
- [**DELETE `/locations/{id}`**](#delete-locationsid) - Delete a location entry.

## Authentication

All requests to the `locations` resource require an API key included in the `Authorization` header.

**Header Format**

```makefile
Authorization: Bearer YOUR_API_KEY
```

## Endpoint Details

### GET `/locations`

Retrieves a list of all locations in the catalogue.

**Query Parameters (Optional)**

- `region` (string): Filter locations by region.
- `town` (string): Filter locations by town.
- `name` (string): Filter locations by name.

**Example Request**

```bash
GET /locations?region=Normandie
```

**Example Response**

```json
[
  {
    "id": 2,
    "name": "Etretat Cliffs",
    "address": "n/a",
    "town": "Etretat",
    "region": "Normandie",
    "longitude": "0.195154",
    "latitude": "49.706429",
    "tourist_info": "https://en.normandie-tourisme.fr/professionals/office-de-tourisme-detretat/",
    "local_film_office": "n/a",
    "regional_film_office": "https://www.normandieimages.fr/",
    "seen_in": 1
  }
]
```

### GET `/locations/{id}`

Retrieves detailed information about a specific location by its ID.

**Path Parameters**

- `id` (integer): The unique identifier of the location.

**Example Request**

```bash
GET /locations/3
```

**Example Response**

```json
{
  "id": 3,
  "name": "les Goudes",
  "address": "n/a",
  "town": "13008 Marseille",
  "region": "Provence-Alpes-Côte d'Azur",
  "longitude": "5.347584",
  "latitude": "43.215314",
  "tourist_info": "https://www.marseille-tourisme.com/en/discover-marseille/culture-heritage/the-districts-of-marseille/les-goudes-village/",
  "local_film_office": "https://www.filmfrance.net/en/plan-your-production/film-commissions/marseille-film-commission",
  "regional_film_office": "https://www.filmfrance.net/en/plan-your-production/film-commissions/regional-film-commission-provence-alpes-cote-dazur/",
  "seen_in": 3
}
```

### POST `/locations`

Creates a new location entry in the catalogue.

**Request Headers**

- `Content-Type`: application/json
- `Authorization`: Bearer YOUR_API_KEY

**Fields:** Refer to the [Data Model: Location Object](#data-model-location-object) table for fields.

**Example Request**

```json
{
  "name": "New Location Name",
  "address": "123 Example St.",
  "town": "Example Town",
  "region": "Example Region",
  "longitude": "0.000000",
  "latitude": "0.000000",
  "tourist_info": "https://example.com/tourist-info",
  "local_film_office": "contact@example.com",
  "regional_film_office": "https://example.com/regional-film-office",
  "seen_in": 5
}
```

**Example Response**

```bash
Status Code: 201 Created
```

```json
{
  "id": 6,
  "name": "New Location Name",
  "address": "123 Example St.",
  "town": "Example Town",
  "region": "Example Region",
  "longitude": "0.000000",
  "latitude": "0.000000",
  "tourist_info": "https://example.com/tourist-info",
  "local_film_office": "contact@example.com",
  "regional_film_office": "https://example.com/regional-film-office",
  "seen_in": 5
}
```

### PUT `/locations/{id}`

Updates an existing location entry.

**Path Parameters**

- `id` (integer): The unique identifier of the location to update.

**Request Headers**

- `Content-Type`: application/json
- `Authorization`: Bearer YOUR_API_KEY

**Request Body (JSON)**

Include only the fields you wish to update.

**Example Request**

```json
{
  "tourist_info": "https://updated-example.com/tourist-info"
}
```

**Example Response**

```bash
Status Code: 200 OK
```

```json
{
  "id": 6,
  "name": "New Location Name",
  "address": "123 Example St.",
  "town": "Example Town",
  "region": "Example Region",
  "longitude": "0.000000",
  "latitude": "0.000000",
  "tourist_info": "https://updated-example.com/tourist-info",
  "local_film_office": "contact@example.com",
  "regional_film_office": "https://example.com/regional-film-office",
  "seen_in": 5
}
```

### DELETE `/locations/{id}`

Deletes a location entry from the catalogue.

**Path Parameters**

- `id` (integer): The unique identifier of the location to delete.

**Example Request**

```bash
DELETE /locations/6
```

**Example Response**

```bash
Status Code: 204 No Content
```

No body is returned.

## Data Model: Location Object

The Location object represents a filming location in the catalogue.

| Field                 | Type    | Description                                         |
|-----------------------|---------|-----------------------------------------------------|
| `id`                  | integer | Unique identifier for the location. Generated by the server. |
| `name`                | string  | Name of the specific location or site.              |
| `address`             | string  | Street address of the location.                     |
| `town`                | string  | Town or city where the location is situated.        |
| `region`              | string  | Administrative region of the location.              |
| `longitude`           | string  | Longitude coordinate (decimal degrees).             |
| `latitude`            | string  | Latitude coordinate (decimal degrees).              |
| `tourist_info`        | string  | URL to local tourist information.                   |
| `local_film_office`   | string  | Contact information for the local film office.      |
| `regional_film_office` | string  | URL to the regional film office.                    |
| `seen_in`             | integer | ID of the associated work (works:id).               |

### Field Requirements

- **POST `/locations`:** 
  - **Required Fields:** `name`, `town`, `region`, `longitude`, `latitude`, `seen_in`
  - **Optional Fields:** `address`, `tourist_info`, `local_film_office`, `regional_film_office`
  
- **PUT `/locations/{id}`:** 
  - **All fields are optional.** You can update any subset of the fields as needed.

### Notes

- The `id` field is auto-generated by the server and should **not** be included in the request body.
- The `seen_in` field must correspond to an existing `works:id` field, meaning the `id` of the associated work.
- Ensure that all **required** fields are provided and correctly formatted when creating resources.
- Latitude and longitude should be provided in decimal degrees format (e.g., `"longitude": "5.347584"`).

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
    "message": "The requested location with id 999 does not exist."
  }
}
```

## Notes

- **Pagination**: If the number of locations is large, pagination parameters such as `page` and `limit` may be supported (check the API for details).
- **Data Validation**: All required fields should be provided and correctly formatted when creating or updating resources.
- **Rate Limiting**: Be aware of any rate limits applied to the API to prevent exceeding allowed usage.

## Examples in Different Programming Languages

### Fetching All Locations Using Python

```python
import requests

headers = {
    'Authorization': 'Bearer YOUR_API_KEY'
}

response = requests.get('https://api.holidayflicks.com/v1/locations', headers=headers)
locations = response.json()

for location in locations:
    print(f"{location['name']} in {location['town']}, {location['region']}")
```

### Fetching a Specific Location Using JavaScript (Fetch API)

```javascript
fetch('https://api.holidayflicks.com/v1/locations/2', {
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY'
  }
})
.then(response => response.json())
.then(location => {
  console.log(`${location.name} located at ${location.latitude}, ${location.longitude}`);
})
.catch(error => console.error('Error:', error));
```

* **Explore More Endpoints:** Check out the API Reference for [/works](../api/works.md) or [/locations](../api/locations.md) to learn about other available endpoints and functionalities.
* **Explore Tutorials:** Learn how to [Find Movies by Location](../tutorials/find_movies_by_location.md) or [Filter Works by Genre or Platform](../tutorials/filter_works.md).