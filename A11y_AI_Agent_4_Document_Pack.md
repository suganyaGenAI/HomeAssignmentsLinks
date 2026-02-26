# A11y AI Agent -- Structured Documentation Pack

Generated on: 2026-02-26 05:31:53

============================================================ A. USE CASE
DOCUMENT ============================================================

## Use Case Name

AI-Powered Accessibility Validation Agent for Appian Applications

## Use Case Description

A local developer-first AI agent that validates accessibility compliance
for Appian applications through static SAIL analysis and runtime DOM
inspection. The agent integrates with Jira, Figma, Appian documentation,
and Aurora accessibility checklist to generate structured WCAG-aligned
defects with remediation guidance.

## Problem Statement

Accessibility validation in Appian applications is currently manual,
fragmented, and reactive. Issues are identified late in release cycles,
duplication of defects occurs, and there is no intelligence layer that
connects user stories, defects, and design documentation.

## Why This Use Case

-   Accessibility compliance is mandatory (WCAG).
-   Manual validation slows release cycles.
-   No intelligent duplicate detection.
-   No SAIL-aware remediation support.
-   Lack of trend visibility across releases.

## Expected Benefits

-   Early detection (design-time + runtime).
-   Reduced duplicate defects.
-   AI-assisted severity adjustment.
-   SAIL-specific remediation guidance.
-   CI/CD enforceability.
-   Trend analytics for accessibility debt.
-   Enterprise governance support.

============================================================ B. INPUT &
OUTPUT DEFINITION
============================================================

## Input Sources

1.  Jira REST API
    -   User stories with accessibility inclusions
    -   Defect database
2.  Figma REST API
    -   UI specifications
    -   Flow definitions
    -   Component metadata
3.  Appian Application Package
    -   SAIL interfaces (static analysis source)
4.  Appian Documentation (Pre-indexed)
    -   https://docs.appian.com/
5.  Aurora Accessibility Checklist
    -   https://appian-design.github.io/aurora/accessibility/checklist/
6.  Runtime Browser Capture
    -   outerHTML (full page)
    -   outerHTML (selected component)
    -   ARIA attributes
    -   DOM structure

------------------------------------------------------------------------

## Output Produced by the Agent

1.  HTML Accessibility Defect Report

    -   Defect Severity
    -   WCAG Reference + Level
    -   Observation
    -   Expectation
    -   Remediation (HTML + SAIL)
    -   Confidence Score
    -   Duplicate Similarity Indicator

2.  JSON Report (for CI/CD)

3.  CLI Exit Code

    -   0 → No blocking defects
    -   1 → Critical defects found
    -   2 → Engine failure

4.  Trend Data Storage

    -   Release-based defect metrics

============================================================ C.
ARCHITECTURE / TECHNICAL DOCUMENT
============================================================

## Design Principle

-   Simple architecture
-   API-first
-   Single local backend
-   No microservices
-   Modular components
-   Fully local AI models
-   AWS-hosted vector DB only

  -----------------------------
  1\. High-Level Architecture
  -----------------------------

Chrome Extension\
→ Local FastAPI Backend\
→ Static Engine + Runtime Engine\
→ Local Embedding Model\
→ AWS Vector DB\
→ Local LLM\
→ HTML Generator

  ------------------------
  2\. API-First Approach
  ------------------------

All capabilities exposed through REST endpoints.

Core APIs:

POST /scan/runtime\
POST /scan/static\
POST /scan/deep\
GET /report/{scan_id}\
GET /trend/{app_id}

CLI and Web UI consume the same APIs.

  --------------
  3\. DB Layer
  --------------

A. AWS Vector DB - Stores embeddings - Separate namespace per Appian
application

B. Local SQLite (simple persistence) - Scan metadata - Release tags -
Trend metrics

No distributed databases. No event streaming.

  ---------------
  4\. Web Layer
  ---------------

1.  Chrome Extension (Capture Layer)
    -   Manifest V3
    -   DOM capture
    -   Sends JSON to backend
2.  Optional Local Dashboard
    -   Simple React or Streamlit UI
    -   View reports
    -   View trends

  ------------------------------
  5\. Core Internal Components
  ------------------------------

-   SailParser
-   RuleEngine
-   RuntimeDomAnalyzer
-   EmbeddingService
-   VectorSearchService
-   SeverityAdjuster
-   RemediationGenerator
-   HtmlReportBuilder
-   TrendAggregator

All components are modular and independently testable.

============================================================ D. COPILOT
PLAN MODE OUTPUT
============================================================

(PLAN ONLY -- NO CODE GENERATION)

  ------------------
  1\. API -- FIRST
  ------------------

Step 1: Define API Schemas (Pydantic Models) - ScanRequest -
StaticScanRequest - DefectModel - ReportModel

Step 2: Implement Core API Routes - Runtime Scan Endpoint - Static Scan
Endpoint - Report Retrieval Endpoint - Trend Endpoint

Step 3: Add CLI wrapper to call APIs

  ------------------
  2\. DB -- SECOND
  ------------------

Step 1: Define SQLite schema - Applications - Scans - Defects - Releases

Step 2: Configure AWS Vector DB namespaces

Step 3: Implement Repository Layer - ScanRepository - DefectRepository -
TrendRepository

  ------------------
  3\. WEB -- THIRD
  ------------------

Step 1: Build Chrome Extension - Capture full DOM - Capture selected
DOM - Send payload

Step 2: Build Minimal Dashboard - List scans - View defect report - View
trends

  -----------------------
  4\. DESIGN GUIDELINES
  -----------------------

-   Keep architecture simple.
-   Avoid microservices.
-   Avoid event-driven complexity.
-   Build in small testable components.
-   Validate each layer independently.
-   Maintain API contracts.
-   Write unit tests for RuleEngine and Parser first.
-   Add AI reasoning only after deterministic checks are stable.

============================================================ END OF
DOCUMENT ============================================================
