# AI-Powered Customer Feedback Classifier (n8n Workflow)

This repository contains a production-ready **n8n workflow** designed to automate the capture, classification, and routing of customer feedback. Utilizing the Google Gemini language model, the workflow intelligently categorizes incoming responses into actionable buckets, updates a central database, and alerts internal teams instantly.

## 📁 Workflow Overview

The automation implements the following end-to-end lifecycle:
1. **Capture:** Receives submissions via a native **n8n Form Trigger** containing user metadata and feedback.
2. **Analysis:** Routes the raw text to an **AI Agent node backed by Google Gemini** to dynamically classify the feedback as a *Complaint*, *Compliment*, or *Feature Addition Request*.
3. **Synchronization:** Uses a data **Merge** and **Switch** routing matrix to update the respective **Airtable** tables.
4. **Notification:** Sends targeted alerts to specific **Slack** channels based on classification.
5. **Auto-Response:** Dispatches a structured reassurance email via **Gmail** if the feedback is flagged as a Complaint.

---

## 🛠️ Integrated Nodes & Prerequisites

To run this workflow, ensure your n8n instance is updated and you have access to the following third-party credentials:

* **n8n version:** 1.0+ (utilizing Advanced AI/LangChain Nodes)
* **Google Gemini Chat Model:** API access for `lmChatGoogleGemini`
* **Airtable:** Personal Access Token with access to your Feedback base
* **Slack:** OAuth2 App configuration with channel write scopes (`chat:write`)
* **Gmail:** OAuth2 API configuration for secure email dispatching

---

## 🚀 Getting Started & Deployment

### 1. Import the Workflow into n8n
1. Clone this repository or download the `workflows/feedback-form-workflow.json` file.
2. Open your n8n instance dashboard.
3. Click on **Workflows** -> **Add Workflow** (or open an empty canvas).
4. Click on the three dots `...` in the top right-hand corner and select **Import from File**.
5. Select the `feedback-form-workflow.json` file.

### 2. Configure Node Credentials
Upon import, nodes requiring authentication will display warning icons. You will need to click into the following nodes to link your own credentials:
* **Google Gemini Chat Model:** Link your Gemini API key.
* **Airtable Nodes (Complaint, Compliment, Feature Request):** Select your Base ID and specific Table IDs.
* **Slack Nodes:** Authenticate your Slack workspace and select target channels.
* **Gmail Node:** Set up your OAuth2 profile for automatic replies.

### 3. Activate the Webhook
Once credentials and IDs are configured, toggle the workflow from **Inactive** to **Active** in the top-right corner to make the Form public.
