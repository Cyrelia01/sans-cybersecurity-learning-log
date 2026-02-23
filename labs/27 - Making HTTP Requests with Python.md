Making HTTP Requests with Python

## Objective

Use Python’s requests library to perform HTTP GET requests against a locally hosted web application, retrieve page content, interpret response objects, and extract structured JSON data.

## Environment
- Lab-based Linux container environment
- Python interpreter (python / python3)
- requests library
- Local web service running at:
-   http://localhost
- JSON endpoint:
-   http://localhost/secret.json

## Walkthrough

### Phase 1 – Performing a Basic HTTP GET Request

```Python
import requests

page = requests.get("http://localhost")
print(page)
```

The requests library simplifies sending HTTP requests in Python.

Running:

```Python
python output.py

<Response [200]>
```

<Response [200]> indicates a successful HTTP request. At this stage, only the response object was printed — not the actual content of the page.

### Phase 2 – Retrieving Raw Page Content

The last line was modified to:

```print(page.content)```

Running the program produced:

```b'<HTML><HEAD><TITLE>***** - sensitive</TITLE></HEAD>\n  <BODY>\n***** - sensitive\n    </BODY>\n    </HTML>\n'```

The b prefix indicates the response is returned as raw bytes.

The \n characters represent newline characters.

Formatting is not automatically interpreted when printing byte content.

### Phase 3 – Displaying Formatted Text

To properly render the HTML formatting, the code was updated to:

```print(page.text)```

Output:

```Python
<HTML><HEAD><TITLE>***** - sensitive</TITLE></HEAD>
  <BODY>
***** - sensitive
    </BODY>
    </HTML>
```

Key Difference

```page.content``` → Returns raw byte data.

```page.text``` → Decodes the content into readable text format.

Using .text respects formatting and removes the raw byte prefix.

### Phase 4 – Retrieving JSON Data

The lab included a JSON endpoint at:

```http://localhost/secret.json```

The code was modified to:

```Python
page = requests.get("http://localhost/secret.json")
print(page.text)
```

Output:

```Python
python output.py

{"login": "***** - sensitive", "id": *****, "url": "***** - sensitive", "type": "User", "name": "***** - sensitive"}
```

This confirms that JSON responses are transmitted as text over HTTP.

### Phase 5 – Parsing JSON and Accessing Specific Data

To extract a specific value from the JSON response, the final line was modified to:

```print(page.json()['name'])```

Running the program displayed successful results, which are not shared here due to SANS requirements.

```page.json()``` converts the response body into a Python dictionary.

```['name']``` accesses the value associated with the name key.

This allows structured access instead of manually parsing text.

## Key Concepts 
- HTTP GET requests can be performed easily using the requests library
- Status code 200 indicates successful communication
- ```.content``` returns raw byte data
- ```.text``` returns decoded string content
- ```.json()``` converts JSON responses into Python dictionaries
- Structured data can be accessed using dictionary key indexing

## Conclusion

The ability to automate HTTP interactions is foundational for tasks such as API integration, automation, data retrieval, and security testing workflows.
