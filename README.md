# Module 12: WebScraping-challenge

# Deliverable 1: Scrape Titles and Preview Text from Mars News

The code provided is a Python script that demonstrates web scraping using the Splinter and BeautifulSoup libraries. The goal of the script is to scrape the titles and preview text from a Mars news website.

Here's a breakdown of the code:
- Importing the necessary libraries:
   - `from splinter import Browser`: This imports the Browser class from the Splinter library, which allows automated browsing.
   - `from bs4 import BeautifulSoup as soup`: This imports the BeautifulSoup class from the BeautifulSoup library, which is used for parsing HTML.

- Setting up the browser:
   - `browser = Browser('chrome')`: This creates an instance of the Browser class using the Chrome browser. This will be used for automated browsing.

Step 1. Visiting the website:
   - `url = 'https://static.bc-edx.com/data/web/mars_news/index.html'`: This sets the URL of the Mars news website to be scraped.
   - `browser.visit(url)`: This uses the browser instance to visit the specified URL.

Step 2. Scraping the website:
   - `html = browser.html`: This retrieves the HTML content of the visited page.
   - `mars_news_soup = soup(html, 'html.parser')`: This creates a BeautifulSoup object by parsing the HTML content.
   - `text_elements = mars_news_soup.find_all('div', class_='list_text')`: This finds all the `<div>` elements with the class name 'list_text' on the page. These elements contain the titles and preview text of the news articles.

Step 3. Storing the results:
   - `news_list = []`: This creates an empty list to store the dictionaries containing the scraped data.
   - Looping through the text elements:
     - `for result in text_elements: ...`: This iterates over each text element found on the page.
     - Extracting the title and preview text:
       - `title = result.find('div', class_='content_title').text`: This extracts the text content of the `<div>` element with the class name 'content_title', which represents the article title.
       - `preview = result.find('div', class_='article_teaser_body').text`: This extracts the text content of the `<div>` element with the class name 'article_teaser_body', which represents the preview text.
     - Storing the title and preview in a dictionary:
       - `news_dict = {'title': title, 'preview': preview}`: This creates a dictionary with the extracted title and preview.
     - Adding the dictionary to the list:
       - `news_list.append(news_dict)`: This appends the dictionary to the news_list.
   - Printing the list:
     - `print(news_list)`: This prints the list of dictionaries containing the scraped data.

The output of the script will be a list of dictionaries, where each dictionary represents an article with its title and preview text.
