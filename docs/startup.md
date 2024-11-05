[Back to Overview](index.md)

# Test the JSON Server

The goal here is to start the JSON server, test to see that it is running, and make a test call using cURL to see if you get a response.

1. Navigate to the `holiday-flicks/api` directory.

2. Start the JSON Server by running:

    ```shell
    json-server -w holiday_flicks_db.json
    ```

    You should see the following if successful:

    ```shell
    Loading holiday_flicks_db.json
    Done

    Resources
    http://localhost:3000/works
    http://localhost:3000/locations

    Home
    http://localhost:3000

    Type s + enter at any time to create a snapshot of the database
    Watching...
    ```

3. Make a test call for resource `works` with ID `1`:

    ```shell
    curl http://localhost:3000/works/1
    ```

    You should see the following if successful:

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
