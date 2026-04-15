# 🧬 Craig's Science Machine

![Project Maturity](https://img.shields.io/badge/Maturity-MOCK--UP-orange)

### 🔬 Fidelity Note
This codebase represents a **Functional Mock-up**. While it contains actual integration logic for the Google Gemini API and physical file parsing via `pdftotext` and `python-docx`, it is currently structured as a Jupyter Notebook/Colab script. It lacks production-grade environment variable management (API keys are hardcoded strings), formal logging, and persistent data storage.

### 🗺️ Technical Roadmap
1. **Environment Security**: Transition hardcoded `API_KEY` to `.env` or Secret Manager usage.
2. **Orchestration**: Wrap the script into a CLI or FastAPI service to handle concurrent requests.
3. **Persistence Layer**: Implement a database (PostgreSQL/MongoDB) to track document metadata and synthesis history.
4. **Robust Parsing**: Replace `subprocess.run` calls with native Python libraries (like `PyMuPDF`) for better error handling and performance.

### 💎 Value Chunks
*   **Multi-Format Ingestion**: Includes a versatile `read_file` utility capable of handling `.pdf`, `.docx`, and `.txt` files seamlessly.
*   **API Resilience**: Implements a dedicated retry loop with specific handling for `429 Rate Limit` errors, ensuring stability during bulk processing.
*   **Native Layout Extraction**: Utilizes `pdftotext -layout` to preserve document structure, which is critical for context-aware AI analysis.