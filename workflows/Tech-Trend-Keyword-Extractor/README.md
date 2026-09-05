# Amazon Bestsellers → Pinterest Affiliate Automation

An end-to-end automation workflow built with **n8n** that discovers Amazon Best Seller products, generates Pinterest-optimized content using a local AI model, and automatically publishes affiliate pins to Pinterest.

The workflow is fully automated, from product discovery to content generation and publishing, while avoiding duplicate products.

---

## Features

- Automatically discovers Amazon Best Seller products
- Generates product category URLs using a local AI model (Ollama)
- Scrapes product information from Amazon
- Stores products inside Google Sheets
- Removes duplicate products automatically
- Generates Pinterest SEO titles and descriptions using AI
- Resizes product images for Pinterest
- Publishes pins automatically through a custom posting API
- Runs on a configurable schedule without manual intervention

---

# Workflow Overview

The automation is divided into three main stages.

## 1. Product Discovery

The workflow starts on a schedule.

The AI generates multiple Amazon Best Seller category URLs related to home decor products such as:

- Floor Lamps
- Furniture
- Rugs
- Lighting
- Candles
- Home Accessories

Each generated URL is visited automatically.

For every category, the workflow extracts:

- Product Rank
- ASIN
- Product Title
- Price
- Image URL
- Amazon Product Link

The extracted products are then stored inside Google Sheets.

---

## 2. Data Cleaning

Once all products are collected:

- Every row is loaded from Google Sheets.
- Duplicate products are detected using the ASIN.
- Only unique products are kept.
- The sheet is refreshed with the cleaned dataset.

This ensures products are never processed twice.

---

## 3. Pinterest Content Generation

For every product:

A local LLM (running through Ollama) generates:

- Pinterest title
- SEO-friendly description
- Relevant keyword tags

The prompts are optimized for high click-through rates by focusing on:

- Curiosity
- Benefits
- Home decor inspiration
- SEO keywords

---

## 4. Image Preparation

Before publishing:

- The original Amazon product image is resized to Pinterest dimensions.
- Images are converted into a Pinterest-friendly format.

---

## 5. Pinterest Publishing

Finally, the workflow sends the generated content to a custom posting service.

Each published pin contains:

- Optimized Pinterest title
- SEO description
- Product image
- Amazon affiliate link
- Pinterest board

Everything is published automatically without manual intervention.

---

# Technologies Used

- n8n
- Ollama
- Llama 3.1
- Google Sheets
- Amazon Best Sellers
- JavaScript
- HTTP Requests
- HTML Extraction
- Pinterest API (custom posting service)

---

# AI Usage

This project uses a **local Large Language Model** through Ollama to:

- Generate Amazon category URLs
- Write Pinterest titles
- Create SEO descriptions
- Generate keyword tags

No cloud AI service is required.

---

# Project Structure

The workflow includes:

- Scheduled triggers
- AI Agents
- HTTP Requests
- HTML Extraction
- JavaScript processing
- Google Sheets integration
- Duplicate removal
- Image preprocessing
- Pinterest publishing