# Web-Crawler
A Web Crawler essentially just fetches Web Pages and just parses a website's content, extracting the relevant data and finding more Web Pages to crawl, for instance locating relevant Keywords, putting the content in an inverted table in MongoDB, allowing you to map the relevant keyword to the URL, the UML below displays the program flow clearly. As well as creating a Search UI, which allows you to locate a keyword, putting it in the Queue, which is then popper to parse through the Web Page content to further insert it into the database.



Experience

I chose to use simple technologies for the web crawler in order to fully understand all the components of the system. The only external services/libraries I used were MongoDB Atlas Search for the implementation of the searchable web archive. All other operations including fetching webpages, parsing HTML, threading, and benchmarking were done using Go's standard library. With this approach, I prioritized simplicity which will allow me to easily expand on this software in the future.

Although my web crawler accomplished the goal of crawling at least 1000 pages, here are a few future enhancements I could make. First, I would like to allow the user to decide the seed url. This could be easily implemented in my command line tool by prompting the user for a url at the start of the program. However, there would need to be some added error handling for if a user enters an invalid url.

Currently, the crawler searches Breadth-First. I would like to be able to experiment with different crawling algorithms like BFS, DFS, and hybrids. Making a swappable crawl would be ideal to compare the crawler statistics.

Below is a summary of the pros and cons of my web crawler.

Pros
Concurrently fetches and parses web pages
Database inserts are concurrent
Avoids loops and dead ends
Ignores script tags
Gracefully handles invalid urls, page not founds, and other errors
Searching the web archive is relatively fast
The crawled to queued ratio approached ~0.7 at its maximum, meaning pages were being crawled relatively effectively
Cons
Parsing the first 500 characters after the <body> tag isn't always a great representation of the webpage's content due to aria labels, navigation components, and scripts
Only crawls the first 500 tokens (open + closing tags) of a web page, which can result in an "incomplete" crawl of a page
Ignores relative links, which can result in an "incomplete" crawl of a page
The crawl speed decreases after about 500 seconds
