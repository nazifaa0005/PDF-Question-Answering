# PDF-Question-Answering


This Google Colab notebook answers questions using text from an uploaded PDF. It extracts the text, splits it into shorter passages, ranks passages related to the question, and uses the pretrained `deepset/minilm-uncased-squad2` model to select an answer.

Uploading a PDF gives the model text to search. It does not train the model.

## How to run

1. Open `PDF_Question_Answering.ipynb` in Google Colab.
2. Run the cells from top to bottom.
3. When prompted, upload one PDF containing selectable text.
4. Run the question cell to see the answers.

To ask another question about the same PDF, run:

```python
print(answer_from_pdf(PDF_PATH, "What is the main finding?"))
```

To use a different PDF, rerun the upload cell first.

## How it works

- **PyMuPDF** extracts text from each page.
- The text is cleaned and split into overlapping passages of up to 300 tokens.
- **TF-IDF and cosine similarity** rank passages by relevance to the question.
- The pretrained QA model checks the ranked passages and returns an answer found in the text.

## Example results and limitations

The notebook’s saved output shows seven correct answers to the prepared questions about Bangladesh. In a separate seagrass test, the tool returned the expected facts for nine answerable questions and rejected a question about a budget that was not stated in the PDF.

The tool does not always reject missing answers. When asked for Bangladesh’s national bird, it incorrectly returned “royal bengal tiger,” which the PDF identifies as the national animal. Scanned image-only PDFs also need OCR before this notebook can read them.

## Files

- `PDF_Question_Answering.ipynb` — the notebook

The model downloads when the notebook runs; its weights are not stored in this repository.
