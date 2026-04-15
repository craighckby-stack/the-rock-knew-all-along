# the-rock-knew-all-along

A high-throughput document processing and summarization engine utilizing the Google Gemini 2.0 Flash API. This project specializes in extracting text from diverse formats (PDF, DOCX, TXT) and generating idiosyncratic, scientifically-styled summaries via Large Language Models (LLMs).

## Features

- **Multi-Format Extraction**: Integrated support for PDF (via `poppler-utils`), DOCX (via `python-docx`), and plaintext files.
- **Gemini 2.0 Flash Integration**: Leverages the latest Gemini models for high-speed, long-context window processing.
- **Chunked Analysis**: Automatically segments large documents into manageable fragments to optimize API token usage and context relevance.
- **Robust Error Handling**: Implements exponential backoff and rate-limit handling (429 errors) for stable execution on Gemini's free tier.
- **Customizable Prompting**: Features a unique "scientific yet unhinged" persona for generating non-standard metadata and insights.

## Prerequisites

- Python 3.8+
- Poppler (for PDF processing)
- Google Gemini API Key (obtainable from [Google AI Studio](https://aistudio.google.com))

## Installation

Install the required system and Python dependencies:

bash
sudo apt-get install -qq poppler-utils
pip install -q google-generativeai pdfplumber python-docx fpdf2


## Usage

1.  **Configure API Key**: Update `ApiGemini.py` with your `API_KEY`.
2.  **Add Documents**: Place target documents in the `/content/` directory.
3.  **Run the Synthesizer**:

bash
python ApiGemini.py


## Technical Architecture

1.  **Ingestion Layer**: `read_file()` detects extensions and routes files to specific parsing logic (e.g., `pdftotext` with layout preservation for PDFs).
2.  **Processing Layer**: `summarise()` divides text into 6000-character chunks, ensuring comprehensive coverage of lengthy documents.
3.  **Inference Layer**: `ask_gemini()` manages the stateful interaction with the `gemini-2.0-flash` model, handling retries and rate limiting.

## License

This project is licensed under the MIT License - see the LICENSE file for details.