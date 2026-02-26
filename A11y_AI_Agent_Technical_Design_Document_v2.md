# A11y AI Agent for Appian Applications

## Technical Architecture & System Design Document (Expanded with Technology Stack)

Version: 2.0\
Generated on: 2026-02-26 05:18:21

------------------------------------------------------------------------

# 1. Executive Summary

This document defines the full technical architecture, technology stack,
system design, and execution model for a Local Developer-First A11y AI
Agent designed for Appian applications.

The system supports:

-   Static SAIL code analysis
-   Runtime DOM analysis via Chrome extension
-   AI-based reasoning (fully local LLM)
-   AWS-hosted vector database
-   Jira + Figma live integrations
-   WCAG-compliant HTML defect generation
-   CI/CD enforcement
-   Multi-application isolation

------------------------------------------------------------------------

# 2. Complete Technology Stack

## 2.1 Frontend / Capture Layer

  Component           Technology
  ------------------- -----------------------------------
  Browser Extension   Chrome Extension (Manifest V3)
  DOM Capture         Vanilla JS + Chrome DevTools APIs
  UI Panel            React (optional lightweight UI)
  Communication       REST to Local Backend

------------------------------------------------------------------------

## 2.2 Backend (Local Service)

  Layer            Technology
  ---------------- ------------------------------
  API Framework    FastAPI (Python)
  Web Server       Uvicorn
  Authentication   Token-based (Jira / Figma)
  Configuration    YAML-based config files
  CLI Interface    Typer (Python CLI framework)

------------------------------------------------------------------------

## 2.3 Static SAIL Analysis Engine

  Capability           Technology
  -------------------- -----------------------------
  Package Extraction   Python Zip/XML parsing
  SAIL Parsing         Custom SAIL AST Parser
  Rule Engine          Python-based rule evaluator
  Partial Embedding    Local Embedding Model

------------------------------------------------------------------------

## 2.4 Runtime Analysis Engine

  Capability             Technology
  ---------------------- --------------------------
  DOM Processing         BeautifulSoup / lxml
  Accessibility Checks   Custom rule framework
  ARIA Validation        WCAG rule mapping engine

------------------------------------------------------------------------

## 2.5 Embedding Layer

  Component             Technology
  --------------------- -------------------------------------------------
  Embedding Model       Open-source model (e.g., BGE / Instructor / E5)
  Runtime               Local inference via HuggingFace Transformers
  Vector Storage        AWS OpenSearch / Pinecone (AWS Hosted)
  Namespace Isolation   Per Appian Application

------------------------------------------------------------------------

## 2.6 AI Reasoning Layer

  Component              Technology
  ---------------------- ----------------------------------
  Local LLM              Llama / Mistral (quantized)
  Runtime Engine         Ollama or Local vLLM
  Prompt Orchestration   LangChain (optional)
  Severity Adjustment    AI-assisted classification layer

------------------------------------------------------------------------

## 2.7 Knowledge Sources Integration

  Source             Integration Method
  ------------------ ----------------------------------
  Jira               Jira REST API (Token Auth)
  Figma              Figma REST API
  Appian Docs        Pre-indexed locally
  Aurora Checklist   Pre-indexed + version monitoring
  Defect DB          Embedded + similarity search

------------------------------------------------------------------------

## 2.8 Reporting & Output

  Capability      Technology
  --------------- -----------------------------
  HTML Report     Jinja2 Template Engine
  JSON Output     Pydantic models
  Trend Storage   PostgreSQL (Local optional)
  Dashboard       Optional Streamlit UI

------------------------------------------------------------------------

## 2.9 CI/CD Integration

  Capability         Technology
  ------------------ --------------------------
  CLI Execution      Typer CLI
  Exit Codes         Severity-based
  Pipeline Support   GitHub Actions / Jenkins

------------------------------------------------------------------------

# 3. System Architecture Overview

Chrome Extension\
→ FastAPI Local Backend\
→ Static + Runtime Engine\
→ Local Embedding Model\
→ AWS Vector DB\
→ Local LLM Reasoning\
→ HTML Generator\
→ CLI / CI Pipeline

------------------------------------------------------------------------

# 4. Static Analysis Flow

Appian Application Package\
→ Extract SAIL Objects\
→ AST Parsing\
→ Rule Engine Execution\
→ Partial Embedding\
→ Similarity Lookup\
→ Defect Draft

------------------------------------------------------------------------

# 5. Runtime Analysis Flow

User Clicks Extension\
→ Capture Full or Selected DOM\
→ Send to Backend\
→ Quick Scan or Deep Analysis\
→ RAG Retrieval\
→ AI Reasoning\
→ Defect Output

------------------------------------------------------------------------

# 6. Defect Output Structure

Each defect contains:

-   Defect Severity
-   WCAG Reference + Level (A/AA/AAA)
-   Observation
-   Expectation
-   Remediation (HTML + SAIL)
-   Confidence Score
-   Duplicate Similarity Indicator

------------------------------------------------------------------------

# 7. Multi-Application Architecture

Each Appian Application Includes:

-   Dedicated Vector Namespace
-   Separate Rule Config
-   Independent Trend History
-   Isolated Embedding Context

------------------------------------------------------------------------

# 8. Trend & Analytics Engine

Tracks:

-   Accessibility debt over releases
-   Component recurrence patterns
-   Severity distribution
-   WCAG compliance coverage
-   Mean time to remediation

------------------------------------------------------------------------

# 9. Security Model

-   All embeddings generated locally
-   All LLM reasoning executed locally
-   AWS vector DB secured via IAM roles
-   Jira + Figma tokens encrypted locally
-   Partial code embedding only (no business logic)

------------------------------------------------------------------------

# 10. Implementation Phases

Phase 1 -- Static + Runtime Engine\
Phase 2 -- Embeddings + AWS Vector DB\
Phase 3 -- Local LLM + Severity Intelligence\
Phase 4 -- Analytics + CI/CD + Governance

------------------------------------------------------------------------

# 11. Strategic Positioning

This system is:

-   Enterprise Accessibility Intelligence Platform
-   CI/CD Gatekeeper
-   Release Quality Signal
-   Compliance Enforcement Engine
-   Architecture Innovation Asset

------------------------------------------------------------------------

End of Document.
