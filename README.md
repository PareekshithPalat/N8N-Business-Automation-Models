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
