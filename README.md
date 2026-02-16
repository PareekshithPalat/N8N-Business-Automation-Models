# n8n Business Process Automation Models

A collection of professional-grade n8n automation workflows designed to streamline business processes, increase efficiency, and leverage AI for intelligent decision-making.

This repository serves as a personal portfolio of business automations developed to solve real-world operational challenges. Each model is provided as a ready-to-import JSON file.

## 🚀 Automation Catalog

### Automation A: AI-Powered Email Triage System
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

### Automation B: Smart Lead Capture System
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

### Automation C: Social Media Auto Repurposer
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

### Automation D: Automated Meeting Notes Generator
**File:** [Automated Meeting Notes Generator.json](./Automated%20Meeting%20Notes%20Generator.json)

#### 📝 Description
An executive assistant automation that processes raw meeting transcripts to generate concise summaries, actionable tasks, and key decisions. It automatically emails these insights to all participants and connects to Notion for archiving.

#### 🛠️ Functionality
- **Transcript Processing:** Accepts meeting transcripts via a Webhook (e.g., from Otter.ai, Zoom, or a custom script).
- **AI Analysis:** Gemini acts as an executive assistant to extract:
    - **Summary:** A concise overview (max 150 words).
    - **Key Decisions:** A bulleted list of approved items.
    - **Action Items:** Specific tasks assigned to owners.
- **Automated Distribution:** Sends a structured email with the meeting highlights to all participants found in the payload.
- **Notion Integration:** Linked to a Notion database for centralized record-keeping of all meeting notes.

#### ⚙️ How to Run
1. **Import the Workflow:**
   - Import the `Automated Meeting Notes Generator.json` file.
2. **Configure Webhook:**
   - Ensure your meeting tool sends a JSON payload containing `transcript`, `meeting_title`, and `participants`.
3. **Setup Credentials:**
   - **Google Gemini:** API key for analysis.
   - **Gmail:** For sending the summary email.
   - **Notion:** Connect your workspace and select the target database for archiving.

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
