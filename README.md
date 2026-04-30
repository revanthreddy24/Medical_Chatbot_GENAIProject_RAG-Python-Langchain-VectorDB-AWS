🩺 Medical Chatbot (RAG-Based)
🤔 Why did I build this?

Most people don’t have easy access to clear and reliable medical information.

If you’ve ever tried searching your symptoms online, you probably know the experience:

You get flooded with too many articles
Half of them contradict each other
The language is too technical to understand
And somehow every search makes things feel worse 😅

I wanted to build something simpler.

This chatbot lets a user ask medical questions in plain English and get clear, structured, and relevant answers — without jumping across multiple websites.

It’s not meant to replace doctors (obviously), but it helps people understand what’s going on before taking the next step.

📌 What this project is

This is an end-to-end Medical Chatbot built using a Retrieval-Augmented Generation (RAG) approach.

Instead of training a model from scratch or fine-tuning, I used a smarter approach:

Store medical knowledge in a searchable format
Retrieve only what’s relevant
Let an LLM generate answers based on that

So the model doesn’t “guess” — it answers based on actual medical content.

🧠 How it works (simple explanation)
A user asks a question
The system finds the most relevant medical content
That context is sent to the language model
The model generates a response based on that information

Think of it like:

“Search → Understand → Answer”

🏗️ What’s under the hood
📚 Data
Source: The Gale Encyclopedia of Medicine (~637 pages)
This acts as the chatbot’s knowledge base
⚙️ Core Components
LangChain – connects everything together
OpenAI LLM – generates the final answers
Hugging Face Embeddings
Model: sentence-transformers/all-MiniLM-L6-v2
🧮 Vector Database
Pinecone – stores embeddings and enables fast search
🌐 Interface
Flask – backend
HTML + CSS – simple frontend
🔄 What actually happens behind the scenes
Step 1: Data preparation
Extract text from the medical book
Split into smaller chunks (~500 tokens)
Convert each chunk into embeddings
Step 2: Store knowledge
Save embeddings in Pinecone
This makes searching fast and meaningful
Step 3: When a user asks something
The question is converted into an embedding
Top 3 most relevant chunks are retrieved
Step 4: Generate answer
Retrieved content + user question → sent to LLM
LLM generates a clean, contextual response
