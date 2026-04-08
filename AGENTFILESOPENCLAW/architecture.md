# 🏗️ System Architecture — OpenClaw Mechanics RAG System

> Maintained by: Architect Agent
> Owner approval required before any structural changes.

---

## SYSTEM OVERVIEW

The OpenClaw Mechanics RAG System is a document intelligence platform that allows
technicians to search business operating manuals, shop documents, and technical files
using natural language. It reduces downtime by eliminating the need to manually
navigate scattered documentation.

```
┌─────────────────────────────────────────────────────────┐
│ TECHNICIAN / USER │
└─────────────────────┬───────────────────────────────────┘
 │ Natural language query
 ▼
┌─────────────────────────────────────────────────────────┐
│ FRONTEND (Next.js) │
│ • Folder-style navigation (Machine→System→Doc) │
│ • Search interface + results display │
│ • Offline cache layer │
└─────────────────────┬───────────────────────────────────┘
 │ API calls
 ▼
┌─────────────────────────────────────────────────────────┐
│ BACKEND API (Node.js) │
│ • Query routing │
│ • Auth / user roles │
│ • Document management │
└──────┬──────────────────────────────────┬───────────────┘
 │ │
 ▼ ▼
┌──────────────┐ ┌────────────────────────┐
│ RAG PIPELINE│ │ POSTGRESQL DATABASE │
│ │ │ • Document metadata │
│ 1. Embed │ │ • User data │
│ query │ │ • pgvector extension │
│ 2. Retrieve │◄────────────────│ • Embeddings store │
│ chunks │ └────────────────────────┘
│ 3. Rerank │
│ 4. Generate │
│ answer │
└──────┬───────┘
 │
 ▼
┌─────────────────────────────────────────────────────────┐
│ INGESTION PIPELINE │
│ Raw Files → Parse → Clean → Chunk → Embed → Store │
│ Supported: PDF, DOCX, TXT, CSV │
└─────────────────────────────────────────────────────────┘
```

---

## DOCUMENT HIERARCHY

All documents are organized in a strict hierarchy that mirrors how technicians
naturally navigate physical folders:

```
Business / Organization
└── Machine / Asset
 └── System (e.g., Engine, Hydraulics, Electrical)
 └── Subsystem (e.g., Fuel System, Cooling)
 └── Document (Manual, Procedure, Warning Sheet)
 └── Section / Page
 └── Chunk (RAG unit)
```

---

## RAG PIPELINE DETAIL

### Ingestion (Data Agent → AI/RAG Agent)
1. Upload raw file (PDF/DOCX/TXT)
2. Parse text + extract metadata (part numbers, warnings, torque specs)
3. Chunk by semantic section (not fixed token size)
4. Generate embeddings (OpenAI or local model)
5. Store chunks + embeddings in pgvector
6. Index metadata for hybrid search

### Retrieval (AI/RAG Agent)
1. Embed user query
2. Hybrid search: vector similarity + keyword (BM25)
3. Rerank results by relevance + document hierarchy
4. Return top chunks with metadata
5. Generate answer with source citations
6. Suggest \"next step\" action if applicable

---

## OFFLINE ARCHITECTURE

| Mode | Capability |
|---|---|
| Online | Full LLM generation, cloud embeddings, sync |
| Offline | Local embeddings (pre-computed), local LLM (Ollama), cached docs |
| Degraded | Keyword search only, no generation |

---

## DECISIONS LOG
See /docs/decisions.md for all pending and approved architectural decisions.
