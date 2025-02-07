---
dg-publish: true
---


Got it! Here’s a **complete, step-by-step guide** to building your **web-based PDF summarization tool**, including fine-tuning a Hugging Face model, integrating it into Flask, and deploying it.

---

# **📌 Project Overview**

We will:

1. **Extract text from PDFs**
2. **Fine-tune an AI model** for summarization
3. **Build a Flask API** to process and return summaries
4. **Create a Svelte-based frontend**
5. **Deploy the application online**

---

# **🚀 Step 1: Set Up the Project**

## **1. Install Python and Virtual Environment**

Make sure you have **Python 3.8+** installed. Then, create and activate a virtual environment:

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python -m venv venv
source venv/bin/activate
```

## **2. Install Required Libraries**

```bash
pip install flask transformers torch pdfminer.six pymupdf datasets accelerate
```

- **Flask** → Backend
- **Transformers** → AI model
- **Torch** → Required for AI models
- **pdfminer.six / pymupdf** → PDF text extraction
- **Datasets / Accelerate** → Fine-tuning

---

# **📌 Step 2: Fine-Tune the Model**

## **1. Prepare Training Data**

Create `data.csv` with custom training examples:

```csv
text,summary
"Long document content here","Short summary here"
"Another long document","Its summary"
```

## **2. Load the Dataset**

Create a file `train_model.py`:

```python
from datasets import load_dataset

dataset = load_dataset("csv", data_files="data.csv")
```

## **3. Tokenize Data**

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("facebook/bart-large-cnn")

def preprocess_data(batch):
    inputs = tokenizer(batch["text"], max_length=1024, truncation=True, padding="max_length")
    labels = tokenizer(batch["summary"], max_length=150, truncation=True, padding="max_length")
    return {"input_ids": inputs["input_ids"], "labels": labels["input_ids"]}

dataset = dataset.map(preprocess_data, batched=True)
```

## **4. Train the Model**

```python
from transformers import AutoModelForSeq2SeqLM, TrainingArguments, Trainer

model = AutoModelForSeq2SeqLM.from_pretrained("facebook/bart-large-cnn")

training_args = TrainingArguments(
    output_dir="./results",
    per_device_train_batch_size=2,
    per_device_eval_batch_size=2,
    evaluation_strategy="epoch",
    save_strategy="epoch",
    logging_dir="./logs",
    num_train_epochs=3
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=dataset["train"]
)

trainer.train()
```

## **5. Save and Load the Model**

```python
model.save_pretrained("my_summarizer")
tokenizer.save_pretrained("my_summarizer")
```

To load it later:

```python
from transformers import pipeline
summarizer = pipeline("summarization", model="my_summarizer")
```

---

# **📌 Step 3: Build Flask Backend**

## **1. Project Structure**

```
pdf_summarizer/
│── static/        # Frontend assets (CSS, JS)
│── templates/     # HTML files
│── uploads/       # Temporary PDF storage
│── app.py        # Flask application
│── train_model.py # Model fine-tuning
│── requirements.txt
```

## **2. Create `app.py`**

```python
from flask import Flask, request, render_template, jsonify
import os
import fitz  # PyMuPDF
from transformers import pipeline

app = Flask(__name__)
UPLOAD_FOLDER = "uploads"
os.makedirs(UPLOAD_FOLDER, exist_ok=True)
app.config["UPLOAD_FOLDER"] = UPLOAD_FOLDER

# Load fine-tuned model
summarizer = pipeline("summarization", model="my_summarizer")

def extract_text_from_pdf(pdf_path):
    text = ""
    with fitz.open(pdf_path) as doc:
        for page in doc:
            text += page.get_text()
    return text

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/summarize", methods=["POST"])
def summarize_pdf():
    if "file" not in request.files:
        return jsonify({"error": "No file uploaded"}), 400

    file = request.files["file"]
    if file.filename == "":
        return jsonify({"error": "No selected file"}), 400

    file_path = os.path.join(app.config["UPLOAD_FOLDER"], file.filename)
    file.save(file_path)

    text = extract_text_from_pdf(file_path)
    if len(text.strip()) == 0:
        return jsonify({"error": "No text found in PDF"}), 400

    summary = summarizer(text[:1024], max_length=150, min_length=50, do_sample=False)
    return jsonify({"summary": summary[0]["summary_text"]})

if __name__ == "__main__":
    app.run(debug=True)
```

---

# **📌 Step 4: Build Frontend**

## **1. Create `templates/index.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PDF Summarizer</title>
</head>
<body>
    <h1>Upload a PDF to Summarize</h1>
    <form id="uploadForm" enctype="multipart/form-data">
        <input type="file" id="fileInput" name="file" accept=".pdf">
        <button type="submit">Summarize</button>
    </form>
    <h2>Summary:</h2>
    <p id="summary"></p>

    <script>
        document.getElementById("uploadForm").addEventListener("submit", async function(event) {
            event.preventDefault();
            let fileInput = document.getElementById("fileInput").files[0];
            let formData = new FormData();
            formData.append("file", fileInput);

            let response = await fetch("/summarize", {
                method: "POST",
                body: formData
            });

            let result = await response.json();
            document.getElementById("summary").innerText = result.summary || result.error;
        });
    </script>
</body>
</html>
```

---

# **📌 Step 5: Run and Test**

## **1. Start the Flask Server**

```bash
python app.py
```

## **2. Open in Browser**

Visit: **`http://127.0.0.1:5000/`**

---

# **📌 Step 6: Deploy Online**

## **1. Deploy Backend to Render**

1. Push your code to GitHub
2. Sign up at [Render](https://render.com/)
3. Create a **new Flask web service**
4. Deploy the app

## **2. Deploy Frontend with Netlify**

1. Upload your frontend files
2. Set the backend API URL
3. Deploy 🎉

---

# **🎯 Next Steps**

✅ Improve **UI with Svelte**  
✅ Add **Q&A Feature** (Ask questions about the PDF)  
✅ Store summaries in **SQLite**

Want me to **help with Svelte UI**? 🚀