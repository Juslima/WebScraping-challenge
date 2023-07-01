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

# Deliverable 2: Scrape and Analyze Mars Weather Data
The code is also a Python script that performs web scraping and data analysis on Mars weather data. 

Step 1: Visit the Website
- The script uses the `splinter` library to automate browsing and visits a specific URL that contains Mars temperature data.
- The URL being visited is "https://static.bc-edx.com/data/web/mars_facts/temperature.html".

Step 2: Scrape the Table
- The HTML content of the visited webpage is extracted using `browser.html`.
- The `BeautifulSoup` library is used to create a BeautifulSoup object, `mars_data_soup`, by parsing the HTML content.
- The script finds the table element within the HTML using `mars_data_soup.find('table')`.
- It then finds all the rows within the table using `table.find_all('tr')`.

Step 3: Store the Data
- An empty list called `new_list` is created to store the scraped data.
- A loop iterates through each row (excluding the header row) and extracts the data from each cell using `row.find_all('td')`.
- The data from each row is stored in a dictionary called `row_data`, with keys corresponding to the column names.
- The `row_data` dictionary is appended to the `new_list` list.
- Finally, a Pandas DataFrame, `df`, is created using the `new_list` and the column names.

Step 4: Prepare Data for Analysis
- The script examines the data types of each column in the DataFrame using `df.dtypes`.
- The data types are initially represented as objects (strings).
- The script then converts the 'terrestrial_date' column to datetime format using `pd.to_datetime()`.
- The 'sol', 'ls', 'month', 'min_temp', and 'pressure' columns are converted to their appropriate data types using `.astype()` function.
- The updated data types are confirmed by printing `df.dtypes`.

Step 5: Analyze the Data
- The script uses various Pandas functions to analyze the dataset and answer specific questions:
  - Counting the number of months on Mars using `df['month'].value_counts()`.
  - Counting the total number of Martian days worth of data using `len(df)`.
  - Finding the average minimum temperature by month using `df.groupby('month')['min_temp'].mean()`.
  - Plotting the average minimum temperature by month using `plot(kind='bar')`.
  - Identifying the coldest and warmest months on Mars by finding the index of the minimum and maximum values.
  - Finding the average atmospheric pressure by month using `df.groupby('month')['pressure'].mean()`.
  - Plotting the average atmospheric pressure by month using `plot(kind='bar')`.
  - Plotting the daily minimum temperature over the number of terrestrial days.
- The results are printed or plotted accordingly.

Step 6: Save the Data
- The DataFrame is exported to a CSV file named "mars_weather_data.csv" using `df.to_csv()`.
- The browser instance is closed using `browser.quit()`.

Overall, the script scrapes Mars weather data, stores it in a DataFrame, performs some data cleaning and analysis, and saves the results to a CSV file.
