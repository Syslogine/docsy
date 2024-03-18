---
linkTitle: Simple Web Crawler
title: Building a Simple Web Crawler on Nvidia Jetson Nano using Ubuntu
description: >
 In this tutorial, we'll guide you through the steps of creating a simple web crawler on your Nvidia Jetson Nano running Ubuntu. A web crawler is a script or program that systematically browses the internet, typically for the purpose of extracting data. By building a basic web crawler, you can explore the fundamentals of web scraping and data extraction.
toc_hide: true
hide_summary: true
categories: ["jetson nano"]
---

## **Requirements**

- Nvidia Jetson Nano with Ubuntu installed
- Basic knowledge of Python programming

## **Steps**

1. **Install Required Packages:**

   Start by updating the package lists and installing the necessary packages for web crawling:

   ```bash
   sudo apt update
   sudo apt install -y python3 python3-pip
   ```

2. **Set Up a Python Virtual Environment:**

   Create a virtual environment to manage dependencies for your web crawler:

   ```bash
   python3 -m venv crawler_env
   source crawler_env/bin/activate
   ```

3. **Install BeautifulSoup and Requests:**

   Install the Python packages BeautifulSoup and Requests for web scraping:

   ```bash
   pip install beautifulsoup4 requests
   ```

4. **Create the Web Crawler Script:**

   Write a simple Python script to perform web crawling. You can use a text editor or an integrated development environment (IDE) to create a file named `web_crawler.py`:

   ```python
   import requests
   from bs4 import BeautifulSoup

   def simple_web_crawler(url):
       # Make a GET request to the specified URL
       response = requests.get(url)

       # Parse the HTML content of the page
       soup = BeautifulSoup(response.text, 'html.parser')

       # Extract and print links from the page
       links = soup.find_all('a')
       for link in links:
           print(link.get('href'))

   # Example usage
   if __name__ == "__main__":
       target_url = "https://example.com"
       simple_web_crawler(target_url)
   ```

5. **Run the Web Crawler:**

   Execute the web crawler script to see it in action:

   ```bash
   python web_crawler.py
   ```

   The script will fetch the HTML content of the specified URL and print the links found on the page.

6. **Customize and Extend:**

   Feel free to customize the script based on your needs. You can explore more advanced features such as handling different types of content, implementing crawling depth, or storing extracted data.

## **Conclusion**

Congratulations! You've successfully built a simple web crawler on your Nvidia Jetson Nano using Ubuntu. This tutorial provides a foundation for understanding web scraping concepts, and you can further enhance and customize your web crawler for specific applications or projects.
