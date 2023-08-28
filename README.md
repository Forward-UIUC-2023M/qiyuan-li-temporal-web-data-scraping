# qiyuan-li-temporal-web-data-scraping

# Temporal Web Data Scraping

## Overview

This module is designed to scrape faculty information from university department web pages and their historical versions archived on the Wayback Machine. Utilizing libraries like Selenium and urllib, it automates a Google search to identify potential faculty list URLs, filters and ranks these URLs based on their structure and relevance, and then fetches the actual faculty data. The script uses machine learning models for accuracy and writes the results to text files for each university and department combination. It aims to provide a comprehensive and historical view of faculty members in specified university departments.

## Setup

1. Install Python 3.10.7 64-bit.

2. Install dependencies.

```
pip3 install -r requirements.txt
pip3 install pandas
pip3 install sklearn
pip3 install nltk
pip3 install selenium
```

3. Run tests
```
 // running the following command should print a list of department names
 python3 department/algorithm.py

 // running the following command should print a list of faculty info
 python3 faculty/algorithm.py
```

4. Important functions
```bash
qiyuan-li-education-today/
├── api.py								# the backend for the UI
├── Faculty URL Dataset.csv						# the csv file with training data (faculty and non-faculty URLs)
├── data								# faculty info already collected
├── department
│   ├── algorithm.py
│   ├── find_possible_list_department.py     # main functions here
├── faculty
│   ├── algorithm.py
│   ├── annotator			# annotate text elements on a webpage
│   ├── trained_model.py	# machine learning model that trains the faculty data
│   ├── get_historical_faculty_urls.py	# get the historical urls from 2000 to 2023 given a specific university department
│   ├── get_data_from_multiple_lists.py       # main functions here
│   ├── get_data_from_multiple_lists_with_old_classifier.py   *
│   ├── LinkedIn
│   │   ├── get_background.py
│   │   ├── get_linkedin_data.py
│   ├── Orcid
            └── get_orcid_data.py

* Very similar to get_data_from_multiple_lists.py except it is using a classifier instead of an annotator to annotate text elements
```

## Functional Design (Usage)
## Demo video

https://drive.google.com/file/d/1y-LZYx3ODr1UBbjsEqHZeC-Q59nUg-qe/view?usp=drive_link

## Algorithmic Design for Advanced Web Scraping of Academic Faculty Data
The following algorithmic design outlines the architecture and functioning of an advanced web scraping tool for collecting academic faculty data over a time range from 2000 to 2023.

##### 1. Modules and Dependencies
Python Standard Libraries: time, math, re, json, datetime, collections, urllib.request, sys, pickle
Third-Party Libraries: requests, selenium
##### 2. Key Files
algorithm.py - Main script that initiates the web scraping process.
get_historical_faculty_urls.py - Contains functions for URL selection and processing.
##### 3. Workflow
##### Step 1: Initialization
Initialize variables such as university, department, and forbidden (list of strings to ignore while searching URLs).
##### Step 2: Find Possible URLs
Construct a Google Search query URL.
Make an HTTP request to fetch search results.
Parse the HTML to find relevant URLs.
Filter out URLs containing forbidden words like 'google', 'wiki', etc.
##### Step 3: URL Pre-processing and Historical Data Collection
Identify the base URL of the department.
Generate a list of likely faculty listing URLs based on predefined common URL patterns and Web Archive data.
Extract historical URLs from the Web Archive based on the generated list.
##### Step 4: Rank and Filter URLs
Calculate the Levenshtein distance for each URL to rank them.
Select the best URLs for each year from 2000 to 2023.
Save these URLs into a text file.
##### Step 5: View HTML Structure and Scrape Data
Visit each URL in a web browser automated by Selenium.
Scrape faculty information and save it for further processing.
##### 4. Key Functions in algorithm.py
find(university, department):
This is the main function that initializes the scraping process. It calls various utility functions to find, process, and rank URLs.
##### 5. Key Functions in get_historical_faculty_urls.py
levenshtein_distance(s1, s2):
Computes the Levenshtein distance between two strings.
process_link(link):
Extracts a snippet from a URL for further comparison.
group_possible_faculty_urls_by_year(lines):
Groups URLs by the year of archive.
get_best_urls_of_each_year(...):
Selects the best URLs for each year based on several criteria.
save_best_urls_of_each_year(url_text_file_name, new_urls):
Saves the selected URLs into a text file.
get_url_list(filename, new_urls):
Writes the faculty data scraped from the selected URLs into a text file.

## Issues and Future Work

In this section, please list all know issues, limitations, and possible areas for future improvement. For example:

* Incomplete Data Extraction: The algorithm sometimes misses the first names of faculty or skips URLs entirely. Improvements in text parsing and URL filtering techniques are required to address these issues. 
* Performance and Scalability: The current version can take 20-30 minutes to scrape faculty data spanning over two decades. Optimization techniques like parallel processing can be employed in future versions to reduce this time and make the algorithm more scalable.
* Precision and Recall: Integration of more advanced machine learning models—supervised, semi-supervised, or unsupervised—can potentially improve the accuracy of the data extraction process.
