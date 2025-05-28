# University-Data-Web-Scraper
A Python-based web scraper designed to extract information about universities from the internet. The extracted data is then compiled into a CSV file for easy analysis and use.

## Project Overview
The primary goal of this project is to automate the collection of comprehensive university data, including:
- University Name
- Location
- Type (Public/Private)
- Summary
- Official Website
- Established Year
- Student Enrollment
- Application Link (for international graduate programs)
- Funding/Financial Aid Link (for international graduate programs)
- Acceptance Rate

This data can be valuable for various purposes, such as academic research, university comparisons, or building educational directories.

## How It Works
The scraper operates by:
1. **Searching Wikipedia:** For each university in a predefined list, it performs a Google search to find the corresponding Wikipedia page.
2. **Parsing Wikipedia Data:** It then uses ```BeautifulSoup``` to parse the Wikipedia page and extract structured information like location, type, established year, website, and enrollment from the infobox and initial summary.
3. **Searching Google for Specific Links:** For "Application Link," "Funding Link," and "Acceptance Rate," the scraper performs targeted Google searches using specific keywords (e.g., "university international graduate apply").
4. **Extracting Google Search Results:** It identifies relevant links and information within the Google search results pages.
5. **Data Compilation:** All extracted data points for each university are assembled into a list.
6. **CSV Export:** Finally, the collected data is saved into a CSV file.

## Performance and Efficiency
The script is designed with pauses to avoid overwhelming websites and getting blocked. On average, it takes approximately 10 seconds to extract data for a single university. This means that scraping data for a list of 100 universities will take around 1000 seconds, or roughly 16 minutes. While this ensures responsible scraping, users should factor this time into their expectations when running the script on larger lists.

## Data Completeness and Quality Insights
Analysis of the generated datasets reveals varying levels of completeness for different data points:
- **High Completeness for Core Information:**
  - **Name, Application Link, and Funding Link** consistently show 100% non-null values across all tested university lists (Top 100 World, Top 20 UK, Top 20 USA, Top 50 USA). This indicates robust extraction for these critical fields.
  - **Location, Type, Summary, Website, Established, and Enrollment** generally have very high non-null counts, often at or near 100% for specific regional lists (e.g., Top 20 UK, Top 20 USA, Top 50 USA). This suggests that Wikipedia infoboxes usually contain these details for well-known institutions.

- **Challenges with Acceptance Rate:**
  - The **Acceptance Rate** field shows significantly lower completeness across all datasets. For the "Top 100 universities in the world," only 31 out of 101 entries have this data. Similarly, for the "Top 20 UK" and "Top 20 USA" lists, only 8 and 15 entries, respectively, have acceptance rates. Even for the "Top 50 USA" list, only 28 out of 50 entries have this information. This suggests that acceptance rates are often not readily available or consistently formatted in the search results the scraper targets.
 
- **Minor Data Gaps:**
  - Some columns like ```Location```, ```Type```, ```Summary```, ```Website```, and ```Established``` occasionally have a few missing values, particularly in the larger "Top 100 universities in the world" dataset. This could be due to variations in Wikipedia page structure, less standardized information for certain international universities, or slight parsing mismatches.
  - The ```Established``` column for the "Top 100 universities in the world" was detected as ```float64``` type, implying some entries might have been parsed as numbers, while for other smaller datasets it remained ```object``` type. This indicates minor inconsistencies in data types that might require cleaning if numerical operations are intended.

In summary, while the scraper is highly effective at collecting core university details and application/funding links, obtaining comprehensive acceptance rate data proves to be a consistent challenge due to its less standardized availability on web sources.

## Key Features and Improvements
- **Robust Data Extraction:** The script leverages ```BeautifulSoup``` and regular expressions to effectively parse HTML and extract specific data fields.
- **Handles Dynamic Content:** The use of ```DrissionPage``` (which relies on Chromium) allows the scraper to interact with dynamic web pages and bypass potential CAPTCHA challenges, a common hurdle with traditional ```requests```-based scraping.
- **Error Handling:** ```try-except``` blocks are implemented to gracefully handle potential errors during web requests and data extraction, preventing the script from crashing.
- **Predefined University List:** A comprehensive list of universities is included, making it easy to run the scraper on a curated set of institutions.
- **User-Agent Randomization:** The ```fake_useragent``` library is used to rotate user-agents, reducing the likelihood of being blocked by websites.

## Important Considerations for Running the Script
- **Dependencies:** Ensure all required Python libraries are installed. The script explicitly lists them in the ```imports``` section:
  ```html5lib```, ```re```, ```urllib```, ```time```, ```pandas```, ```DrissionPage```, ```bs4``` (BeautifulSoup), ```selenium```, ```fake_useragent```

  You can install these using pip:
  ```python
  pip install html5lib requests pandas DrissionPage beautifulsoup4 selenium fake-useragent
  ```
- **Chromium Browser:** The script relies on DrissionPage to control a Chromium browser. Ensure you have a compatible Chromium/Chrome browser installed on your system where the script will be executed.
- **University Name Formatting:** It's crucial that the university names in the universityList are in English only. Using native language names (e.g., "Université Paris-Saclay" instead of "Paris-Saclay University") can lead to the scraper accessing the native language Wikipedia page, which may have a different HTML structure and result in failed data extraction. The provided list already incorporates this correction.
- **Rate Limiting:** ```time.sleep()``` calls are included to introduce delays between requests, which helps to avoid overwhelming websites and getting IP-blocked. However, be mindful that excessive scraping without adequate delays can still lead to temporary blocks.

## Data Snapshots
Below snapshot shows the extracted dataset for Top 100 Universities of the World
![Image](https://github.com/13ASRamgarhia/University-Data-Web-Scraper/blob/main/top%20100%20world.png)

Below snapshot shows the extracted dataset for Top 20 Universities of the USA
![Image](https://github.com/13ASRamgarhia/University-Data-Web-Scraper/blob/main/top%2020%20usa.png)
  
