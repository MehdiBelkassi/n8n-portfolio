# 42 LinkedIn Automation

An automated workflow built with **n8n** that monitors my validated projects at **1337 Coding School (42 Network)** and publishes personalized LinkedIn posts after manual approval.

The workflow connects multiple services including the **42 API**, **Ollama (Llama 3.2)**, **Google Drive**, **Discord**, and **LinkedIn**, allowing the entire process to run automatically while still giving me full control before anything is published.

---

## How It Works

Every few minutes, a scheduler checks the 42 API to see if I have validated a new project.

When a new validation is detected, the workflow extracts information such as the project name, grade, and acquired skills. This data is then sent to a local **Llama 3.2** model running through **Ollama**, which generates a personalized LinkedIn post based on the project's technical content.

Next, the workflow retrieves the project's cover image from Google Drive and sends both the generated post and the image to Discord as a preview.

From Discord, I can either approve or reject the generated content. If I reject it, the workflow asks the AI to generate another version and sends a new preview. This process repeats until I'm satisfied with the result.

Once approved, the workflow automatically publishes the post to LinkedIn.

---

## Technologies Used

- n8n
- 42 API
- Ollama
- Llama 3.2
- Discord API
- Google Drive API
- LinkedIn API
- OAuth 2.0
- HTTP Webhooks

---

## What I Learned

### n8n

This project was my first experience with n8n. I originally assumed it was a paid platform, but discovered that self-hosting provides access to all of its features for free. Its visual workflow editor made it straightforward to build and connect multiple services while keeping the automation easy to understand and maintain.

### OAuth 2.0

Since the workflow interacts with several external services, I had to implement OAuth 2.0 authentication for the 42 API, Google Drive, and LinkedIn.

Building these integrations helped me better understand how OAuth works, including authorization servers, access tokens, client credentials, permission scopes, and secure API access without exposing user passwords.

### Local AI

To keep the project completely local and free, I used **Llama 3.2** through **Ollama**.

Running the model on CPU made inference relatively slow, and the generated content was not always as polished as expected. However, it allowed me to validate the entire workflow without relying on external AI services. In a future version, I plan to experiment with more capable local models or cloud-based APIs.

### Webhooks

The automation is divided into multiple workflows that communicate through HTTP webhooks.

I used **POST** requests to exchange project data between workflows and **GET** requests for the approval links triggered directly from Discord. This approach keeps the workflows modular while allowing them to communicate efficiently.

---

## Features

- Automatic detection of newly validated 42 projects
- AI-generated LinkedIn posts using a local language model
- Automatic retrieval of project cover images
- Discord approval system before publishing
- Regeneration loop until approval
- Automatic publishing to LinkedIn
- Secure authentication with OAuth 2.0
- Workflow communication using HTTP webhooks

---

## Future Improvements

- Replace Llama 3.2 with a more capable model.
- Reduce the delay by using event-driven triggers instead of scheduled polling when possible.
- Improve prompt engineering for more personalized posts.
- Automatically generate custom project banners.
- Add support for publishing to additional social platforms.
- Store publication history in a database to prevent duplicate posts.

---

