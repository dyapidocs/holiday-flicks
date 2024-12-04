---
layout: page
---

# Quickstart Guide

Welcome to the Holiday Flicks API Quickstart Guide. This guide will help you make your first API calls and explore the key endpoints.

## Prerequisites

* Verify the JSON server is running by completing instructions in the [API Startup](startup.md) guide.
* Use cURL or Postman to make requests and receive responses.

## Test the API

### Retrieve All Works

Fetch all movies and series in the Holiday Flicks catalogue:

#### Request

```bash
http://localhost:3000/works
```

#### Response

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
    "id": 2,
    "title": "The Count of Monte Cristo",
    "source": "The Count of Monte Cristo (novel)",
    "release_date": "2024",
    "platform": "coming soon",
    "genre": "Adventure",
    "loc_id": 4
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
]
```

### Retrieve a Specific Work

To retrieve details for a specific movie or series, use its `id`. Get the work with `id 1`:

#### Request

```bash
http://localhost:3000/works/1
```

#### Response

```json
{
    "id": 1,
    "title": "All the lights we cannot see",
    "source": "All the lights we cannot see (novel)",
    "release_date": "2023",
    "platform": "Netflix",
    "genre": "historical fiction",
    "loc_id": 1
}
```

### Search Works by Genre

Filter works by genre (e.g., “historical fiction”):

#### Request

```bash
http://localhost:3000/works?genre=historical%20fiction
```

#### Response

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
  }
]
```

## Make a POST Request

### Add a New Work

Add a new movie or series to the catalogue. Replace the placeholders with your data.

#### Request Template

Use this template to `POST` a new movie or series.

```json
{
  "id": null,
  "title": "New Movie",
  "source": "Original Script",
  "release_date": "2024",
  "platform": "Prime",
  "genre": "Drama",
  "loc_id": 2
}
```

For this example, let's add the 1998 movie Ronin, which was filmed in several locations outside of Paris, France. Some filming was done in Paris.

#### Request

```json
{
  "id": null,
  "title": "Ronin",
  "source": "Original Script",
  "release_date": "1998",
  "platform": "Prime, Hulu",
  "genre": "Action Thriller",
  "loc_id": null
}
```

Notice `"loc_id": null`. Once we add the filming location(s) to the JSON database we can then update the Ronin entry in the JSON database with those locations using the PUT command. 

#### Response

```json
{
  "id": 5,
  "title": "Ronin",
  "source": "Original Script",
  "release_date": "1998",
  "platform": "Prime, Hulu",
  "genre": "Action Thriller",
  "loc_id": null
}
```

### Add Location For Ronin

Use the `id` from the `works` you added for the `seen_in` POST. In our example above the `id` is `5` so the  `POST` will use `seen_in: 5`.

#### Request

```json
{
  "id": null,
  "name": "Villefranche-sur-Mer",
  "address": "Various locations",
  "town": "Villefranche-sur-Mer",
  "region": "Provence-Alpes-Côte d'Azur",
  "longitude": "7.312878",
  "latitude": "43.705247",
  "tourist_info": "https://www.villefranche-sur-mer.com/",
  "local_film_office": "contact@villefranche-sur-mer.fr",
  "regional_film_office": "https://www.filmfrance.net/en/plan-your-production/film-commissions/regional-film-commission-provence-alpes-cote-dazur/",
  "seen_in": 5
}
```

#### Response

```json
{
  "id": 5,
  "name": "Villefranche-sur-Mer",
  "address": "Various locations",
  "town": "Villefranche-sur-Mer",
  "region": "Provence Alpes Cote Azur",
  "longitude": "7.312878",
  "latitude": "43.705247",
  "tourist_info": "https://www.villefranche-sur-mer.com/",
  "local_film_office": "contact@villefranche-sur-mer.fr",
  "regional_film_office": "https://www.filmfrance.net/en/film-commissions/provence",
  "seen_in": 5
}
```
## Next Steps

* **Explore More Endpoints:** Check out the API Reference for [/works](api/works.md) or [/locations](api/locations.md) to learn about other available endpoints and functionalities.
* **Explore Tutorials:** Learn how to [Find Movies by Location](tutorials/find_movies_by_location.md) or [Filter Works by Genre or Platform](tutorials/filter_works.md). 
* **Integrate into Applications:** Use these API calls within your applications to provide dynamic content to users.
* **Provide Feedback:** If you have suggestions or encounter issues, please contact us at support@holidayflicks.com.

## Need Help?
- **Support**: Contact us at support@holidayflicks.com.

Happy exploring with the Holiday Flicks API!