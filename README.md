# n8n Business Process Automation Models

A collection of professional-grade n8n automation workflows designed to streamline business processes, increase efficiency, and leverage AI for intelligent decision-making.

This repository serves as a personal portfolio of business automations developed to solve real-world operational challenges. Each model is provided as a ready-to-import JSON file.

## � Table of Contents
- [1. AI-Powered Email Triage System](#1-ai-powered-email-triage-system)
- [2. Smart Lead Capture System](#2-smart-lead-capture-system)
- [3. Social Media Auto Repurposer](#3-social-media-auto-repurposer)
- [4. Automated Meeting Notes Generator](#4-automated-meeting-notes-generator)
- [5. Crypto & Stock Price Alert System](#5-crypto--stock-price-alert-system)
- [General Setup Instructions](#-general-setup-instructions)
- [License](#-license)
- [Contact](#-contact)

---

## 🚀 Automation Catalog

### 1. AI-Powered Email Triage System
**File:** [AI-Powered Email Triage System.json](./AI-Powered%20Email%20Triage%20System.json)

#### 📝 Description
An intelligent email management system that automatically monitors a Gmail inbox, classifies incoming messages using Google Gemini AI, and routes them to specific Slack channels based on their priority and intent.

#### 🛠️ Functionality
- **Automated Monitoring:** Polls Gmail every minute for new messages.
- **AI Classification:** Uses Gemini 1.5 Flash to categorize emails into:
    - **Urgent:** Time-sensitive tasks and deadlines.
    - **Sales:** Promotional offers and commercial deals.
    - **Spam:** Suspected phishing or irrelevant mass mail.
    - **Personal:** Casual or non-business communication.
- **Smart Routing:** 
    - `Urgent` emails are immediately pushed to an `#important-mails` Slack channel.
    - Non-urgent or `Spam` contents are logged to a separate Slack section for review.
- **Context Awareness:** The AI is instructed with strict classification rules to ensure high accuracy.

#### ⚙️ How to Run
1. **Import the Workflow:**
   - Create a new workflow in your n8n instance.
   - Go to the **Settings** menu (three dots) and select **Import from File**.
   - Select the `AI-Powered Email Triage System.json` file from this repository.
2. **Configure Credentials:**
   - **Gmail Trigger:** Connect your Google account.
   - **Google Gemini:** Provide your Google PaLM/Gemini API key.
   - **Slack:** Connect your Slack workspace and specify your desired channel IDs.
3. **Activate:**
   - Set the workflow to **Active** to start the one-minute polling cycle.

---

### 2. Smart Lead Capture System
**File:** [Smart Lead Capture.json](./Smart%20Lead%20Capture.json)

#### 📝 Description
A high-performance lead generation and nurturing system that captures leads via webhooks, organizes them in Google Sheets, and uses AI to craft personalized welcome emails before notifying the sales team.

#### 🛠️ Functionality
- **Webhook Integration:** Entry point for lead data from any website form or third-party source.
- **Data Persistence:** Automatically appends new lead details (Name, Email, Company, Phone, Message) to a centralized **Google Sheet**.
- **AI Personalization:** Leverages Gemini AI to:
    - Write a friendly, professional, and personalized welcome email based on the lead's company and message.
    - Generate a contextually relevant email subject line.
- **Automated Communication:** Sends the AI-generated email through Gmail immediately after capture.
- **Instant Notification:** Pushes the full lead profile to a **Slack** `#sales` channel for rapid follow-up.

#### ⚙️ How to Run
1. **Import the Workflow:**
   - Import the `Smart Lead Capture.json` file into your n8n instance.
2. **Configure External Services:**
   - **Google Sheets:** Select your target spreadsheet and sheet name.
   - **Google Gemini:** Uses the same PaLM/Gemini credentials for email body and subject generation.
   - **Gmail:** Connect your sender account.
   - **Slack:** Set the channel to your sales team's notification channel.
3. **Webhook Setup:**
   - Copy the Webhook URL and point your lead source (e.g., a Webflow or Elementor form) to this endpoint.

---

### 3. Social Media Auto Repurposer
**File:** [Social Media Auto Repurposer.json](./Social%20Media%20Auto%20Repurposer.json)

#### 📝 Description
A content strategist automation that automatically turns blog posts into platform-optimized social media content. It monitors an RSS feed, uses AI to repurpose the content for LinkedIn, Twitter, and Instagram, and publishes the results automatically.

#### 🛠️ Functionality
- **RSS Monitoring:** Continuously polls an RSS feed for new blog posts or articles.
- **AI Content Strategist:** Uses Gemini 1.5 Flash to transform the article into:
    - **LinkedIn Post:** Professional tone, structured for engagement (150-200 words).
    - **Twitter Thread:** A 5-tweet sequence designed for high readability.
    - **Instagram Caption:** A catchy summary including 5 relevant hashtags.
- **Automated Publishing:**
    - **LinkedIn:** Automatically creates a professional update.
    - **Twitter:** Automatically posts the content as a tweet or thread.
- **Structured Output:** Uses strict JSON formatting for the AI response to ensure seamless parsing between nodes.

#### ⚙️ How to Run
1. **Import the Workflow:**
   - Import the `Social Media Auto Repurposer.json` file.
2. **Configure Triggers & APIs:**
   - **RSS Feed:** Enter the URL of the blog or site you want to monitor.
   - **Google Gemini:** Provide your API key for content generation.
   - **LinkedIn & Twitter:** Connect your respective developer accounts/credentials.
3. **Customize Strategy:** 
   - You can modify the system prompt in the Gemini node to change the tone or length of the generated posts.

---

### 4. Automated Meeting Notes Generator
**File:** [Automated Meeting Notes Generator.json](./Automated%20Meeting%20Notes%20Generator.json)

#### 📝 Description
An advanced executive assistant workflow designed to transform raw meeting transcripts into structured, actionable business intelligence. It uses a specialized Gemini AI prompt to parse conversation text and distribute professional summaries via email and Notion.

#### 🛠️ Technical Deep Dive
- **Trigger Payload (Webhook):**
  - The workflow expects a `POST` request with the following JSON structure:
    ```json
    {
      "meeting_title": "Q3 Planning Strategy",
      "transcript": "Speaker A: ... Speaker B: ...",
      "participants": ["alice@company.com", "bob@company.com"]
    }
    ```
- **AI Logic (Executive Persona):**
  - **Model:** Gemini 1.5 Flash.
  - **System Prompt:** Configured as an "Executive Meeting Assistant" with strict output rules.
  - **Output Schema:** Forces the AI to return a valid JSON object containing:
    - `summary`: A high-level overview (max 150 words).
    - `key_decisions`: An array of strings defining agreed-upon points.
    - `action_items`: An array of objects with `task` and `owner` fields.
- **Data Routing:**
  - **JSON Parsing:** A set node parses the stringified AI response into usable n8n variables (`$json.Summary`, `$json.key_decisions`, etc.).
  - **Email Dispatch:** Dynamically joins the `participants` array to send a single summary email to all attendees.
  - **Notion Integration:** Connects to a specific Notion database (ID: `309df...`) to retrieve or verify the storage destination (customizable to *Create Page* for archiving).

#### ⚙️ How to Run & Customize
1. **Import:** Load `Automated Meeting Notes Generator.json` into n8n.
2. **Webhook Integration:**
   - Use a tool like **Otter.ai** or a **Zoom Webhook** to send the transcript to this workflow's URL.
   - *Tip:* You can also use a simple cURL command or Postman to test:
     ```bash
     curl -X POST <YOUR_WEBHOOK_URL> -H "Content-Type: application/json" -d '{"meeting_title":"Test","transcript":"...","participants":["you@example.com"]}'
     ```
3. **Refine the AI Prompt:** 
   - Open the **Message a Model** node to adjust the persona (e.g., change "Executive Assistant" to "Technical Scribe" for engineering meetings).
4. **Update Credentials:**
   - Link your Gmail and Notion accounts.
   - Update the Notion Database ID in the final node to match your own "Meeting Notes" database.

---

### 5. Crypto & Stock Price Alert System
**File:** [Crypto_Stock Price Alert System.json](./Crypto_Stock%20Price%20Alert%20System.json)

#### 📝 Description
A dedicated financial monitoring tool that tracks real-time market prices for cryptocurrencies (like Bitcoin) or stocks. It runs on a schedule, fetches live data, and triggers instant alerts via Slack and Telegram when specific price thresholds are crossed.

#### 🛠️ Functionality
- **Scheduled Monitoring:** Automatically runs every 30 minutes to check market status.
- **Live Data Fetching:** Uses an HTTP Request node to pull real-time data from the CoinGecko API (configurable for other APIs).
- **Threshold Logic:**
    - Checks if the current price exceeds a user-defined target (e.g., BTC > $50,000).
    - Uses an 'If' node to determine whether to trigger an alert.
- **Multi-Channel Alerts:**
    - **Slack:** Sends a formatted message to a specific channel.
    - **Telegram:** Sends a text alert to your phone or group.

#### ⚙️ How to Run
1. **Import the Workflow:**
   - Import the `Crypto_Stock Price Alert System.json` file.
2. **Configure Triggers:**
   - **Schedule Trigger:** Adjust the interval (default: 30 mins) to your preference.
3. **API Setup:**
   - **HTTP Request:** The template uses CoinGecko (no key required for basic use). You can swap this URL for any stock API (e.g., Alpha Vantage, Finnhub).
4. **Set Thresholds:**
   - Open the **If** node and change the value `50000` to your desired price target.
5. **Connect Alerts:**
   - **Slack & Telegram:** Add your bot tokens and channel IDs.

---

## 📥 General Setup Instructions

To use any of the automations in this repository:
1. **Clone the Repo:** `git clone https://github.com/PareekshithPalat/N8N-Business-Automation-Models.git`
2. **Import JSON:** Import the desired `.json` file into your n8n environment.
3. **Update Credentials:** Each node requiring authentication (Gmail, Slack, AI, etc.) must be updated with your personal credentials.
4. **Customization:** Feel free to adjust the prompt in the AI nodes or the routing logic in the 'If' nodes to better suit your business needs.

## 📄 License
This repository is licensed under the [MIT License](./LICENSE).

## 🤝 Contact
Developed by **Pareekshith Palat**. If you have questions or want to collaborate on business automations, feel free to reach out!
