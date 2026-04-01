---
layout: page
icon: fas fa-project-diagram
order: 4
---

# Projects

## Haishi AI Agent — Manufacturing ERP Intelligence Platform

**Consulting project** — Solo 0→1 AI agent for a manufacturing company with real production users.

An AI-powered "Sales Copilot" that sits on top of a legacy ERP system (Zhibang ERP / SQL Server 2008 R2), enabling sales teams to query business data in natural language, get automated insights, and write back to ERP — all without replacing existing systems.

**Tech Stack**: FastAPI · Claude API (tool_use + extended thinking) · React 19 · TypeScript · PostgreSQL · pgvector · Docker · Huawei Cloud

**Key Results**:
- 6,600+ ERP customers synced with automated nightly incremental sync
- 25 business tables with full schema-aware AI query generation
- Automated daily/weekly/monthly reports with AI-driven sales health diagnosis
- Lead discovery pipeline: web scraping → LLM scoring → product-process matching (615+ companies scored)
- ERP write-back with 2-step confirmation (preview → confirm → write)
- Multi-tenant architecture with dual-DB isolation (Core DB + Tenant DB)
- Admin dashboard: conversation trace, usage analytics, user feedback, sync control

**Architecture**: Raw → Silver → Gold three-layer data pipeline (dbt-style), proxy API for tenant isolation, FDW cross-database joins, ASP session management for legacy ERP integration.

---

## AstrumU — ML/AI Platform

**Tech Lead** — Led 6-person AI/ML team building the talent intelligence platform at AstrumU (LevelSet API).

The core challenge: entity resolution at scale — deduplicating and linking people, skills, jobs, courses, and education fields across fragmented data sources (SIS, ATS, LinkedIn, military records).

**Tech Stack**: Ray Serve · vLLM · Kafka CDC · pgvector HNSW · Dagster · FastAPI · PostgreSQL · MLflow

**Key Results**:
- Multi-model serving: 6+ Ray Serve deployments with scale-to-zero, 10K+ entities/day online inference
- Fine-tuned Qwen-2.5 (1.5B-7B) with LoRA SFT for structured extraction — 1-2 orders of magnitude cheaper than API
- Multi-stage RAG pipeline: retrieve → generate → retrieve again → rerank (Google Search + pgvector dual retrieval)
- Event-driven pipelines with Kafka CDC + SCD patterns, replacing Databricks batch jobs
- Unified PostgreSQL platform replacing fragmented Databricks/Postgres/feature store architecture

**Deep Dive**: [The Evolution of MLOps: A Six-Year Journey at AstrumU](/posts/mlops-evolution-at-astrumu/)

---

## CityDecoded — AI-Powered Zoning Copilot

**Side project** — SaaS platform making zoning codes and municipal regulations accessible through AI.

Property owners, developers, and homeowners often can't answer basic questions about what they can build — because zoning codes are written in legal language, buried across hundreds of pages, and vary by city. CityDecoded makes this information actionable.

**Tech Stack**: Next.js · Supabase (Postgres + Auth + Edge Functions) · Google Gemini · MCP · Airflow · Tailwind CSS

**Key Features**:
- Dual-window interface: code browsing + AI chat side by side
- Property-specific reports: buildable envelope, expansion potential, permit roadmap
- Developer API for third-party integration
- ETL pipeline for ingesting and structuring municipal code documents

---

## Writing

### Agentic Data Engineering Series

A 9-part blog series on LinkedIn exploring the data infrastructure requirements for production AI agents. Core thesis: your AI agent's ceiling isn't the model — it's the data underneath.

Topics covered: data quality as agent reliability, semantic layers, context engineering, agent-as-teammate patterns, AI-native team structure, and why you can't vibe-code a data system.

[Read on LinkedIn →](https://www.linkedin.com/in/gongjue/recent-activity/articles/)

### Selected Blog Posts

- [From Data Science to Production: Understanding API, SDK, CLI, and MCP Tools](/posts/from-data-science-to-production-understanding-api-sdk-cli-mcp/)
- [Supabase Is All You Need for RAG Backend](/posts/supabase-is-all-you-need-for-rag-backend/)
- [The Evolution of MLOps: A Six-Year Journey at AstrumU](/posts/mlops-evolution-at-astrumu/)
- [LangGraph Platform: From Code to Cloud Deployment](/posts/langgraph-platform-deploy/)
