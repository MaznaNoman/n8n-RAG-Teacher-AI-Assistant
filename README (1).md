# n8n RAG Teacher AI Assistant

An AI-powered teaching assistant built using n8n, OpenAI (GPT & Embeddings), and a custom HTML/JS frontend. Students upload their study material (PDF) and ask questions. The system uses a Vector Store RAG pipeline to answer strictly from the uploaded material while enforcing security guardrails.

## Features

* **Strict Study Material Context (RAG):** Explains topics and answers questions using only the uploaded PDF/document.
* **Guardrails & Privacy:** Blocks system prompt leakage, internal model details, and out-of-scope, off-topic questions (e.g., general trivia, recipes).
* **Custom Frontend:** Lightweight web interface to upload study material and ask the Teacher AI Assistant questions.
* **Session Memory:** Retains chat history for continuous conversation context.

## Repository Structure

* `index.html` - Frontend user interface for interacting with the Teacher AI Assistant.
* `workflow.json` - Exported n8n workflow pipeline containing nodes and system prompts.
* `README.md` - Setup and execution instructions.

## Local Setup Instructions

### 1. Import n8n Workflow

1. Start n8n (`n8n start`) and open your local instance at `http://localhost:5678`.
2. Create a new workflow, click the 3 dots (...) in the top right, and select **Import from File**.
3. Select the `workflow.json` file from this repository.
4. Configure your OpenAI credentials for both the Chat Model and Embedding nodes.

### 2. Frontend Configuration

1. Open `index.html` in a text editor.
2. Update the webhook `fetch` URL in `index.html` to match your n8n Test or Production webhook URL.
3. Open `index.html` directly in your browser to launch the interface.

### 3. Using the Assistant

1. Upload a study material PDF.
2. Type your question, for example: *"Explain chapter 3 in simple words"*.
3. Click **Ask teacher** (or press Enter) to get the answer.

## Test vs Production Webhook

* **Test URL** (`/webhook-test/...`): Click "Listen for test event" or "Execute workflow" on the Webhook node before every request. It works for one request at a time.
* **Production URL** (`/webhook/...`): Set the workflow to **Active**, then use this URL in `index.html`.

## Troubleshooting

* **"Failed to fetch" error:** This is usually a CORS issue. In the Webhook node, open **Options**, add **Allowed Origins (CORS)**, and set it to `*`.
* **No response:** Make sure n8n is running and the workflow is listening (test mode) or active (production mode).
