# McKinsey AI Market Research Engine

**Author:** Shivam Tyagi, Mayuri Laddha, Jignesh Kumar,Archana singh

AI-powered market research workspace with a React frontend and FastAPI backend. See [frontend documentation](frontened/README.md) and [backend documentation](backened/README.md) for setup details.

# API Documentation

## Overview

McKinsey AI Market Research Engine exposes a FastAPI backend for creating and managing AI-powered market research jobs.

The API connects the frontend with the research pipeline and provides access to research jobs, sources, evidence, validations, and generated reports.

## Authentication

Protected endpoints use an authenticated access token.

```text
Authorization: Bearer <supabase_access_token>
```

---

## POST /research

Starts a new research pipeline for the provided query.

### Request

```json
{
  "query": "Impact of Generative AI on education."
}
```

### Response

Creates a research job and starts the McKinsey AI Market Research Engine research pipeline.

The pipeline processes the query through planning, research, evidence extraction, validation, report generation, and citation linking.

---

## GET /research/{job_id}/tasks

Returns the planner tasks associated with a research job.

---

## GET /research/{job_id}/sources

Returns the sources collected during the research process.

---

## GET /research/{job_id}/evidence

Returns the evidence extracted from the collected sources.

---

## GET /research/{job_id}/validations

Returns the validation records associated with the research evidence.

---

## GET /research/{job_id}/report

Returns the generated report for a research job.

---

## GET /docs

FastAPI Swagger UI for exploring and testing the available API endpoints.

```text
http://127.0.0.1:8000/docs
```

---

## Backend Services

The backend uses repository and service components to manage research data and pipeline execution.

* ResearchJobRepository
* PlannerTaskRepository
* SourceRepository
* EvidenceRepository
* ValidationRepository
* ReportRepository
* ResearchService

## Research Pipeline

The API connects to the following research workflow:

**Planner → Research → Extraction → Validation → Citation Builder → Report Agent → Report Linker**

The final output is a structured, evidence-backed research report with traceable citations.
# Architecture

## Overview

McKinsey AI Market Research Engine is an AI-powered market research and strategy engine designed to convert a research query into a structured, evidence-backed report.

The system uses a multi-agent architecture where each agent performs a specific stage of the research workflow.

## Research Pipeline

The main workflow is:

**Planner → Research → Extraction → Validation → Citation Builder → Report Agent → Report Linker**

Each stage contributes to building the final research output.

### 1. Planner Agent

Receives the user's research query and breaks it into smaller research tasks.

### 2. Research Agent

Searches the web for relevant information and collects useful sources for each research task.

### 3. Extraction Agent

Processes the collected sources and extracts relevant evidence, facts, and claims.

### 4. Validation Agent

Checks the extracted evidence for relevance, validity, credibility, and consistency.

### 5. Citation Builder

Organizes source and evidence information so that findings can be connected to their supporting sources.

### 6. Report Agent

Uses the validated evidence to generate a structured research report with findings, insights, and strategic recommendations.

### 7. Report Linker

Links the generated report findings back to their supporting evidence and citations, providing traceability between the report and the underlying research.

## Backend Architecture

The backend is built with FastAPI and contains:

* API layer
* Service layer
* Repository layer
* Database integration
* AI research pipeline

The repository layer manages research jobs, planner tasks, sources, evidence, validations, and reports.

## Database

Supabase is used for database storage.

The system maintains information related to:

* Research Jobs
* Planner Tasks
* Sources
* Evidence
* Validation Records
* Reports
* Feedback
* Memory

## AI and External Services

McKinsey AI Market Research Engine integrates:

* **Google Gemini** for AI-powered planning, extraction, validation, and report generation.
* **Tavily** for web search and source discovery.
* **Supabase** for persistent data storage.

## Frontend and Backend

The frontend provides the user interface for submitting research queries and viewing results.

The FastAPI backend handles API requests and connects them to the research pipeline and database.

## Traceability

A key part of the architecture is the connection between the final report and its supporting evidence.

The Report Linker ensures that important report findings can be traced back to the evidence and sources collected during the research process.
# Deployment Guide

## Frontend

Platform: Vercel

Framework: Vite

Root Directory: `./`

Build Command: `npm run build`

Output Directory: `dist`

## Backend

Platform: Render

Start Command:

```text
uvicorn backend.main:app --host 0.0.0.0 --port $PORT
```

Environment Variables:

* `GOOGLE_API_KEY`
* `TAVILY_API_KEY`
* `SUPABASE_URL`
* `SUPABASE_KEY`

## Database

Supabase PostgreSQL is used for persistent application data.

The database stores information related to research jobs, planner tasks, sources, evidence, validations, reports, and other project data.

## Live Services

* Frontend: Vercel
* Backend: Render
* Database: Supabase
* AI Model: Gemini
* Search Engine: Tavily
