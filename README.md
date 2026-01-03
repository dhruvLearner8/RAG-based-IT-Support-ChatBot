
# 🧠 RAG-based IT Support Troubleshooting Assistant
## 📌 Problem Statement

IT support teams frequently deal with repetitive troubleshooting queries related to VPNs, networks, firewalls, and servers. While documentation exists, it is:

Scattered across multiple sources

Often verbose and hard to search

Not conversational or context-aware

The goal of this project is to explore how Retrieval-Augmented Generation (RAG) can be used to build an intelligent troubleshooting assistant that:

Retrieves relevant technical documentation

Grounds responses in real sources

Reduces hallucinations compared to vanilla LLMs

Handles ambiguous or underspecified user queries

This project focuses on engineering the RAG framework and retrieval logic, rather than full UI or production deployment.

## 🛠️ Solution Overview

This project implements a category-aware RAG pipeline using LangChain and ChromaDB, designed specifically for IT troubleshooting scenarios.

At a high level:

User Query
   ↓
Category Classification (VPN / Network / Firewall / Server / General)
   ↓
Query Expansion (RAG Fusion)
   ↓
Vector Similarity Retrieval (ChromaDB)
   ↓
Context Aggregation
   ↓
LLM-based Answer Generation


The system is currently implemented and demonstrated inside a Jupyter Notebook to allow fast iteration, debugging, and experimentation with retrieval strategies.

## 🧩 Key Engineering Decisions
1️⃣ Category-Based Retrieval

Instead of storing all documents in a single vector store, documentation is grouped by domain:

VPN

Network

Firewall

Server

General IT

Each category has its own ChromaDB collection, reducing retrieval noise and improving relevance.

## 2️⃣ RAG Fusion (Multi-Query Expansion)

To improve recall, a single user question is expanded into multiple semantically related queries using an LLM.

Example:

“Why is my VPN disconnecting every 60 seconds?”

This is rewritten into multiple variants that target:

Protocol issues

Timeout settings

Network instability

Configuration mismatches

Each expanded query retrieves documents independently, increasing coverage and robustness.

## 3️⃣ Semantic Vector Retrieval with ChromaDB

Documents are chunked and embedded using OpenAI embeddings

Top-k relevant chunks are retrieved via cosine similarity

Retrieved chunks are flattened and merged into a single context window

This ensures the LLM answer is grounded in actual documentation, not guesswork.

## 4️⃣ Explicit Context Construction

Rather than relying on opaque chains, the project:

Explicitly flattens retrieved documents

Builds the context passed to the LLM manually

Makes it easy to inspect why a specific answer was generated

This design choice improves debuggability and transparency, which is critical for RAG systems.

## 📒 Current Implementation

Implemented as a Jupyter Notebook for clarity and experimentation

Supports:

Document ingestion

Vector storage

Query expansion

Retrieval

Context-aware answer generation

The notebook format allows recruiters and reviewers to see each step of the RAG pipeline clearly, including intermediate outputs.

## ⚠️ Current Limitations

This project is intentionally scoped for learning and demonstration:

No web UI or chat frontend (yet)

No persistent conversation memory across sessions

Limited document corpus (focused, not exhaustive)

No automated web crawler for enterprise documentation

These tradeoffs were made to prioritize RAG correctness and retrieval quality over surface-level completeness.

## 🚀 Future Improvements

Planned extensions include:

Converting the pipeline into a FastAPI backend

Adding multi-turn conversation memory

Introducing source attribution per response

Expanding the document corpus

Building a simple chat interface for live interaction

## 🧠 Why This Project Matters

This project demonstrates:

Practical understanding of RAG architectures

Hands-on experience with LangChain and vector databases

Awareness of hallucination risks in LLMs

Engineering judgment in scoping and tradeoffs

It is designed as a foundation for a production-grade IT support assistant.

## 🧰 Tech Stack

Python

LangChain

OpenAI (LLM + embeddings)

ChromaDB

Jupyter Notebook



Install dependencies

Set your OpenAI API key

Run the notebook cells sequentially
