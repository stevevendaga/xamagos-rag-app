# Xamagos RAG Application

## Overview

The Xamagos RAG (Retrieval-Augmented Generation) application is an n8n workflow that creates an intelligent document processing and Q&A system. It monitors Google Drive for new documents, processes them using AI embeddings, and provides an AI-powered chat interface for answering questions about your business.

## Features

- **Automated Document Processing**: Monitors a specific Google Drive folder for new files
- **Vector Storage**: Uses Pinecone to store document embeddings for fast retrieval
- **AI-Powered Q&A**: Provides natural language interface to query stored documents
- **Lead Capture**: Collects user information when they request business details
- **Multi-Modal Integration**: Connects Google Drive, Pinecone, OpenAI, and Google Sheets

## Architecture

### Document Ingestion Pipeline
1. **Google Drive Trigger**: Watches for new file creation events
2. **Google Drive Node**: Downloads the uploaded document
3. **Text Splitter**: Breaks large documents into manageable chunks
4. **Embeddings**: Creates vector representations using OpenAI
5. **Pinecone Vector Store**: Stores vectors for semantic search

### Query Pipeline
1. **Chat Trigger**: Receives user messages via webhook
2. **AI Agent**: Processes queries using custom instructions
3. **xamagos_q Tool**: Retrieves relevant information from vector store
4. **Google Sheets Tool**: Captures lead information when requested

## Setup Requirements

- Google Drive OAuth2 credentials
- OpenAI API key
- Pinecone API key and index (`xamagos-rag`)
- Google Sheets OAuth2 credentials

## Configuration

The workflow uses these key parameters:
- **Pinecone Index**: `xamagos-rag`
- **Pinecone Namespace**: `Q&A`
- **OpenAI Model**: `gpt-4o`
- **System Prompt**: Custom instructions for the AI assistant role

## Usage

1. Upload documents to the monitored Google Drive folder
2. Access the public chat endpoint to ask questions about your business
3. The AI will respond based on the processed documents
4. Lead information is captured in Google Sheets after business inquiries

## Customization

The AI agent's behavior can be modified through its system message, which defines:
- The assistant's role as "Xamagos Bot"
- Instructions to use the `xamagos_q` tool for business questions
- Instructions to capture contact information after business inquiries