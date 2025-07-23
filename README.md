# 📘 Overview of xdoc2json
xdoc2json is a PyQt5-based desktop GUI tool for extracting structured content using OCR, table parsers, and graph detection from document files (.txt, .docx, and .pdf only ) and exporting that content into a well-organized JSON or JSONL format.

It is designed for researchers, data engineers, analysts, and AI practitioners who want to convert documents into machine-processable formats for downstream tasks like NLP, search, summarization, or graph analysis.

## Install

    pip install -r requirements.txt

## Run

    python xdoc2json.py


# 🔧 Key Features
## 1. Multi-format Document Support
Supports .txt, .docx, and .pdf.

Automatically detects the file type and applies the appropriate parser.

## 2. PyQt5 GUI Interface
Intuitive GUI with buttons for file selection, removal, and export.

Lists selected files for visibility.

Modal dialogs for errors, confirmations, and status messages.

## 3. Text Extraction
.txt: Reads file as UTF-8.

.docx: Extracts text using docx2txt, with fallback to python-docx.

.pdf: Extracts page-wise text using PyMuPDF (fitz).

## 4. Table Extraction
.docx: Extracts tables using python-docx, cleans them into row-column JSON arrays.

.pdf: Uses pdfplumber for robust PDF table parsing.

## 5. Image Extraction & OCR
Extracts images embedded in .docx or .pdf.

Performs OCR using pytesseract.

Extracts positional text elements and bounding boxes for layout preservation.

## 6. Graph Representation from Text
Uses regex to detect simple "A -> B" or "A --> B" patterns in OCR'd text.

Constructs directed graphs using networkx.

## 7. Diagram Context Extraction
Captures bounding boxes, confidence scores, and text fragments using OCR data.

Normalizes and packages them into a structured object.

## 8. Batch Processing
Handles multiple documents in a single run.

Status labels and confirmation dialogs help manage workflow.

## 9. JSON and JSONL Output Support
JSON: Single structured dictionary with per-file keys.

JSONL: Newline-delimited format with one JSON object per file.

json

```json
{
  "myfile.pdf": {
    "content_type": "pdf",
    "text_by_page": {"page_1": "..." },
    "tables": [{ "id": "table_1", "data": [["A", "B"], ["1", "2"]] }],
    "images": {
      "image_1.png": {
        "ocr_text": "...",
        "diagram_context": { "recognized_items": [...], "notes": "..." },
        "graph_representation": { "nodes": [...], "edges": [...] }
      }
    }
  }
}
```

## ✅Summary
| Component        | Tool Used               | Purpose                              |
| ---------------- | ----------------------- | ------------------------------------ |
| GUI              | PyQt5                   | Interactive file selection & control |
| Text Extraction  | docx2txt, fitz          | Extract raw readable content         |
| Table Extraction | python-docx, pdfplumber | Structure tabular data               |
| Image OCR        | pytesseract             | Retrieve text from diagrams/images   |
| Graph Detection  | networkx                | Represent relationships visually     |
| Output Formats   | JSON, JSONL             | Developer- and ML-friendly           |
