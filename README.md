# ESG Intelligence Platform

## System Charter

This repository contains the **ESG Intelligence Platform**, a
production-grade AI system designed to support **governed, explainable,
and auditable ESG scoring** within enterprise environments.

The platform is intended for **internal deployment** and **controlled pilot
use** where ESG outputs must withstand executive review, compliance scrutiny,
and post-hoc audit.

This is an **enterprise decision system**, not a research artifact.

---

## Problem Context

Most ESG scoring implementations rely on opaque NLP similarity models or
unconstrained machine learning outputs.

Such approaches introduce unacceptable risk in enterprise contexts due to:

- Non-deterministic behavior
- Inability to explain score drivers
- Lack of governance and policy enforcement
- No reproducible audit trail
- Unclear human accountability

In regulated or reputation-sensitive organizations, these limitations
prevent operational adoption.

**ESG assessment is not a prediction task.  
It is a governed decision process.**

---

## System Objective

The objective of this platform is to:

- Convert unstructured ESG disclosures into **consistent ESG scores**
- Provide **explicit, reviewable rationale** for each score
- Enforce **policy, constraint, and override rules**
- Preserve **human accountability**
- Enable **full auditability and replay**

The system supports decision-making.  
It does not replace decision ownership.

---

## Design Principles

The platform is built on the following principles:

- Deterministic execution over probabilistic inference
- Policy encoded as executable logic
- Clear separation between signal generation and decision enforcement
- Explicit handling of uncertainty
- Governance treated as a system property, not an add-on

Model outputs are treated as **inputs**, not decisions.

---

## High-Level Architecture

```bash

esg-intelligence-platform/
│
├── README.md                      # Executive + technical overview
├── pyproject.toml                 # Locked dependencies & build
├── Dockerfile
├── docker-compose.yml             # Local + staging parity
├── .env.example
├── .gitignore
│
├── platform/                      # Application platform layer
│   ├── main.py                    # FastAPI entrypoint
│   ├── api/
│   │   ├── v1/
│   │   │   ├── routes.py          # /score /explain /health
│   │   │   └── schemas.py         # Strong API contracts
│   │   └── middleware.py          # Auth, logging, tracing
│   │
│   ├── core/
│   │   ├── config.py              # Env + secrets
│   │   ├── logging.py             # JSON structured logs
│   │   ├── errors.py              # Typed exceptions
│   │   └── lifecycle.py           # Startup/shutdown hooks
│   │
│   └── services/
│       ├── scoring_service.py     # Orchestration logic
│       ├── explanation_service.py
│       └── report_service.py      # PDF / dashboard outputs
│
├── intelligence/                  # ML & decision intelligence
│   ├── ingestion/
│   │   ├── document_loader.py     # PDF / HTML / reports
│   │   └── validation.py          # Schema & data quality
│   │
│   ├── nlp/
│   │   ├── preprocessing.py
│   │   ├── embeddings.py
│   │   └── keyword_models.py
│   │
│   ├── scoring/
│   │   ├── esg_scoring.py          # Core ESG logic
│   │   ├── weighting.py            # Policy-driven weights
│   │   └── normalization.py
│   │
│   ├── explainability/
│   │   ├── shap_engine.py
│   │   ├── rationale_builder.py
│   │   └── counterfactuals.py
│   │
│   ├── governance/
│   │   ├── bias_checks.py
│   │   ├── constraints.py          # Score bounds
│   │   ├── audit_trail.py
│   │   └── override_policy.py
│   │
│   └── registry/
│       ├── model_registry.py
│       └── versioning.py
│
├── pipelines/                     # Automation & workflows
│   ├── training_pipeline.py
│   ├── scoring_pipeline.py
│   └── batch_reporting_pipeline.py
│
├── configs/                       # Policy as code
│   ├── esg_policy.yaml
│   ├── thresholds.yaml
│   └── governance.yaml
│
├── artifacts/                     # Versioned outputs
│   ├── models/
│   ├── reports/
│   └── audit_logs/
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── governance/
│
├── docs/                          # What execs & auditors read
│   ├── architecture.md
│   ├── data_flow.md
│   ├── scoring_methodology.md
│   ├── explainability.md
│   ├── governance_and_bias.md
│   ├── security_and_privacy.md
│   └── deployment_guide.md
│
└── ci/
    └── github_actions.yml
```

Each stage is independently versioned, testable, and auditable.

---

## Platform Structure & Responsibilities

### Application Platform Layer (`platform/`)
Responsible for controlled access, orchestration, and delivery.

- **FastAPI entrypoint** for scoring and explanation endpoints
- Strong request/response schemas
- Middleware for logging, tracing, and policy enforcement
- Service layer coordinating scoring, explanation, and reporting

This layer contains no business logic related to ESG scoring.

---

### Intelligence Layer (`intelligence/`)
Responsible for all decision intelligence and governance logic.

#### Ingestion
- Document loading from PDFs, HTML, and reports
- Schema validation and data quality enforcement

#### NLP
- Controlled preprocessing and feature extraction
- Deterministic text representations
- Avoidance of unconstrained free-form generation

#### Scoring
- ESG dimension scoring (Environmental, Social, Governance)
- Policy-driven weighting and normalization
- Deterministic score computation

#### Explainability
- Factor-level contribution analysis
- Rationale construction for human review
- Counterfactual and sensitivity analysis

#### Governance
- Bias and sanity checks
- Score bounds and constraints
- Mandatory justification for overrides
- Immutable audit logging

#### Registry
- Model and policy versioning
- Explicit lifecycle control

---

### Pipelines (`pipelines/`)
Defines automated and batch workflows:

- Training and evaluation pipelines
- Batch scoring execution
- Report generation workflows

Pipelines are designed to be reproducible and observable.

---

### Configuration (`configs/`)
All scoring logic, thresholds, and governance rules are defined as
**versioned configuration**, not hard-coded behavior.

Changes to configuration are treated as policy changes.

---

### Artifacts (`artifacts/`)
Stores versioned outputs:

- Trained models
- Executive and analytical reports
- Immutable audit logs

Artifacts are the system’s source of truth for historical decisions.

---

### Testing (`tests/`)
The test suite enforces:

- Deterministic behavior
- Governance guarantees
- Constraint enforcement
- API contract stability

Governance logic is explicitly testable.

---

### Documentation (`docs/`)
Contains material intended for:

- Architecture review
- Compliance and audit teams
- Security and privacy assessment
- Operational handover

This documentation is part of the system, not supplementary material.

---

## Intended Use

This platform is intended for:

- ESG and sustainability analysis
- Risk and compliance review
- Internal strategy and governance workflows
- Advisory and consulting engagements

It is **not** intended for:

- Fully automated decision-making
- Consumer-facing ESG scoring
- Unconstrained experimentation

---

## Operational Characteristics

- Environment-scoped configuration and secrets
- No hard-coded credentials
- Deterministic outputs for identical inputs
- All decisions are logged, replayable, and inspectable
- Designed for internal network deployment

Additional controls may be layered to meet organizational security
or regulatory requirements.

---

## Scope and Limitations

This system provides **decision support**.

Final ESG determinations remain the responsibility of designated human
reviewers and governance bodies.

The platform is explicitly designed to make that responsibility
**visible, documented, and enforceable**.

---

## Change Management

This repository represents a **controlled system**.

Changes affecting scoring logic, governance rules, or outputs should be
reviewed through formal change management and documented via versioning.

---

## Ownership

Maintained by:

Vignesh Murugesan  
AI / Data Science Engineer  

Focus Areas:  
Decision Intelligence · Explainable AI · Governed Machine Learning
