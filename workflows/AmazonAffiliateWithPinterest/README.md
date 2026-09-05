# Amazon Best Seller Affiliate Automation

An end-to-end automation built with **n8n** that discovers Amazon Best Seller products, generates Pinterest-ready content using AI, creates affiliate links, and publishes pins automatically.

The workflow combines **Amazon product scraping**, **Google Sheets**, **Ollama (Llama 3.2)**, and the **Pinterest API** to create a fully automated affiliate marketing pipeline.

---

## How It Works

The automation runs on a schedule and begins by asking a local AI model to suggest profitable Amazon Best Seller products from a chosen niche.

For each suggested product, the workflow performs an HTTP request to retrieve the product page and extracts relevant information such as the product title, image, rating, and price. The collected data is then cleaned and stored in Google Sheets.

Before continuing, another workflow removes duplicate products to ensure the same item is never processed twice.

The publishing workflow then reads a product from the spreadsheet and sends its information to a local **Llama 3.2** model running through **Ollama**. The model generates an SEO-friendly Pinterest title and description designed to improve discoverability.

Finally, the workflow builds the Amazon affiliate URL, combines it with the generated content, and publishes the pin to Pinterest automatically.

---

## Technologies Used

- n8n
- Ollama
- Llama 3.2
- Google Sheets API
- Pinterest API
- HTTP Requests
- JavaScript
- HTML Extraction
