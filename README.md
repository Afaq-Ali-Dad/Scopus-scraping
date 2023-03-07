# Scopus-scraping
With this code you can get required information about the author in scopus database using author's ID. You must have Elsevier developer active API for that.

Here is the code

import requests
import json

# Ask the user for the author last name
author_id = input("Enter Author ID: ")

# Scopus API endpoint and headers
url = f"https://api.elsevier.com/content/search/author?query=AU-ID({author_id})"
headers = {
    "Accept": "application/json",
    "X-ELS-APIKey": "API"
}
params = {'query = "AU-ID({author_id}"'}
# Send the request and get the response
response = requests.get(url, headers=headers)

# Parse the JSON data
data = json.loads(response.text)

# Extract the relevant information
author_name = data["search-results"]["entry"][0]["preferred-name"]["surname"]
affiliation = data["search-results"]["entry"][0]["affiliation-current"]["affiliation-name"]
document_count = data["search-results"]["opensearch:totalResults"]
#subject_areas = data["search-results"]["entry"][0]["subject-areas"]["subject-names"]
#citedby_count = data["search-results"]["entry"][0]["citedby-count"]

# Print the information
print(f"Author name: {author_name}")
print(f"Affiliation: {affiliation}")
print(f"Document count: {document_count}")
#print(f"Subject areas: {subject_areas}")
#print(f"Cited by count: {citedby_count}")
