---
title: "Script for getting website URLs"
date: 2021-09-19T21:15:30-04:00
categories:
  - Scripts
tags:
  - website_scraping
  - las_files_from_sites
---

As part of the research work into solar cities, it is often necessary to download large amounts of data from websites. For that purpose, I put together a simple python function that downloads a list of all the available URL links on a website of interest that meet a particular filetype. The default filetype is '.las' since, most often, I'm interestedin getting a list of URLs for each of the LIDAR las files on the website. 

The function is available below:

```python
import requests
import os
from bs4 import BeautifulSoup

def get_links(URL, filetype='.las'):
    # use requests to retrieve data from a given URL
    URL_response = requests.get(URL)

    # parse the whole HTML page using BeautifulSoup
    URL_soup = BeautifulSoup(URL_response.text, 'html.parser')

    # get all links on the page
    links = [link.get('href') for link in URL_soup.find_all('a')]

    #  Add homepage and keep the unique links
    fixed_links = set([''.join([URL, link]) for link in links if link])

    # only keep links with certain filetype
    links_filetype = []

    for entry in fixed_links:
        if entry.endswith(filetype):
            links_filetype.append(entry)

    return links_filetype
```

The resutling links_filetype list of URLs can then be subset through, for instance, an index of LAS files and their spatial coverage. Subsetting the URL list based on a particular spatial area of interest, for example, lowers the storage requirements by not downloading files that are external to the analysis at hand. A resulting links_of_interest list can then be entered into the function below to use wget and actually download the data directly into the working directory. 

```python
import os as os
def get_data_from_links(links_of_interest):
    for a in links_of_interest:
        if os.path.exists(a):
            print('file already downloaded')
        else:
            full_text = 'wget -np -r -nH -L ' + a
            os.system(full_text)
```
