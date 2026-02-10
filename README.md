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
