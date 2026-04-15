# The Rock Knew All Along

![Maturity: Functional-Prototype](https://img.shields.io/badge/Maturity-Functional--Prototype-yellow)
![Stack: Python/Gemini](https://img.shields.io/badge/Stack-Python_%7C_Gemini_2.0-blue)

## Project Overview
A document synthesis and summarization engine designed to extract and reinterpret content from various file formats (PDF, DOCX, TXT) using the Gemini 2.0 Flash model. The system provides 'faintly unhinged' scientific summaries, specifically optimized for handling large documents through chunking and iterative API processing.

## Technical Stack
- **LLM Engine:** Google Generative AI (`gemini-2.0-flash`)
- **Document Parsing:** `pdfplumber`, `pdftotext` (Poppler), `python-docx`
- **Environment:** Python (Colab optimized)
- **Output Generation:** `fpdf2` for potential PDF synthesis

## Core Capabilities
- **Multi-Format Ingestion:** Automated detection and reading of PDFs, Word documents, and text files.
- **Resilient API Interaction:** Implements a retry mechanism with exponential backoff for 429 (Quota) errors.
- **Smart Chunking:** Splits large text blocks into manageable 6000-character segments for LLM context window compatibility.
- **Automated Summarization:** Generates context-aware summaries across entire directories of files.

## Standalone Value Chunks
- **The Retry Logic:** A robust `ask_gemini` wrapper that handles common API failures gracefully.
- **Layout-Preserving PDF Reading:** Uses `pdftotext -layout` for superior text extraction compared to basic PDF readers.

## Production Gaps
- **Secrets Management:** API keys are currently hardcoded as placeholders.
- **Environment Dependencies:** Hardcoded `/content/` paths limit portability outside of Google Colab.
- **Error Boundaries:** Broad exception catching without structured logging.

## Path to Production
1. **Environment Abstraction:** Implement `python-dotenv` for API key management and command-line arguments for input/output directories.
2. **Dependency Management:** Move `!pip` installs to a standard `requirements.txt` file.
3. **Asynchronous Processing:** Implement `asyncio` to handle multiple file summaries in parallel, respecting rate limits via a semaphore.
4. **Containerization:** Dockerize the Poppler and Python environment to ensure consistent behavior across different host OSs.