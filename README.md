# LLM Zoomcamp 2026

My coursework and projects for [LLM Zoomcamp](https://github.com/DataTalksClub/llm-zoomcamp) by [DataTalks.Club](https://datatalks.club/) — a free, hands-on course on building production-ready LLM applications with RAG, agents, and vector search.

## About the Course

LLM Zoomcamp is a 10-week course covering Retrieval-Augmented Generation, vector search, embeddings, AI agents, function calling, evaluation, monitoring, hybrid search, and reranking. This repo tracks my homework, notes, and the final capstone project as I work through it.

## Progress

| Module | Topic | Status |
|---|---|---|
| 1 | Agentic RAG | [Complete](agentic_rag.ipynb) |
| 2 | Vector Search |  |
| 3 | Orchestration |  |
| 4 | Evaluation |  |
| 5 | Monitoring | |
| 6 | Best Practices |  |
| 7 | End-to-End Project |  |
| Capstone | Final Project |  |

## Module 1: Agentic RAG

In this module I built a RAG pipeline that answers questions about the LLM Zoomcamp course material itself, then turned it into an agent that can search and re-search on its own.

### What it does

- Pulls all lesson markdown files directly from the [course GitHub repo](https://github.com/DataTalksClub/llm-zoomcamp) using `gitsource`
- Indexes them with `minsearch` for keyword search, both at the document level and chunked (2000 chars, 1000-char step) for finer-grained retrieval
- Wraps a baseline RAG flow (`search → build prompt → call LLM`) using a shared `RAGBase` helper
- Builds an **agentic** version on top: instead of a fixed one-shot search, the LLM is given a `search` tool and decides for itself when and how many times to query the index, including recovering from typos or vague queries by reformulating its own search terms
- Uses [ToyAIKit](https://github.com/DataTalksClub/llm-zoomcamp/blob/main/01-agentic-rag/lessons/15-frameworks.md) to handle the agent loop (tool registration, schema generation from type hints/docstrings, and the underlying `while` loop) instead of hand-rolling it
- Tracks token usage and cost per call via the OpenAI Responses API's `usage` field



### Running it

```bash
# install dependencies
uv add openai python-dotenv gitsource minsearch toyaikit

# set your API key
echo "OPENAI_API_KEY=your-key-here" > .env

# run the notebook
jupyter notebook agentic_rag.ipynb
