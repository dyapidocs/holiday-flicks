---
layout: page
---

# Tutorial: Filter Works by Genre or Platform

The Holiday Flicks API allows you to filter movies and series based on various attributes such as genre and platform. This tutorial will guide you through the steps to retrieve works that match specific criteria.

## Prerequisites

- **API Key**: Have your API key ready. If not, [obtain an API Key](register_api_key.md).
- **API Base URL**: `http://localhost:3000`

---

## Understanding Query Parameters

The `/works` endpoint supports query parameters that allow you to filter results based on certain attributes:

- `genre`: Filter works by genre (e.g., `Thriller`, `Drama`).
- `platform`: Filter works by platform (e.g., `Netflix`, `Prime Video`).
- `release_year`: Filter works by release year (e.g., `2021`).
- `loc_id`: Filter works by location ID.

You can combine multiple query parameters to narrow down your search.

## Step 1: Retrieve Works by Genre

Retrieve all works that belong to a specific genre.

### Example: Fetch Works of Genre "Thriller"

#### Request Details

- **Method**: `GET`
- **Endpoint**: `/works`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Query Parameters**:
  - `genre`: `Thriller`

#### Example Request

```shell
GET /works?genre=Thriller
```

#### Expected Response

```json
[
  {
    "id": 3,
    "title": "Stillwater",
    "source": "Original Script",
    "release_date": "2021",
    "platform": "Netflix, Prime Video",
    "genre": "Thriller",
    "loc_id": 3
  },
  {
    "id": 6,
    "title": "Ronin",
    "source": "Original Script",
    "release_date": "1998",
    "platform": "Prime, Hulu",
    "genre": "Thriller",
    "loc_id": 5
  }
  // Additional works...
]
```

## Step 2: Retrieve Works by Platform

You can filter works based on the platform(s) where they are available. Note that with the `platform` field there could be multiple entries, ie. `Netflix, Prime Video`. To search fields that have multiple entries, use `_like` such as `platform_like` in your calls.

### Example: Fetch Works Available on "Netflix"

#### Request Details

- **Method**: `GET`
- **Endpoint**: `/works`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Query Parameters**:
  - `platform`: `Netflix`

### Example Request

```shell
GET /works?platform_like=Netflix
```

### Expected Response

```json
[
    {
        "id": 1,
        "title": "All the lights we cannot see",
        "source": "All the lights we cannot see (novel)",
        "release_date": "2023",
        "platform": "Netflix",
        "genre": "historical fiction",
        "loc_id": 1
    },
    {
        "id": 3,
        "title": "Stillwater",
        "source": "original script",
        "release_date": "2021",
        "platform": "Netflix,Prime",
        "genre": "Thriller",
        "loc_id": 3
    },
    {
        "id": 4,
        "title": "Lupin",
        "source": "Arsene Lupin",
        "release_date": "2021",
        "platform": "Netflix",
        "genre": "Crime Drama",
        "loc_id": 2
    }
  // Additional works...
]
```

## Step 3: Combining Filters

You can combine multiple query parameters to refine your search further.

### Example: Fetch "Thriller" Works Available on "Netflix"

#### Request Details

- **Method**: `GET`
- **Endpoint**: `/works`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Query Parameters**:
  - `genre`: `Thriller`
  - `platform`: `Netflix`

### Example Request

```shell
GET /works?genre=Thriller&platform_like=Netflix
```

### Expected Response

```json
[
  {
    "id": 3,
    "title": "Stillwater",
    "source": "Original Script",
    "release_date": "2021",
    "platform": "Netflix, Prime Video",
    "genre": "Thriller",
    "loc_id": 3
  }
]
```

## Step 4: Filtering by Release Year

You can also filter works based on their release year.

### Example: Fetch Works Released in "2021"

#### Request Details

- **Method**: `GET`
- **Endpoint**: `/works`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Query Parameters**:
  - `release_date`: `2021`

### Example Request

```shell
GET /works?release_date=2021
```

### Expected Response

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
    },
    {
        "id": 4,
        "title": "Lupin",
        "source": "Arsene Lupin",
        "release_date": "2021",
        "platform": "Netflix",
        "genre": "Crime Drama",
        "loc_id": 2
    }
  // Additional works...
]
```

## Step 5: Advanced Filtering

Combine multiple filters to narrow down the results even further.

### Example: Fetch "Thriller" Works Available on "Netflix" Released in "2021"

#### Request Details

- **Method**: `GET`
- **Endpoint**: `/works`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Query Parameters**:
  - `genre`: `Thriller`
  - `platform`: `Netflix`
  - `release_date`: `2021`

### Example Request

```shell
GET /works?genre=Thriller&platform_like=Netflix&release_date=2021
```

### Expected Response

```json
[
  {
    "id": 3,
    "title": "Stillwater",
    "source": "Original Script",
    "release_date": "2021",
    "platform": "Netflix, Prime Video",
    "genre": "Thriller",
    "loc_id": 3
  }
]
```

## Notes on Filtering

* **Case Sensitivity:** The API treats query parameter values as case-insensitive. For example, `Thriller` and `thriller` will not return the same results.
* **Partial Matches:** The API does not support partial matches for query parameters. The value must match exactly.
* **Multiple Values:** If a field contains multiple values (e.g., `"platform": "Netflix, Prime Video"`), the API will return works if any of the platforms match the query when `_like` is appended to the field name such as `platform_like`.

## Handling No Results

If no works match the provided filters, the API will return an empty array.

### Example

#### Example Request

```bash
GET /works?genre=Sci-Fi&platform_like=HBO
```

#### Example Response

```json
[]
```

## Congratulations

You have learned how to filter works by genre, platform, and release year using the Holiday Flicks API. By combining query parameters, you can refine your searches to find exactly what you're looking for.

## Next Steps

* **Explore More Endpoints:** Check out the API Reference for [/works](../api/works.md) or [/locations](../api/locations.md) to learn about other available endpoints and functionalities.
* **Explore Tutorials:** Learn how to [Find Movies by Location](../tutorials/find_movies_by_location.md) or [Filter Works by Genre or Platform](../tutorials/filter_works.md). 
* **Integrate into Applications:** Use these API calls within your applications to provide dynamic content to users.
* **Provide Feedback:** If you have suggestions or encounter issues, please contact us at support@holidayflicks.com.

## Need Help?
- **Support**: Contact us at support@holidayflicks.com.

Happy exploring with the Holiday Flicks API!