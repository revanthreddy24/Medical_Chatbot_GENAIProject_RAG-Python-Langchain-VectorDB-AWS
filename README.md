# 🩺 Medical Chatbot (RAG-Based)

# Why did I build this?

Most people don’t have easy access to clear and reliable medical information.

If you’ve ever tried searching your symptoms online, you probably know the experience:
- You get flooded with too many articles  
- Half of them contradict each other  
- The language is too technical to understand  
- And somehow every search makes things feel worse  

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

## ⚙️ Key Design Decisions

While building this project, I made a few important design choices to balance **accuracy, speed, and simplicity**. I’m also noting how these choices could be improved for production-scale systems.

---

### 📄 Chunking Strategy
- Each document is split into chunks of **~500 tokens**
- This size works well because most disease-related information in the book is covered within that range  
- An **overlap of 20 tokens** is added between chunks  
  - This helps preserve context  
  - Prevents breaking important medical meaning across chunks  

🔄 **Production improvement:**
- Move from fixed-size chunking → **semantic chunking**
- Instead of splitting by length, chunks are created based on **meaning and context boundaries**
- This significantly improves retrieval quality and downstream answer accuracy  

---

### 🧠 Embedding Model
- Used: `sentence-transformers/all-MiniLM-L6-v2` (Hugging Face)

Why this model?
- Fast and lightweight  
- Open-source (no cost)  
- Generates **384-dimensional vectors**  

Trade-off considered:
- Higher-dimensional models → better accuracy but slower  
- Lower-dimensional models → faster but less expressive  

This model provides a **good balance between speed and semantic understanding**.

🔄 **Production improvement:**
- Use **higher-quality embedding models** with larger dimensions  
- These capture richer semantic relationships and improve retrieval accuracy  
- Trade-off: increased latency and compute cost  

---

### 🧮 Vector Database Choice
- Used: **Pinecone**

Reasons:
- Easy to integrate  
- Optimized for vector search  
- Works well for semantic retrieval use cases  

🔄 **Production improvement:**
- Use **graph-based or advanced indexed vector databases**
- Better indexing strategies can:
  - Improve retrieval latency  
  - Scale more efficiently for large datasets  

---

### 🔍 Similarity Search
- Metric used: **Cosine Similarity**

Why?
- Works well for text embeddings  
- Focuses on semantic similarity rather than magnitude  

🔄 **Production improvement:**
- Combine vector search with **hybrid search (BM25 + embeddings)**  
- This improves results by:
  - Capturing both keyword relevance and semantic meaning  

---

### 📊 Retrieval Strategy
- Top **K = 3** chunks are retrieved for each query  

Reasoning:
- Keeps context focused and relevant  
- Avoids adding too much noise to the LLM input  
- Helps generate more precise answers  

🔄 **Production improvement:**
- Increase the number of retrieved chunks (higher K)  
- Apply **re-ranking using cross-encoder models**  
  - This refines results by scoring relevance more precisely  
- Final pipeline becomes:
  - Retrieve → Re-rank → Select best context  

---

Overall, these decisions were made to ensure the chatbot is:
- ⚡ Fast  
- 🎯 Contextually accurate  
- 💡 Practical to run without heavy infrastructure  

And with the production improvements, it can scale into a much more **robust and high-accuracy system**.





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
