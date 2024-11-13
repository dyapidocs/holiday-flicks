---
layout: page
---

# Quickstart Guide

Welcome to the Holiday Flicks API Quickstart Guide. This guide will help you make your first API calls and explore the key endpoints.

## Prerequisites

Verify the JSON server is running by completing Step 1 below or refer to [Startup](startup.md) to start the server.

## Step 1: Testing the API with curl

### Retrieve All Works

To fetch all movies and series in the Holiday Flicks catalog, use the following command:

```bash
curl http://localhost:3000/works
```

### Retrieve a Specific Work

To retrieve details for a specific movie or series, use its ID. For example, to get the work with ID 1:

```bash
curl http://localhost:3000/works/1
```

**Expected Response**

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

To filter works by genre (e.g., “historical fiction”), use:

```bash
curl "http://localhost:3000/works?genre=historical%20fiction"
```

## Step 2: Making POST Requests

### Add a New Work

To add a new movie or series to the catalog, use the following command. Make sure to replace the placeholders with your data.

```bash
curl -X POST -H "Content-Type: application/json" -d '{"id": null, "title": "New Movie", "source": "Original Script", "release_date": "2024", "platform": "Prime", "genre": "Drama", "loc_id": 2}' http://localhost:3000/works
```

#### Request

For this example, let's add the 1998 movie Ronin, which was filmed in several locations outside of Paris, France. Note that some filming was done in Paris.

```bash
curl -X POST -H "Content-Type: application/json" -d '{"id": null, "title": "Ronin", "source": "Original Script", "release_date": "1998", "platform": "Prime, Hulu", "genre": "Action Thriller", "loc_id": null}' http://localhost:3000/works
```

Notice `"loc_id": null` in the cURL command. Once we add the filming location(s) to the JSON database we can then update the Ronin entry in the JSON database with those locations using the PUT command. 

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

### Verify Your New Work

You can verify the new work by calling:

```bash
curl http://localhost:3000/works/5
```




### Add Location For Ronin

#### Request

```shell
curl -X POST -H "Content-Type: application/json" -d '{"id": null, "name": "Villefranche-sur-Mer", "address": "Various locations", "town": "Villefranche-sur-Mer", "region": "Provence-Alpes-Côte d'Azur", "longitude": "7.312878", "latitude": "43.705247", "tourist_info": " https://www.villefranche-sur-mer.com/", "local_film_office": "contact@villefranche-sur-mer.fr", "regional_film_office": "https://www.filmfrance.net/en/plan-your-production/film-commissions/regional-film-commission-provence-alpes-cote-dazur/", "seen_in": 5}' http://localhost:3000/locations
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