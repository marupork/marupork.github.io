# API Blueprint

[<<](../)

## APIB to HTML

1. Install [aglio](https://github.com/danielgtaylor/aglio) via npm

    ```console
    npm install -g aglio
    ```

1. Generate html based on apib

    ```console
    aglio -i input.apib --theme-template triple -o output.html
    ```

## Mock APIB

### Using drakov

1. Install [drakov](https://www.npmjs.com/package/drakov) via npm
   - `Prerequisite:` Python is available on path
      - Use existing python on path

        ```console
        npm config set python "C:\Program Files\IBM\SPSS\Statistics\25\Python3\python.exe"

        npm install -g drakov --force --python="C:\Program Files\IBM\SPSS\Statistics\25\Python3\python.exe"
        ```

      - Download [Windows x86-64 embeddable zip file](https://www.python.org/downloads/release/python-382/)

        ```console
        npm install -g drakov --force --python="~\python-3.8.2-embed-amd64\python.exe"
        ```

1. Create file: *hello.apib*

    ```md
    FORMAT: 1A

    # Example API

    hello world

    ## Message [/messages]

    ### Get Message [GET]

    + Response 200 (application/json)

            {
              "message": "Hello World!"
            }
    ```

1. Mock server

    ```console
    $ drakov -f ./hello.apib -p 3000
    [INFO] No configuration files found
    [INFO] Loading configuration from CLI
   DRAKOV STARTED
    [LOG] Setup Route: GET /messages Get Message
   Drakov 1.0.4      Listening on port 3000
    ```

1. Access mock endpoint

    ```console
    $ curl http://localhost:3000/messages
    {
        "message": "Hello World!"
    }
    ```

## References

- [API Blueprint Tutorial](https://apiblueprint.org/documentation/tutorial.html)
- [API Blueprint Tools](https://apiblueprint.org/tools.html)
- [Medium: Using API Blueprint To Build Your API Documentations](https://medium.com/@songofcode/using-api-blueprint-to-build-your-api-documentations-16ecd2c2cc07)
- [curl.haxx.se: Using curl to automate HTTP jobs](https://curl.haxx.se/docs/httpscripting.html)

[<<](../)
