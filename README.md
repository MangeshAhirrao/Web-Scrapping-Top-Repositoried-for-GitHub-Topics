# Web-Scrapping-Top-Repositoried-for-GitHub-Topics
### Pick a Website and Describe your objective

* Browse through different sites and pick on to scrape. Check the "Project Ideas" section for inspiration.
* Identify the information you'd like to scrape from the site. Decide the format of the output CSV file.
* Summarize your project idea and outline your strategy in a Juptyer notebook. Use the "New" button above.

### Project Outline:

- We are going to scrape https://github.com/topics
- We'll get a list of topics. For each topic, we'll get topic title, topic page URL and topic description
- For each topic, we'll get the top 25 repositories in the topic from the topic page.
- For each repository, we'll grab the repo, name, username, stars, and repo URL.
- For each topic we'll create a CSV file in the following format: 
```
Repo Name,Username,Stars,Repo URL
three.js,mrdoob,87000,https://github.com/mrdoob/three.js
libgdx,libgdx,20800,https://github.com/libgdx/libgdx
```
### Use the requests library to download web pages
```
!pip install requests --upgrade --quiet
import requests
```
### Use Beautiful Soup to parse and Extract information
```
!pip install beautifulsoup4 --upgrade
from bs4 import BeautifulSoup
```
### Importing Pandas
```
!pip install pandas --quiet
import pandas as pd
topics_dict = {
    'title': topic_titles,
    'description': topic_descs,
    'url': topic_urls
}
topics_df = pd.DataFrame(topics_dict)
topics_df
topics_df.to_csv('topics.csv', index = None)
```

### Putting it all together
* We have a funciton to get the list of topics
* We have a function to create a CSV file for scraped repos from a topics page
* Let's create a function to put them together

```
def scrape_topics_repos():
    print('Scraping list of topics')
    topics_df = scrape_topics()
    
    os.makedirs('data', exist_ok=True)
    for index, row in topics_df.iterrows():
        print('Scraping top repositories for "{}"'.format(row['title']))
        scrape_topic(row['url'], 'data/{}.csv'.format(row['title']))
```
