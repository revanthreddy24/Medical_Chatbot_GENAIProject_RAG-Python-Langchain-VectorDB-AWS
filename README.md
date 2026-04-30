# 🩺 Medical Chatbot (RAG-Based)

## 🤔 Why did I build this?

Most people don’t have easy access to clear and reliable medical information.

If you’ve ever tried searching your symptoms online, you probably know the experience:
- You get flooded with too many articles  
- Half of them contradict each other  
- The language is too technical to understand  
- And somehow every search makes things feel worse 😅  

I wanted to build something simpler.

This chatbot lets a user ask medical questions in plain English and get **clear, structured, and relevant answers** — without jumping across multiple websites.

It’s not meant to replace doctors (obviously), but it helps people **understand what’s going on** before taking the next step.

---

## 📌 What this project is

This is an end-to-end **Medical Chatbot** built using a **Retrieval-Augmented Generation (RAG)** approach.

Instead of training or fine-tuning a model, this project:
- Stores medical knowledge in a searchable format  
- Retrieves only what’s relevant  
- Uses an LLM to generate answers based on that context  

So the system doesn’t “guess” — it **answers based on actual medical content**.

---

## 🧠 How it works (simple)

1. User asks a question  
2. System finds the most relevant medical content  
3. That context is passed to the language model  
4. Model generates a response based on that information  

Think of it like:

> Search → Understand → Answer

---

## 🏗️ Tech Stack

### 📚 Data
- *The Gale Encyclopedia of Medicine* (~637 pages)

### ⚙️ Core Components
- LangChain (orchestration)
- OpenAI LLM (response generation)
- Hugging Face Embeddings  
  - `sentence-transformers/all-MiniLM-L6-v2`

### 🧮 Vector Database
- Pinecone

### 🌐 Interface
- Flask (backend)
- HTML + CSS (frontend)

---

## 🔄 Workflow

### 1. Data Preparation
- Extract text from PDF  
- Split into chunks (~500 tokens)  
- Convert chunks into embeddings  

### 2. Store Knowledge
- Store embeddings in Pinecone  
- Enables semantic similarity search  

### 3. Query Handling
- Convert user query into embedding  
- Retrieve top 3 relevant chunks  

### 4. Response Generation
- Combine retrieved context + user query  
- Send to LLM  
- Generate final answer  

---

## 📂 Project Structure
