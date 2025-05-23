# Flickdone_Data_Engineer_Task

This task demonstrates a simplified ETL (Extract–Transform–Load) data pipeline designed for training Braille translation AI models. The goal is to process unstructured documents (like scanned books) into a clean, structured, Braille-aligned dataset for accessibility purposes.

---

## 📌 Objective

To simulate Flickdone’s internal pipeline that transforms printed books into Braille data using open-source OCR and translation tools.

---

## ⚙️ Setup Instructions

1. Clone the Repo & Upload PDFs
  - git clone https://github.com/your-username/braille-ai-pipeline.git
  - Upload your PDFs into the /data/raw_pdfs/ folder or use the ones already included.
    
2. Run the Google Colab Notebook
  - Open Braille_AI_Data_Pipeline.ipynb in Google Colab:
  - Make sure all setup cells run correctly (e.g., installing tesseract).
  - Run each pipeline step in order.
  - Final JSON output will be saved in /data/braille/parallel_corpus.json.

---

## 🎯 Note

Due to system constraints, the Liblouis toolchain was not fully compatible inside Colab, so a Unicode mapping approach was used to simulate Braille output.
The process can be extended to support:
  - Hindi text using Google Translate API before conversion.
  - Annotation of visual elements like tables or figures.

---

## 🧰 Technologies Used

- Python (Google Colab)
- Tesseract OCR (`pytesseract`)
- PDF to image (`pdf2image`)
- PIL (Image handling)
- Braille Unicode Translation using open-source mapping (Liblouis-inspired logic)

---

## 📂 Folder Structure
```
data/
├── raw_pdfs/ # Uploaded scanned book PDFs
├── ocr_texts/ # Cleaned extracted text files
├── structured/ # structured JSON
└── braille/ # Final plain-to-braille parallel corpus
```
---

## 📚 Collected Data

The dataset consists of 3 scanned English-language books downloaded from the [Internet Archive](https://archive.org/):

1. *1984* by George Orwell  
2. *The Martian* by Andy Weir  
3. *Animal Farm* by George Orwell

Each book was uploaded in PDF format and contains clean OCR-friendly text.

---

## 🔄 Pipeline Overview

The pipeline consists of the following steps:

### 1️⃣ Collect
- Upload scanned book PDFs to `/data/raw_pdfs/`.

### 2️⃣ Extract & Clean (OCR)
- Convert each PDF page into an image using `pdf2image`.
- Apply Tesseract OCR (`pytesseract`) to extract the raw text.
- Clean and normalize the text to remove headers/footers or noise.

### 3️⃣ Structure
- Split extracted text into paragraphs.
- Create a structured JSON object for each paragraph with:
  - `id`: unique paragraph identifier
  - `source`: book name
  - `language`: content language (English)
  - `content`: paragraph text

Saved to: `/data/structured/structured_text.json`

### 4️⃣ Translate to Braille
- Convert each paragraph's content to Braille using a Unicode-mapped conversion.
- Open-source Braille table (Liblouis-compatible) was referenced but replaced with direct Unicode logic due to environment compatibility issues.

### 5️⃣ Generate Parallel Corpus
- Combine original text and Braille translation with metadata.
- Save as a list of JSON objects containing:
  - `braille`: Unicode Braille translation
  - `id`: paragraph ID
  - `source`: book title
  - `content`: plain text

Saved to: `/data/braille/parallel_corpus.json`

---

## ✅ Output Sample

```json
{
  "braille": "⠁⠇⠇ ⠁⠝⠊⠍⠁⠇⠎ ⠁⠗⠑ ⠑⠟⠥⠁⠇⠂ ⠃⠥⠞ ⠎⠕⠍⠑ ⠁⠝⠊⠍⠁⠇⠎ ⠁⠗⠑ ⠍⠕⠗⠑ ⠑⠟⠥⠁⠇ ⠞⠓⠁⠝ ⠕⠞⠓⠑⠗⠎⠲"
  "id": "Animal Farm_pg1",
  "source": "Animal Farm",
  "content": "All animals are equal, but some animals are more equal than others."
}
```

---

## Demo Video

Please find the demo video and all the files in the given [drive link](https://drive.google.com/drive/folders/1D96hromyQk1Y8inwUPnN_ptg0xuasUym?usp=sharing)

---

## 📩 Contact

For questions:

ABHITESH MADHARAM – abhitesh1369@gmail.com

[GitHub](https://github.com/Abhitesh-1369)
