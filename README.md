# LSmith-WebScrapingChallenge

## Web Scraping to Vector Database
**IT 721 VS1 Spring 2026 | Walsh College | Lamonte Smith**

A production-grade web scraping and semantic search pipeline that extracts content from publicly accessible URLs, generates dense vector embeddings, and stores them in a ChromaDB vector database for semantic retrieval — forming a complete RAG foundation.

## Architecture
URLs → BeautifulSoup4 Scraper → Text Chunker → SentenceTransformer Embedder → ChromaDB (Docker) → Semantic Search

## Tech Stack
| Component | Technology |
|-----------|-----------|
| Web Scraping | requests + BeautifulSoup4 |
| Text Chunking | Custom sliding window (200 words, 20 overlap) |
| Embeddings | all-MiniLM-L6-v2 (SentenceTransformers) |
| Vector Database | ChromaDB (Docker container, port 8000) |
| Container Runtime | Docker (GitHub Codespaces) |

## Dataset
Three Wikipedia articles selected for doctoral research domain alignment:
- Autonomous Vehicles — 44 chunks
- Operational Technology — 7 chunks
- 5G — 22 chunks
Total: 73 chunks | 88,626 characters | 384-dimensional embeddings

## Setup
1. docker pull chromadb/chroma
2. docker run -d --name chromadb -p 8000:8000 chromadb/chroma
3. pip install -r requirements.txt
4. jupyter notebook web_scraping_vector_db.ipynb

## Results
- URLs scraped: 3/3
- Total chunks: 73
- Embedding dimensions: 384
- Top similarity score: 0.6408

## Author
Lamonte Smith | Milford, MI
DBA (AI/ML Leadership) & PhD in Technology (Cybersecurity) — Walsh College
