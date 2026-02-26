# A11y AI Agent for Appian Applications

**Technical Architecture & System Design Document**\
Version: 1.0\
Generated on: 2026-02-26 05:16:36

------------------------------------------------------------------------

# 1. Vision

Design a local developer-first Accessibility AI Agent for Appian
applications that supports:

-   Static SAIL code analysis
-   Runtime DOM analysis via Chrome extension
-   AI-assisted severity classification
-   Duplicate detection via vector similarity
-   WCAG-compliant defect generation (HTML format)
-   SAIL-based remediation suggestions
-   Trend analytics across releases
-   CI/CD enforcement
-   Multi-application isolation

------------------------------------------------------------------------

# 2. High-Level Architecture

Chrome Extension → Local Backend (FastAPI) →\
Static Engine + Runtime Engine →\
Local Embedding Model → AWS Vector DB →\
Local LLM Reasoning Layer → HTML Defect Generator → CI/CD

------------------------------------------------------------------------

# 3. Input Sources

  Source                Vector Type   Ingestion Mode
  --------------------- ------------- ----------------------------------
  Jira User Stories     V             Jira REST API
  Jira Defect DB        V             Jira REST API
  Figma Specs + Flows   V             Figma REST API
  Appian Docs           V             Pre-indexed
  Aurora Checklist      V             Pre-indexed + Live Version Check
  SAIL Code             PV            Extracted from Appian Package

------------------------------------------------------------------------

# 4. Static Analysis Engine (SAIL)

Pipeline: Appian Package → Extract SAIL Objects → AST Parsing → Rule
Engine → Partial Embedding

Capabilities: - Missing labels - ARIA inconsistencies - Layout misuse -
Visibility logic errors

------------------------------------------------------------------------

# 5. Runtime Engine

Modes: - Full DOM Capture - Selected Component Capture

Execution Modes: - Quick Scan (\<5s) - Deep Analysis (10--60s)

Captured Data: - outerHTML - ARIA attributes - Computed styles - DOM
hierarchy

------------------------------------------------------------------------

# 6. Embedding & Vector Layer

-   Local open-source embedding model
-   AWS-hosted vector DB
-   Duplicate detection via similarity search
-   RAG retrieval for WCAG and historical defects

------------------------------------------------------------------------

# 7. AI Reasoning Layer (Local LLM)

Responsibilities: - Generate explanation - Adjust severity if needed -
Suggest remediation - Generate SAIL fix snippet - Produce confidence
score

Severity Logic: Baseline rule severity → AI contextual adjustment

------------------------------------------------------------------------

# 8. Defect HTML Output Format

``` html
<div class="a11y-defect">
  <h3>Defect ID: A11Y-001</h3>
  <p><strong>Severity:</strong> High</p>
  <p><strong>WCAG Reference:</strong> 1.1.1 (Level A)</p>
  <p><strong>Observation:</strong> Image missing alternative text.</p>
  <p><strong>Expectation:</strong> All images must include descriptive alt text.</p>
  <p><strong>Remediation (SAIL):</strong> Add altText parameter</p>
  <p><strong>Confidence Score:</strong> 0.92</p>
</div>
```

------------------------------------------------------------------------

# 9. Multi-Application Isolation

-   Dedicated vector namespace per application
-   Separate defect history
-   Independent rule configuration

------------------------------------------------------------------------

# 10. Trend Analytics

Tracks: - Accessibility debt - Recurring violations - Severity
distribution - WCAG compliance score

------------------------------------------------------------------------

# 11. CI/CD Integration

CLI Example: a11y-agent scan --app APP_ID --mode quick

Exit Codes: 0 → No blocking issues\
1 → Critical defects detected\
2 → Engine failure

------------------------------------------------------------------------

# 12. Custom Rule Framework

Supports YAML-based custom rule configuration with versioning and
namespace isolation.

------------------------------------------------------------------------

# 13. Implementation Phases

Phase 1 -- Core Engine\
Phase 2 -- Embedding + RAG\
Phase 3 -- AI Severity + Remediation\
Phase 4 -- Governance + Analytics

------------------------------------------------------------------------

End of Document.
