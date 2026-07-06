# n8n FAQ Bot for Telegram

Drop documents into Google Drive, get answers in Telegram. Built with n8n, Gemini, and Pinecone.

## What it does

This workflow runs a customer support bot on Telegram that answers questions strictly from your uploaded documents.

When you add a file to a Google Drive folder, n8n downloads it, breaks it into chunks, embeds it with Gemini, and stores it in Pinecone.

When someone messages your Telegram bot, n8n finds the relevant chunks from Pinecone, feeds them to a Gemini agent, and sends the answer back. The bot has short-term memory so it can follow a conversation.

If the answer isn't in the documents, the bot says: "I don't have that information in the documents. Please contact support for help."

## Screenshot
<img width="1357" height="618" alt="Screenshot (201)" src="https://github.com/user-attachments/assets/54348a1e-0488-4991-8120-2db2d4352e56" />


## Repository Structure
  ## Repository Structure

- `LICENSE` — MIT license
- `README.md` — Project documentation
- `rag-telegram-bot.json` — The n8n workflow file
- `assets/workflow-screenshot.png` — Screenshot of the n8n canvas

## What you need

- n8n (self-hosted or cloud)
- Google Drive folder + OAuth2 credentials
- Pinecone index + API key
- Google Gemini API key
- Telegram bot token from @BotFather
  

## Setup

1. Import `rag-telegram-bot.json` into n8n
2. Create credentials for Google Drive, Pinecone, Gemini, and Telegram
3. Set your Google Drive folder in the **Google Drive Trigger**
4. Set your Pinecone index in both **Pinecone Vector Store** nodes
5. Save and activate

## Nodes

- Google Drive Trigger - watches your folder for changes
- Download file - pulls the file from Drive
- Default Data Loader - chunks the file for embedding
- Embeddings Google Gemini - creates vector embeddings
- Pinecone Vector Store - stores and retrieves chunks
- Telegram Trigger - listens for messages
- AI Agent - generates answers from retrieved documents
- Simple Memory - keeps conversation context
- Vector_Store - retrieves relevant chunks
- Embeddings Google Gemini1 - creates query embeddings
- Google Gemini Chat Model - writes the replies
- Send a text message - sends answers back to Telegram
