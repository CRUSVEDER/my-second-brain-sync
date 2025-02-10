---
dg-publish: true
---
---
# **AI-Powered PDF Summarization & Q&A Web App**

## **1. Project Overview**

This project is an **AI-powered web application** designed to **summarize PDFs** and **answer questions** based on their content. It integrates **two AI models**:

- **A fine-tuned text summarization model** for document summarization.
- **DeepSeek-R1 via Ollama** for answering user queries about the document.

The application consists of a **Flask backend** for AI processing and a **Svelte-based frontend** for user interaction.

---

## **2. Technology Stack**

|Component|Technology Used|
|---|---|
|**Frontend**|Svelte, HTML, CSS, JavaScript|
|**Backend**|Flask (Python)|
|**Summarization Model**|Fine-tuned BART/T5 (Hugging Face)|
|**Q&A Model**|DeepSeek-R1 via Ollama|
|**Database (Optional)**|SQLite/PostgreSQL for storing summaries|
|**Deployment**|Render (backend), Netlify (frontend)|

---

## **3. Summarization Model Training**

### **3.1 Model Choice**

The summarization feature is powered by a **fine-tuned sequence-to-sequence model** using Hugging Face Transformers, such as:

- **BART (`facebook/bart-large-cnn`)**
- **T5 (`t5-small` or `t5-base`)**

### **3.2 Training Process**

#### **Step 1: Prepare Dataset**

We create a CSV dataset (`data.csv`):

```csv
text,summary
"Long document content here","Short summary here"
"Another long document","Its summary"
```

#### **Step 2: Tokenization**

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("facebook/bart-large-cnn")

def preprocess_data(batch):
    inputs = tokenizer(batch["text"], max_length=1024, truncation=True, padding="max_length")
    labels = tokenizer(batch["summary"], max_length=150, truncation=True, padding="max_length")
    return {"input_ids": inputs["input_ids"], "labels": labels["input_ids"]}
```

#### **Step 3: Fine-Tuning**

```python
from transformers import AutoModelForSeq2SeqLM, TrainingArguments, Trainer

model = AutoModelForSeq2SeqLM.from_pretrained("facebook/bart-large-cnn")
training_args = TrainingArguments(output_dir="./results", num_train_epochs=3)
trainer = Trainer(model=model, args=training_args, train_dataset=dataset["train"])
trainer.train()
```

#### **Step 4: Save Model**

```python
model.save_pretrained("my_summarizer")
tokenizer.save_pretrained("my_summarizer")
```

---

## **4. DeepSeek-R1 Integration for Q&A**

### **4.1 Ollama Setup**

DeepSeek-R1 is hosted **locally** using Ollama:

```bash
ollama serve
```

To verify:

```bash
curl http://localhost:11434/api/tags
```

Expected Output:

```json
{"models":[{"name":"deepseek-r1:1.5b"}]}
```

### **4.2 Q&A Processing**

Flask sends requests to Ollama for document-based Q&A:

```python
prompt = f"Context: {pdf_text[:4000]}\nQuestion: {question}\nAnswer:"
response = requests.post(OLLAMA_URL, json={"model": MODEL_NAME, "prompt": prompt}, stream=True)
```

---

## **5. Backend Implementation (Flask API)**

### **5.1 Flask API Endpoints**

|Endpoint|Method|Description|
|---|---|---|
|`/summarize`|POST|Summarizes an uploaded PDF|
|`/ask`|POST|Answers questions about the PDF|

### **5.2 Flask API Working in Detail**

- **Flask initializes** the web application and sets up routes.
- When a **PDF file is uploaded**, Flask extracts text using `PyMuPDF`.
- The extracted text is passed to **two different AI models**:
    - The **fine-tuned summarization model** (BART/T5) processes the text and generates a summary.
    - DeepSeek-R1 (via Ollama) is queried when a user asks questions based on the document.
- Responses are formatted as JSON and sent to the frontend.

### **5.3 Updated `app.py` (Combining Both Models)**

```python
from flask import Flask, request, jsonify
import requests
from transformers import pipeline

app = Flask(__name__)
OLLAMA_URL = "http://localhost:11434/api/generate"
MODEL_NAME = "deepseek-r1:1.5b"
summarizer = pipeline("summarization", model="my_summarizer")

def extract_text_from_pdf(file_path):
    return "Extracted text from PDF..."

@app.route("/summarize", methods=["POST"])
def summarize_pdf():
    pdf_text = extract_text_from_pdf("uploaded.pdf")
    summary = summarizer(pdf_text[:1024], max_length=150, min_length=50)
    return jsonify({"summary": summary[0]["summary_text"]})

@app.route("/ask", methods=["POST"])
def ask_question():
    question = request.json.get("question", "")
    prompt = f"Context: {pdf_text[:4000]}\nQuestion: {question}\nAnswer:"
    response = requests.post(OLLAMA_URL, json={"model": MODEL_NAME, "prompt": prompt}, stream=True)
    return jsonify({"answer": response.json().get("response", "No answer found")})

if __name__ == "__main__":
    app.run(debug=True)
```

---

## **6. Future Enhancements**

✅ **Fine-tune DeepSeek on custom documents** ✅ **Improve UI with real-time updates** ✅ **Optimize prompts for better Q&A accuracy** ✅ **Implement document history storage**

---

## **7. Conclusion**

This project successfully integrates **personal fine-tuned models** and **DeepSeek-R1** to provide a powerful **PDF Summarization & Q&A Web App**. It is designed to be scalable and customizable for different use cases.

🚀 **Next Steps:** Deploy the system and test its performance on real-world data!

---
### **🚀 Algorithms Used in This Project**

This project integrates **two main AI components**, each using a different algorithm for **Summarization** and **Q&A Processing**.

---

## **1️⃣ Summarization Algorithm (Seq2Seq Transformer)**

The **summarization model** uses a **Sequence-to-Sequence (Seq2Seq) Transformer** architecture, specifically:

- **BART (Bidirectional Auto-Regressive Transformer)**
- **T5 (Text-to-Text Transfer Transformer)**

### **🔹 How It Works?**

1. **Encoder:** Converts input text into dense representations (embeddings).
2. **Decoder:** Generates a concise summary by predicting words **token by token**.
3. **Cross-Attention:** Links input and output tokens to refine the summary.
4. **Fine-Tuning with Supervised Learning:** The model is trained with **pairs of text and summaries**, optimizing for **Minimum Cross-Entropy Loss**.

### **🔹 Model Training**

- **Objective Function:** **Maximum Likelihood Estimation (MLE)**
- **Loss Function:** **Negative Log-Likelihood Loss (NLLLoss)**
- **Optimization Algorithm:** **AdamW Optimizer**
- **Gradient Clipping:** Prevents **exploding gradients** during training.
- **Beam Search:** Used during inference to generate better summaries.

---

## **2️⃣ DeepSeek-R1 Algorithm (Causal Language Model)**

The **DeepSeek-R1 model** (via **Ollama**) follows a **Causal Language Model (CLM)** approach:

- **Autoregressive Generation** → Predicts text **sequentially**.
- **Self-Attention Mechanism** → Uses past words to generate the next word.
- **Transformer Decoder-Only Architecture** (like GPT).

### **🔹 How It Works for Q&A?**

1. **Input Processing:**
    - The question is combined with the **context** (extracted PDF text).
    - A prompt is created:
        
        ```
        Context: [Extracted PDF text]
        Question: [User Question]
        Answer:
        ```
        
2. **Tokenization:** Converts text into token IDs.
3. **Autoregressive Generation:** DeepSeek predicts each token **one by one** until the answer is complete.
4. **Sampling Methods:**
    - **Greedy decoding** (default)
    - **Top-k sampling** (better diversity)
    - **Temperature scaling** (controls randomness)

### **🔹 Training Objective**

- **Pre-trained on Massive Text Data** (books, Wikipedia, CommonCrawl).
- **Fine-tuned for instruction-following tasks (like ChatGPT).**
- **Uses Reinforcement Learning with Human Feedback (RLHF) to improve responses.**

---

## **📌 Summary of Algorithms**

|**Feature**|**Algorithm Used**|
|---|---|
|**Summarization**|Seq2Seq Transformer (BART/T5)|
|**Optimization**|AdamW Optimizer, Cross-Entropy Loss|
|**Inference**|Beam Search, Top-k Sampling|
|**Q&A Processing**|Causal Language Model (DeepSeek-R1)|
|**Training Method**|RLHF + Autoregressive Generation|

This combination ensures **accurate document summarization** and **intelligent Q&A responses**. 🚀

Would you like a **mathematical breakdown of these algorithms** as well? Let me know! 🔥


---
