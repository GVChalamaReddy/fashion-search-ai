# fashion-search-ai
## Project Overview

This system implements a complete three-layer RAG architecture to enable natural language search over fashion product catalogs from the Myntra dataset using OpenAI embeddings, ChromaDB vector database, cross-encoder reranking, and GPT-3.5-turbo for generation.

Users can search for products using conversational queries like "comfortable kurta for daily wear under 2000" and receive intelligent, context-aware recommendations.

## DataSet - https://www.kaggle.com/datasets/djagatiya/myntra-fashion-product-dataset

## Key Features

- **Semantic Search:** Natural language understanding for product queries
- **Intelligent Chunking:** Three strategies (Fixed, Semantic, Product-based) with comparative analysis
- **Two-Stage Retrieval:** Fast vector search + precise cross-encoder re-ranking
- **Query Caching:** Persistent caching of search results in ChromaDB (cache TTL) for latency reduction on repeated queries.
- **LLM Generation:** GPT-3.5-turbo with sophisticated prompt engineering
- **Modular Architecture:** Easily swap embedding models, vector databases, or LLMs


## Architecture

### Layer 1: Embedding Layer
- Data preprocessing and cleaning
- Strips HTML, fills missing values, normalizes text
- Multiple chunking strategies - Supports fixed, semantic, product-based chunking - used product-based chunking  in project
- SentenceTransformers / OpenAI embeddings - Generates vector embeddings
- Stores all chunks and metadata in ChromaDB

### Layer 2: Search Layer
- Embeds incoming user queries
- Persistent caching of search results in ChromaDB (cache TTL)
- ChromaDB retrieves top-N similar products
- Cross-Encoder (MiniLM) reranks by contextual relevance
- Cache stored for fast repeated queries

### Layer 3: Generation Layer
- OpenAI API integration
- Comprehensive prompt engineering
- Few-shot learning
- Assembles LLM prompt (query + retrieved items + instructions)
- Injects context and few-shot examples
- Calls OpenAI GPT-3.5-turbo for fully natural recommendations
- Response formatting

## Installation

### Tech Stack
- Python 3.8+
- OpenAI API key (for generation layer)
- openai==1.54.0 
- chromadb==0.5.5 
- sentence-transformers==3.2.1 
- pandas==2.2.3 
- numpy==1.26.4 
- beautifulsoup4==4.12.3 
- python-dotenv==1.0.1

## Test Queries

The system includes 3 comprehensive test queries demonstrating different search patterns:

### Query 1: Wedding Outfit
**Query:** "I need a comfortable ethnic outfit for a wedding ceremony, preferably in red or maroon color"

**Top Result:** Nayo Women Red Floral Printed Kurta (Rs 3,699, 4.09/5.0)

### Query 2: Budget Daily Wear
**Query:** "Looking for casual daily wear kurtas under 2000 rupees with good ratings"

**Top Result:** AHIKA Women Black & Green Printed Straight Kurta (Rs 1,350, 21K reviews)

### Query 3: Festive Palazzo Sets
**Query:** "Show me trendy palazzo sets with dupatta in bright colors for festive occasions"

**Top Result:** InWeave Orange Solid Kurta with Palazzos (Rs 5,899, 4.12/5.0)

## Configuration

### Embedding Models
**OpenAI (API):**
- `text-embedding-ada-002`

### Generation Models
- `gpt-3.5-turbo` (fastest, cheapest)

### Chunking Strategies

- `fixed`: Equal-sized chunks with overlap
- `semantic`: Sentence-based with size limits
- `attribute`: Product-specific structured chunks **Recommended**

## Chunking Strategy Comparison

| Strategy | Chunks/Product | Avg Length | Accuracy | Best For |
|----------|---------------|------------|----------|----------|
| Fixed | 3.2 | 485 chars | Medium | General use |
| Semantic | 2.8 | 543 chars | High | Documents |
| **Attribute** | **2.4** | **467 chars** | **Very High** | **E-commerce** |


## Acknowledgments
- This project was inspired by Upgrad IIIT Bangalore PG program on ML and AI. 
- This project was based on Retrieval-Augmented Generation (RAG)

## Contact
Created by @[GVChalamaReddy](https://github.com/GVChalamaReddy) - feel free to contact me!
---



