# Tesla Financial Reports RAG Assistant

A Retrieval-Augmented Generation (RAG) workflow built with **n8n**, **Google Drive**, **Pinecone**, and **OpenAI**. It is designed to ingest Tesla quarterly financial report documents and let users ask questions about their contents through an AI agent.

> **Portfolio project:** This repository contains an exported n8n workflow. You must configure your own credentials and service resources before running it.

## How it works

1. **Google Drive trigger** — watches the configured Drive location for documents to process.
2. **Document processing and embeddings** — prepares document content and creates embeddings using the configured OpenAI model.
3. **Pinecone vector store** — stores/retrieves the embedded content for semantic search.
4. **AI agent** — uses the retrieved context and an OpenAI chat model to answer questions about the reports.

The workflow uses a RAG pattern: answers are intended to be grounded in information retrieved from the documents indexed in the vector store.

## Technology stack

- [n8n](https://n8n.io/) — workflow automation
- [Google Drive](https://drive.google.com/) — document source
- [Pinecone](https://www.pinecone.io/) — vector database
- [OpenAI](https://platform.openai.com/) — embeddings and language model

## Requirements

Before importing the workflow, prepare:

- An n8n instance
- A Google Drive account and a folder containing the quarterly reports you want to index
- Google Drive credentials configured in n8n with access to that folder
- An OpenAI API key and credentials configured in n8n
- A Pinecone account, an index compatible with the embedding model's vector dimensions, and Pinecone credentials configured in n8n

Model and service availability may depend on your account and n8n version.

## Setup

1. Download `rag-workflow-sanitized.json` from this project.
2. In n8n, choose **Import from File** and select the JSON file.
3. Open the imported workflow and configure the credentials for Google Drive, OpenAI, and Pinecone on the relevant nodes.
4. Replace the placeholder Google Drive folder ID (`REPLACE_AFTER_IMPORT`) with your own folder ID wherever it is used.
5. Replace the Pinecone index placeholder (`YOUR_PINECONE_INDEX`) and namespace placeholder (`YOUR_PINECONE_NAMESPACE`) with the index and namespace you intend to use. Ensure the index's vector dimensions match the selected embedding model.
6. Review the Google Drive trigger and document-loading settings, and confirm the workflow points to the correct folder and files.
7. Keep the workflow **inactive** while configuring it. Run a manual test with a small sample document first, then verify that the document is indexed and that questions return relevant answers.
8. Activate the workflow only after you have verified that the configuration and results are correct.

Exact node labels and available options can vary by n8n version. Review each node after import rather than assuming the exported workflow will run without changes.

## Example questions

Once your Tesla quarterly reports are indexed, you can try questions such as:

- What revenue figures are reported for a specific quarter?
- What risks does the report identify?
- How did a reported metric change between two quarters?
- Which section of the indexed reports supports this answer?

Answer quality depends on the source documents, successful indexing, retrieval settings, and the model configuration. Verify important figures against the original filings.

## Repository contents

```text
.
├── README.md
└── AI-Powered Tesla Quarterly Financial Analyst-RAG.json
```

## Security notes

- Do **not** commit API keys, access tokens, credential exports, or private document links.
- Use your own n8n credentials and service resources; the exported workflow has had credential references and some environment-specific identifiers removed or replaced with placeholders.
- Review the workflow JSON before publishing it publicly to ensure it contains no private information.


