# Website Contact Scraper

This project is a multithreaded web scraper designed to extract contact information (emails and phone numbers) from a list of websites. It scrapes both the home page and the contact page of each website (if available), then stores the extracted data into an Excel file.

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Project Files](#project-files)
- [Explanation of Code Logic](#explanation-of-code-logic)
  - [Main Components](#main-components)
- [Dependencies](#dependencies)

## Introduction

The scraper takes a list of websites from a file, sends HTTP requests to fetch the pages, and parses the HTML using BeautifulSoup to extract email addresses and phone numbers. The data is stored in an Excel file for easy access. This scraper supports multi-threading, which allows it to crawl multiple websites concurrently for faster performance.

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/darsh0o/compact-email-scraper.git
   cd website-contact-scraper
   ```
2. **Install dependencies**:
   To install the required Python packages, run the following command:
   ```bash
   pip install -r requirements.txt
   ```
## Usage

1. **Prepare the URL input file**:
   - Ensure that you have a file named `web_urls.txt` containing the list of website URLs. Each URL should be on a new line, without any additional characters.
   - The scraper will automatically prefix URLs with "https://" if they do not start with "http" or "https".

2. **Run the scraper**:
   - To start scraping, use the following command:
   ```bash
   python main.py
   ```
3. **Output**:
   - Once the script completes, an Excel file named `websites_info.xlsx` will be generated. This file will contain the scraped contact information for each website, with columns for:
     - `Website`: The URL of the website.
     - `Email`: The extracted email address (if available).
     - `Phone`: The extracted phone number (if available).

   The data can be accessed and analyzed using any spreadsheet software that supports `.xlsx` files.

## Project Files

- **`main.py`**: The main script that handles the web scraping logic, using multiple threads to speed up the extraction process.
- **`requirements.txt`**: A list of all Python packages needed to run the project.
- **`web_urls.txt`**: A text file containing the URLs of websites to scrape, with one URL per line.
- **`websites_info.xlsx`**: The output Excel file containing the scraped emails and phone numbers.

## Explanation of Code Logic

### Main Components

- **`read_file()`**: Reads the list of website URLs from the `web_urls.txt` file. If a URL is missing the "http" or "https" prefix, it adds "https://" to ensure valid URLs.
  
- **`get_email()`**: This function uses a regular expression to search for email addresses within the HTML content of the page and returns a list of unique emails.

- **`get_phone()`**: Similar to the email function, this function uses a regular expression to find phone numbers in the HTML and returns a list of unique phone numbers.

- **`crawl()`**: The core of the web scraping process. It retrieves each website's content, checks for email and phone information on the homepage and contact page, and stores the extracted data. This function is executed concurrently using multiple threads for better performance.

- **`main()`**: The entry point of the script. It initializes the threading mechanism, reads the URLs, and manages the entire scraping process. Once the data is gathered, it writes the results into an Excel file using the `pandas` library.

## Dependencies

The following Python libraries are used in this project:
- `requests`: For sending HTTP requests to websites and retrieving their content.
- `beautifulsoup4`: For parsing and extracting data from the HTML content of the websites.
- `coloredlogs`: For improved logging with color-coded messages.
- `pandas`: For handling and exporting data into an Excel file.
- `openpyxl`: For working with `.xlsx` files.
- `requests-random-user-agent`: For generating random User-Agent strings in HTTP requests to avoid blocking.

To install all dependencies, simply run:
```bash
pip install -r requirements.txt
```
## Disclaimer

Use this script responsibly and ensure that you have the legal right to scrape the websites you target. Web scraping may be subject to legal restrictions and terms of service agreements of the websites being scraped. Be respectful of website owners' policies and guidelines.
