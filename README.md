# RagProject

> An end-to-end demo of Retrieval-Augmented Generation (RAG) in a single Jupyter notebook. Shows how to build a tiny “knowledge base,” index it with FAISS, retrieve relevant passages for a user query, and then generate a grounded answer using an LLM.

---

## 📄 Notebook Contents

1. **Introduction & Imports**  
   - Explains the RAG concept.  
   - Imports Python libraries: `sentence-transformers`, `faiss`, `langchain`, `openai` (or `langchain_ollama`), etc.

2. **Data Preparation**  
   - Defines a small list of text snippets (`docs`) that form our toy knowledge base.  
   - (Optionally) shows how to load snippets from a file.

3. **Embedding & Index Construction**  
   - Loads a Sentence-Transformers model (e.g. `all-MiniLM-L6-v2`).  
   - Converts each document into a vector embedding.  
   - Builds a FAISS `IndexFlatL2` index and adds all embeddings.

4. **Retriever Function**  
   - Implements `retrieve(query: str, k: int)` that:  
     1. Embeds the user query.  
     2. Searches the FAISS index for the top-k nearest documents.  
     3. Returns the original text snippets.

5. **LLMChain Setup**  
   - Configures an LLM wrapper (OpenAI or Ollama).  
   - Defines a `PromptTemplate` that injects retrieved context before the user’s question.  
   - Creates an `LLMChain` that, given `context` + `question`, produces an answer.

6. **Interactive Q&A Loop**  
   - Runs a simple REPL:  
     ```python
     while True:
         q = input("Your question (or 'exit'): ")
         if q.lower() in ("exit", "quit"): break
         print(rag_answer(q))
     ```  
   - Demonstrates how retrieval and generation work together.

7. **Sample Outputs**  
   - A few example runs are captured, showing how the system retrieves snippets like “What is RAG?” or “Tell me about FAISS” and produces coherent answers.

---

## 🚀 How to Run

1. **Clone the repo** (or download the notebook):
   ```bash
   git clone https://github.com/tejak2719/your_rag_repo.git
   cd your_rag_repo
