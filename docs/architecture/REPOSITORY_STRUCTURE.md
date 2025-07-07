# UAEngine Repository Structure

## Overview

UAEngine is organized into multiple repositories to properly separate open source components from proprietary trade secrets while maintaining ease of use.

## Repository Layout

```
GitHub (Public)
├── uaengine/
│   ├── uaengine/                 # Main open source framework
│   ├── uaengine-examples/        # Examples and tutorials
│   ├── uaengine-community/       # Community contributions
│   ├── uaengine-docs/            # Documentation site
│   └── uaengine-benchmarks/      # Performance benchmarks

Private Git Server
├── uaengine-internal/
│   ├── trade-secrets/            # Protected algorithms
│   ├── licensing/                # License management
│   ├── distribution/             # Build and packaging
│   ├── customer-portal/          # Customer management
│   └── analytics/                # Usage analytics
```

## Repository Details

### uaengine/uaengine (Public)

Main open source framework repository.

**Structure:**
```
uaengine/
├── src/
│   └── uaengine/
│       ├── __init__.py
│       ├── core/
│       │   ├── engine.py         # Main engine
│       │   ├── optimizer.py      # Base optimizer classes
│       │   ├── metrics.py        # Metrics collection
│       │   └── safety.py         # Rollback mechanisms
│       ├── optimizers/
│       │   ├── database/         # Open source DB optimizers
│       │   ├── cache/            # Basic cache strategies
│       │   ├── api/              # API optimization
│       │   └── container/        # Container orchestration
│       ├── integrations/
│       │   ├── aws/              # AWS integration
│       │   ├── azure/            # Azure integration
│       │   ├── gcp/              # GCP integration
│       │   └── kubernetes/       # K8s integration
│       └── utils/
│           ├── benchmarking.py   # Performance testing
│           └── validation.py     # Result validation
├── tests/
├── docs/
├── examples/
├── LICENSE                       # MIT License
├── README.md
├── setup.py
└── pyproject.toml
```

**Key Files:**
- No trade secrets
- All algorithms are basic/standard implementations
- Full test coverage
- Comprehensive documentation

### uaengine-internal/trade-secrets (Private)

Protected algorithm repository.

**Structure:**
```
trade-secrets/
├── algorithms/
│   ├── heat_scoring.py
│   ├── query_prediction.py
│   ├── cache_optimization.py
│   ├── quantum_optimization.py
│   ├── database_indexing.py
│   ├── api_rate_limiting.py
│   ├── container_orchestration.py
│   └── ai_model_compression.py
├── protection/
│   ├── encryption.py
│   ├── obfuscation.py
│   └── anti_tampering.py
├── keys/
│   └── .gitignore               # Never commit keys
├── build/
│   ├── package_algorithms.py
│   └── generate_stubs.py
└── README.md                    # Internal only
```

**Security:**
- Encrypted at rest
- Access logged
- Two-factor authentication required
- Signed commits only

### uaengine-internal/licensing (Private)

License management system.

**Structure:**
```
licensing/
├── server/
│   ├── api/
│   │   ├── validation.py
│   │   ├── activation.py
│   │   └── telemetry.py
│   ├── models/
│   │   ├── license.py
│   │   ├── customer.py
│   │   └── usage.py
│   └── utils/
│       ├── key_generation.py
│       └── hardware_id.py
├── client/
│   ├── validator.py
│   └── offline_token.py
├── portal/
│   ├── frontend/
│   └── backend/
└── deployment/
    ├── docker/
    └── kubernetes/
```

### uaengine-internal/distribution (Private)

Build and distribution automation.

**Structure:**
```
distribution/
├── builders/
│   ├── open_source.py         # Build OS package
│   ├── licensed.py            # Build licensed packages
│   ├── enterprise.py          # Build enterprise packages
│   └── cloud.py               # Build cloud client
├── publishers/
│   ├── pypi.py               # PyPI publishing
│   ├── private_pypi.py       # Private index
│   └── direct.py             # Direct distribution
├── security/
│   ├── signing.py            # Code signing
│   └── verification.py       # Package verification
└── automation/
    ├── release.yml           # GitHub Actions
    └── jenkins/              # Jenkins pipelines
```

## File Migration Map

### Files to Keep in Open Source Repo

```
Current Location → Target Location
────────────────────────────────────
src/core/engine.py → uaengine/src/uaengine/core/engine.py
src/core/metrics.py → uaengine/src/uaengine/core/metrics.py
src/optimizers/database/query_optimizer.py → uaengine/src/uaengine/optimizers/database/query_optimizer.py
src/integrations/* → uaengine/src/uaengine/integrations/*
tests/* → uaengine/tests/*
docs/* → uaengine/docs/*
```

### Files to Move to Private Repo

```
Current Location → Target Location
────────────────────────────────────
src/core/security/trade_secrets.py → trade-secrets/protection/trade_secrets.py
src/core/security/local_protection.py → licensing/client/local_protection.py
src/core/security/ip_audit.py → trade-secrets/audit/ip_audit.py
TRADE_SECRETS_REGISTRY.md → trade-secrets/REGISTRY.md
```

### Files to Create Stubs For

```
Trade Secret → Open Source Stub
────────────────────────────────
heat_scoring → src/uaengine/algorithms/stubs.py::HeatScoringStub
query_prediction → src/uaengine/algorithms/stubs.py::QueryPredictionStub
[... all 8 algorithms ...]
```

## Installation Methods

### 1. Basic Open Source
```bash
pip install uaengine
```

### 2. Licensed Version
```bash
# Set credentials
export UAENGINE_LICENSE_KEY="your-key"

# Install from private index
pip install uaengine-pro \
  --index-url https://pypi.uaengine.com/simple/ \
  --extra-index-url https://pypi.org/simple/
```

### 3. Enterprise Version
```bash
# Download from portal with auth token
curl -H "Authorization: Bearer $TOKEN" \
  https://portal.uaengine.com/download/enterprise \
  -o uaengine-enterprise.whl

# Install with verification
pip install --verify-signature uaengine-enterprise.whl
```

### 4. Docker Images
```bash
# Open source
docker pull uaengine/uaengine:latest

# Licensed (requires auth)
docker login registry.uaengine.com
docker pull registry.uaengine.com/uaengine-pro:latest
```

## Development Workflow

### For Open Source Contributors

1. Fork `uaengine/uaengine`
2. Create feature branch
3. Make changes (no trade secrets!)
4. Submit PR
5. Pass CI/CD checks
6. Get reviewed and merged

### For Internal Development

1. Clone private repos
2. Create feature branch
3. Implement changes
4. Update both algorithm and stub
5. Test all distribution types
6. Security review required
7. Deploy to all channels

## Security Considerations

### Public Repos
- No credentials
- No internal URLs
- No trade secret references
- Public CI/CD only

### Private Repos
- MFA required
- Signed commits
- Encrypted storage
- Access logging
- Regular audits

## Release Process

### 1. Version Bump
- Update version in all repos
- Update compatibility matrix
- Update changelog

### 2. Build All Packages
```bash
# In distribution repo
python -m builders.all --version 1.2.0
```

### 3. Test All Packages
```bash
# Automated testing
python -m testers.integration --all-packages
```

### 4. Release
```bash
# Release to all channels
python -m publishers.release --version 1.2.0 --channels all
```

### 5. Announce
- GitHub release notes
- Blog post
- Email customers
- Update docs

