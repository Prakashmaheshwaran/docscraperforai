# DocScraperForAI 🚀💻

Welcome to **DocScraperForAI** – the ultimate Python library to effortlessly **scrape documentation**! Whether you need to grab a single page or crawl an entire domain, we've got you covered. ✨

## 🔥 Features

- **Single Page Scraping:** Grab the title, description, body text, code snippets, and even raw HTML! 📄
- **Domain-Wide Crawling:** Recursively follow internal links up to a specified depth. 🕸️
- **Multiple Export Formats:** Save the scraped content as plain text, Markdown, or JSON. 📑
- **Proxy Support:** Use a proxy for your requests – perfect for behind-firewall scraping! 🌐
- **Synchronous Modes:** A reliable, straightforward approach for scraping. ⏱️
- **Respects `robots.txt`:** Plays nice with websites by following their crawling rules. 🤝

## 🛠️ Installation

Install from PyPI with a single command:

```bash
pip install docscraperforai
```

Or, clone the repo and install in editable mode for development:

```bash
git clone https://github.com/Prakashmaheshwaran/docscraperforai.git
cd docscraperforai
pip install -e .
```

## 🚀 Quick Start

Here’s a simple example to get you started:

### Single Page Scraping

Scrape a single documentation page using the synchronous mode with optional proxy support. The output is saved in Markdown format.

```python
from docscraperforai.scraper import PageScraper, save_to_file

# URL to scrape
url = "https://docs.skyvern.com/introduction"

# Initialize the scraper.
# Replace "http://myproxy.com:8080" with your proxy URL or use None if not needed.
scraper = PageScraper(proxy=None)

# Scrape the page
data = scraper.scrape_page(url)

# Print the title and a preview of the text
print("TITLE:", data["title"])
print("Preview:", data["text"][:500], "...")

# Save the output as a Markdown file
save_to_file(data, "skyvern_intro.md", fmt="md")
```

### Domain-Wide Crawling (Depth 2)

Crawl all internal links starting from a base URL up to 2 levels deep. A delay is added between requests to be courteous to the servers. Each page is saved as a Markdown file in a specified output folder.

```python
from docscraperforai.crawler import DomainCrawler

# Base URL to start crawling
start_url = "https://docs.skyvern.com/introduction"

# Initialize the domain crawler:
# - max_depth=2: crawl 2 levels deep
# - delay=1.0: wait 1 second between requests (friendly scraping!)
# - proxy: use a proxy if necessary; for example, "http://myproxy.com:8080" (set to None if not needed)
crawler = DomainCrawler(
    base_url=start_url,
    max_depth=2,
    delay=1.0,
    proxy=None
)

# Run the crawler and save all pages as Markdown in the 'skyvern_docs' folder.
crawler.run(output_dir="skyvern_docs", fmt="md")
```

## ⚙️ Detailed Options & Settings

**DocScraperForAI** provides several configuration options to tailor the scraping behavior:

### Output Formats
- **`txt`**  
  - **Description:** Plain text output containing only the scraped body text.  
  - **Use Case:** Raw text data without formatting.
- **`md`**  
  - **Description:** Markdown output that includes the page title, meta description, and formatted text content.  
  - **Use Case:** Ideal for generating documentation or blog posts.
- **`json`**  
  - **Description:** JSON structured output with keys like `title`, `description`, `text`, `code_blocks`, and `html`.  
  - **Use Case:** When you need structured data for programmatic processing.

### Scraping Modes
- **Single Page Scraping (Sync Mode)**
  - **How It Works:** Uses the standard `requests` library to fetch the page content.
  - **Settings:**
    - `proxy` (optional): Supply a proxy URL (e.g., `"http://myproxy.com:8080"`). Otherwise, use `None`.
  
- **Domain-Wide Crawling**
  - **How It Works:** Recursively follows internal links, starting from a base URL.
  - **Settings:**
    - `max_depth`: Maximum depth to crawl (e.g., `2` for two levels deep).
    - `delay`: A delay (in seconds) between each request to avoid server overload.
    - `proxy` (optional): Supply a proxy URL if needed.

### Command-Line Options (For CLI Use)

If you prefer using the CLI version of DocScraperForAI, you have these options:

- **`--domain`**  
  Enables domain-wide crawling.
- **`--depth`**  
  Sets the maximum crawling depth (only for domain mode).
- **`--delay`**  
  Specifies the delay between each request.
- **`--output` or `-o`**  
  Defines the output directory or filename prefix.
- **`--format` or `-f`**  
  Chooses the output file format (choices: `txt`, `md`, `json`).
- **`--proxy`**  
  Sets the proxy URL for your requests.

Example CLI command:

```bash
python -m docscraperforai.cli https://docs.skyvern.com/introduction --domain --depth 2 --delay 1.0 --output skyvern_docs --format md --proxy http://myproxy.com:8080
```

## 🤖 How It Works

**DocScraperForAI** leverages Python libraries like `requests` and `BeautifulSoup` to download, parse, and extract content from documentation sites. Whether you prefer the classic synchronous approach or domain-wide crawling with advanced settings, our library makes it simple.

## 💡 Tips & Tricks

- **Proxy Support:**  
  Use the proxy parameter when you're behind a proxy or need to route your requests.
- **Customization:**  
  The library is designed to be extended. Feel free to contribute or create plugins for additional functionality.
- **Respect Robots.txt:**  
  The library adheres to `robots.txt`, so use it responsibly!

## ❤️ Contributing

We love contributions! If you have ideas or improvements, please open an issue or submit a pull request. Let's make documentation scraping smarter and more enjoyable for everyone.

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Have fun scraping and happy coding! 🎉🤖
