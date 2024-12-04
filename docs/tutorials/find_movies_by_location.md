---
layout: page
---

# Tutorial: Find Movies by Location

The Holiday Flicks API allows you to find movies and series based on their filming locations. This tutorial will guide you through the steps to find movies or series that were filmed at a specific location.

## Prerequisites

- **API Key**: Have your API key ready. If not, [obtain an API Key](register_api_key.md).
- **API Base URL**: `http://localhost:3000`

---

## Step 1: Retrieve a List of Locations

First, get a list of all available locations to find the one you are interested in.

### Request Details

- **Method**: `GET`
- **Endpoint**: `/locations`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`

### Example Request

```shell
GET /locations
```

### Expected Response

You should receive a JSON array of location objects:

```json
[
    {
        "id": 1,
        "name": "n/a",
        "address": "n/a",
        "town": "Villefranche-de-Rouergue",
        "region": "Occitanie",
        "longitude": "2.037543",
        "latitude": "44.351762",
        "tourist_info": "https://www.bastides-gorges-aveyron.fr/impregner/villages-caractere/villefranche-de-rouergue/",
        "local_film_office": "secretariat@villefranchederouergue.fr",
        "regional_film_office": "https://www.occitanie-films.fr/commission-du-film-filming-in-occitanie/",
        "seen_in": 1
    },
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
    // more locations
]
```

## Step 2: Find the id of the Desired Location

Suppose you are interested in movies filmed at Etretat Cliffs. From the response, find the id associated with this location.

In the example above, the id for "Etretat Cliffs" is 2.

## Step 3: Retrieve Works Associated with the Location

Use the `loc_id` to find all works filmed at that location.

### Request Details

- **Method**: `GET`
- **Endpoint**: `/works`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Query Parameters**:
  - `loc_id`: `2`

### Example Request

```shell
GET /works?loc_id=2
```

### Expected Response

You should receive a JSON array of works associated with `loc_id` 2:

```json
[
    {
        "id": 4,
        "title": "Lupin",
        "source": "Arsene Lupin",
        "release_date": "2021",
        "platform": "Netflix",
        "genre": "Crime Drama",
        "loc_id": 2
    }
]
```

## Step 4: Explore Additional Details

You can retrieve detailed information about each work or location.

### Retrieve Detailed Information About a Work

#### Request Details

- **Method**: `GET`
- **Endpoint**: `/works/{id}`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Path Parameters**:
  - `id`: `1`

### Example Request

```shell
GET /works/1
```

### Expected Response

```json
{
  "id": 1,
  "title": "All the Lights We Cannot See",
  "source": "All the Lights We Cannot See (novel)",
  "release_date": "2023",
  "platform": "Netflix",
  "genre": "Historical Fiction",
  "loc_id": 2
}
```

## Congratulations

You have successfully used the Holiday Flicks API to find movies and series by location. This is a powerful feature for:

- **Tourists**: Planning visits to filming locations.
- **Film Enthusiasts**: Discovering new works based on filming sites.
- **Industry Professionals**: Researching filming locations and associated works.

## Additional Tip: Combine Filters

When searching for works, you can combine multiple query parameters.

### Example Request

```shell
GET /locations?town=Etretat&region=Normandie
```

### Expected Response

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

## Next Steps

* **Explore More Endpoints:** Check out the API Reference for [/works](../api/works.md) or [/locations](../api/locations.md) to learn about other available endpoints and functionalities.
* **Explore Tutorials:** Learn how to [Find Movies by Location](../tutorials/find_movies_by_location.md) or [Filter Works by Genre or Platform](../tutorials/filter_works.md). 
* **Integrate into Applications:** Use these API calls within your applications to provide dynamic content to users.
* **Provide Feedback:** If you have suggestions or encounter issues, please contact us at support@holidayflicks.com.

## Need Help?
- **Support**: Contact us at support@holidayflicks.com.

Happy exploring with the Holiday Flicks API!
