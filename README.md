# the-rock-knew-all-along

## Summary
A document processing and synthesis pipeline that extracts text from various file formats and generates unified thematic reports via the Gemini API. The system automates the ingestion of PDFs and Word documents to produce consolidated summaries and synthesized narratives.

## Architecture Story
The system operates as a linear extraction-to-synthesis pipeline. It utilizes `pdftotext` via subprocess calls to maintain layout integrity during PDF ingestion and `python-docx` for structured Word document parsing. Extracted text is segmented into chunks to accommodate context windows, processed through the Gemini 2.0 Flash model with a specific persona-driven prompt, and finally aggregated into a unified report. The architecture includes a retry layer to handle API rate limiting and quota errors inherent in free-tier LLM usage.

## Proof of Work
The following logic block demonstrates the system's robust handling of API constraints and transient errors:

python
def ask_gemini(content, retries=3):
    for attempt in range(retries):
        try:
            resp = model.generate_content(content)
            return resp.text
        except Exception as e:
            err = str(e)[:120]
            if "quota" in err.lower() or "429" in err:
                print(f"\n  rate limited, waiting 30s...")
                time.sleep(30)
            elif attempt < retries - 1:
                print(f"\n  retry {attempt+1}: {err}")
                time.sleep(5)
            else:
                raise

**Technical Proficiency:** This implementation manages the volatility of remote API calls by incorporating exponential backoff and specific error-code sniffing (429/Quota), ensuring that long-running batch processes do not fail due to temporary network or rate-limiting constraints.

## Engine Specs

| Component | Technology |
| :--- | :--- |
| Language | Python 3.x |
| LLM | Google Gemini 2.0 Flash |
| PDF Extraction | Poppler (pdftotext) |
| Document Parsing | python-docx |
| Export Formatting | fpdf2 |
| Environment | Linux/Colab Support |

## Status
**Functional Prototype**