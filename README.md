# RAG Code Review Assistant (Python)

This project provides a minimal, code-only RAG pipeline for Python code review.
It ingests Python code, retrieves review guidance from a small knowledge base,
sends the prompt to a code-focused LLM, and returns issues, improved code, and
an explanation.

## Setup

1) Create a virtual environment (recommended).
2) Install dependencies:

```bash
pip install -r requirements.txt
```

## Configure LLM

Set environment variables for an OpenAI-compatible API (default config targets Groq):

- `LLM_API_BASE` (default: `https://api.groq.com`)
- `LLM_API_KEY` (required)
- `LLM_MODEL` (default: `llama-3.3-70b-versatile`)
- `LLM_TEMPERATURE` (default: `0.2`)
- `LLM_MAX_TOKENS` (default: `1200`)
- `LLM_TIMEOUT_S` (default: `60`)

## Run

```bash
python -m rag_review.cli --code-file path\to\file.py
```

You can also pass inline code:

```bash
python -m rag_review.cli --code-string "print('hello')"
```

Or pipe via stdin:

```bash
type path\to\file.py | python -m rag_review.cli
```

The output is written to `review_output.json` by default (pretty-printed). You can override it:

```bash
python -m rag_review.cli --code-file path\to\file.py --output-file my_review.json
```

To write compact single-line JSON:

```bash
python -m rag_review.cli --code-file path\to\file.py --compact
```

## Tests

```bash
pytest
```
