import os
import re
from pdf2image import convert_from_path
import pytesseract

# -------- CONFIG --------
PDF_FILE = "Document.pdf"   # input pdf file
OUTPUT_DIR = "Output_txt" # output folder
BASE_NAME = "Doc"   # base name for txt files
LANG = "eng"               # OCR language
# ------------------------

# Make output folder if not exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# Convert PDF pages to images
print("Converting PDF pages to images...")
pages = convert_from_path(PDF_FILE, dpi=300)

for i, page in enumerate(pages, start=1):
    print(f"OCR on page {i} ...")
    # OCR with Tesseract
    text = pytesseract.image_to_string(page, lang=LANG)

    # --- Basic Formatting Cleanup ---
    text = re.sub(r'\n{2,}', '\n\n', text)  # collapse extra newlines
    text = re.sub(r' {2,}', ' ', text)      # collapse extra spaces
    text = text.strip()

    # Add page header
    structured_text = f"==== {BASE_NAME} Page {i} ====\n\n{text}\n"

    # Save to txt file
    output_file = os.path.join(OUTPUT_DIR, f"{BASE_NAME}_{i:02d}.txt")
    with open(output_file, "w", encoding="utf-8") as f:
        f.write(structured_text)

    print(f"Saved {output_file}")

print("OCR complete. Check the 'resume_txts' folder.")
