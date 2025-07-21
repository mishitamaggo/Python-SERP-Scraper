This is a Python script that scrapes Google Search organic results using the SerpAPI and saves the results as a CSV file directly to your Google Drive using Google Colab.

Features
Scrapes top 100 Google organic search results for a given keyword.
Uses SerpAPI for reliable Google SERP data.
Saves results in CSV format to Google Drive.
Displays the title, link, and position of each search result.

Setup & Usage
1. Open Google Colab
Use this script in Google Colab to access Google Drive integration and install dependencies.

2. Mount Google Drive
from google.colab import drive
drive.mount('/content/drive')
Follow the authentication link and authorize access.

3. Install Required Libraries
!pip install google-search-results pandas

5. Import Dependencies
from serpapi import GoogleSearch
import pandas as pd

7. Set Your Parameters
params = {
    "q": ["keyword"],  # Replace "keyword" with your actual search query
    # "gl": ["usa"],   # Optional: specify region
    "num": 100,
    "api_key": "YOUR_API_KEY"  # Replace with your SerpAPI key
}

8. Run the Scraper
search = GoogleSearch(params)
results = search.get_dict()
organic_results = results.get("organic_results", [])

10. Save Results to CSV
if organic_results:
    df = pd.DataFrame(organic_results)[['title', 'link', 'position']]
    csv_path = '/content/SERP Results - Sheet1.csv'
    df.to_csv(csv_path, index=False)
    print(f"✅ CSV saved to Google Drive: {csv_path}")
else:
    print("No organic results found to create DataFrame.")
Output
A CSV file with the following columns:
title: Title of the search result
link: URL of the result
position: Ranking position on the SERP

✅ Example Output
title,link,position
"Example Title 1","https://example.com",1
"Example Title 2","https://example2.com",2

Notes
This script only collects organic results. Paid ads, featured snippets, etc., are not included.
Rate limits apply based on your SerpAPI plan.
