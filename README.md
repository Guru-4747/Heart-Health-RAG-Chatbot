# Heart-Health-RAG-Chatbot
# Heart Health RAG Chatbot 🫀

A localized Retrieval-Augmented Generation (RAG) conversational agent built entirely within a Jupyter/Colab Notebook. This project answers heart-health questions by dynamically retrieving factual medical context from authoritative public sources and generating responses using a local instruction-tuned Large Language Model (LLM).

## 🚀 Overview

This chatbot operates without relying on paid external APIs (like OpenAI) or external deployment servers (like Streamlit or Flask). It uses web scraping to build a knowledge base, FAISS for fast vector similarity search, and a Hugging Face LLM for natural language generation—all integrated into an interactive notebook interface using `ipywidgets`.

## 🛠️ Tech Stack

* **Language Model:** `Qwen/Qwen2.5-1.5B-Instruct`
* **Embedding Model:** `sentence-transformers/all-MiniLM-L6-v2`
* **Vector Store:** FAISS (Facebook AI Similarity Search)
* **Web Scraping:** BeautifulSoup4, Requests
* **UI & Environment:** IPyWidgets, Google Colab / Jupyter Notebook
* **Core Libraries:** PyTorch, Hugging Face `transformers`

## ✨ Key Features

* **Automated Knowledge Ingestion:** Scrapes, cleans, and chunks clinical guidelines directly from the National Heart, Lung, and Blood Institute (NHLBI).
* **Dense Passage Retrieval:** Converts text chunks into vector embeddings and retrieves the top-4 most relevant passages for any user query.
* **Hallucination Control:** System prompts strictly bind the LLM to the retrieved clinical context. If the context does not contain the answer, the bot is instructed to admit it.
* **Interactive Notebook UI:** Features a built-in text area and chat output widget, allowing seamless conversation tracking without leaving the notebook.

## ⚙️ How It Works (The Pipeline)

1. **Scraping:** Extracts primary readable text from targeted NHLBI URLs.
2. **Chunking:** Splits the text into overlapping segments (850 characters, 140-character overlap) respecting sentence boundaries.
3. **Indexing:** Generates 384-dimensional embeddings for each chunk and loads them into a FAISS `IndexFlatIP` vector database.
4. **Retrieval:** Converts the user's question into an embedding, searches FAISS for the nearest matches, and formats them into a context prompt.
5. **Generation:** Passes the retrieved context and recent conversation history to the Qwen LLM to synthesize a grounded, conversational answer.

## 💻 Getting Started

To run this project yourself:

1. Upload the `HEART_CHATBOX.ipynb` file to [Google Colab](https://colab.research.google.com/).
2. Change the runtime to enable a GPU:
   * Go to **Runtime** > **Change runtime type**.
   * Select **T4 GPU** as the hardware accelerator.
   * Click **Save**.
3. Click **Runtime** > **Run all** to install dependencies, ingest the data, build the FAISS index, and load the models.
4. Scroll to the bottom of the notebook to interact with the chat widget.

## ⚠️ Disclaimer

**This chatbot is an educational project and does not provide professional medical advice.** It relies on an AI language model and automated text retrieval. For real medical concerns, emergencies, or severe symptoms, always consult a qualified healthcare provider or seek urgent medical care.
