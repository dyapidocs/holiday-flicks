# API Startup

Follow these instructions before you can use the Holiday Flicks API.

## Prerequisites

* A [GitHub account](https://github.com)
* A development system (PC, Mac, or Linux) running a current or
long-term support (LTS version of the operating system).
* The following software on your development system:
    * [Git](https://docs.github.com/en/get-started/quickstart/set-up-git) (for the command line)
    * [GitHub Desktop](https://desktop.github.com) (optional)
    * A fork of the [Holiday Flicks repo](https://github.com/dyapidocs/holiday-flicks)
    * A current/LTS version of `node.js`
    * A current version of [json-server](https://www.npmjs.com/package/json-server)
    * A current copy of the database file. You can get this by syncing your fork.
    * The [Postman desktop app](https://www.postman.com/downloads/). Because you run the **Holiday Flicks** on your development system with an `http://localhost` hostname, the web-version of Postman cannot perform the exercises.
* cURL installed on your system, which can be used from one of the following:
  * Bash (on Linux, macOS, or Windows with WSL).
  * PowerShell (available on Windows).
  * Command Prompt (on Windows).

## Test the JSON Server

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

## Next Steps

* First time users can start with our [Quickstart Guide](quickstart.md).