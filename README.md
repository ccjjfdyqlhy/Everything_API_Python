
# Everything_API_Python

A Python API wrapper for interacting with the Everything search engine's HTTP server.  This allows you to programmatically perform searches against your Everything index.

## Features
* Search your Everything index using Python.
* Retrieve results as a list of lists, where each inner list represents a row of search results.
* Simple and easy-to-use API.
* Handles basic error cases like incorrect usage.

## Installation
This script requires Python 3 and the following libraries:
* `requests`: For making HTTP requests.
* `beautifulsoup4`: For parsing HTML content.
Install these using pip:
```bash
pip install requests beautifulsoup4
```

## Usage
### Running the script directly:
```bash
python3 everything_api.py <search_query> <everything_server_ip>
```

* `<search_query>`: The text you want to search for.
* `<everything_server_ip>`: The IP address and port of your Everything HTTP server (e.g., `localhost:7345`, `192.168.1.100:8080`).  Make sure the Everything HTTP server is running and accessible.

**Example:**
```bash
python3 everything_api.py "my document.pdf" localhost:7345
```
### Using the `search()` function:
This function simplifies searching when your Everything server is running on `localhost:7345`.
```python
from everything_api import search

results = search("my document.pdf")
for row in results:
    print(row)
```
**Example within a larger script:**
```python
import everything_api

def find_my_files(keyword):
    results = everything_api.search(keyword)
    # Process the results
    for row in results:
        filepath = row[0]  # Assuming the first element is the file path
        # ... do something with the filepath ...

find_my_files("project report")
```

## Everything HTTP Server Setup
* **Enable HTTP Server:**  In Everything, go to **Tools > Options > HTTP Server** and check "Enable HTTP Server".  Configure the port if needed (default is 7345).  Optionally, set authentication if required.
* **Test the Server:** Open a web browser and navigate to `http://localhost:7345/?search=test` (replace `localhost:7345` with your server address if different). You should see a search results page.

## Return Value
The `findit()` and `search()` functions return a list of lists. Each inner list represents a row in the Everything search results table (excluding the header rows).  The contents of each inner list depend on the columns displayed in your Everything HTTP server configuration.  Typically, the first element is the full file path.

## Note
This script scrapes the HTML output of the Everything HTTP server.  Changes to the Everything HTTP server output format may break this script.
