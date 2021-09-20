---
title: "Script for getting website URLs"
date: 2021-09-19T21:15:30-04:00
categories:
  - blog
tags:
  - Jekyll
  - update
---

As part of my research work, I commonly need to get a list of URLs from existing websites so that I can feed a selected subset of URLs into wget. 

```ruby
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

In the project, we then subset the resulting data for links_of_interest. These links_of_interest can then be fed into the function below to get the data itself.

```ruby
def get_data_from_links(links_of_interest):
    for a in links_of_interest:
        if os.path.exists(a):
            print('file already downloaded')
        else:
            full_text = 'wget -np -r -nH -L ' + a
            os.system(full_text)
```
