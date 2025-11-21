# **Enterprise CI/CD for Python Validation Libraries**

A production-grade, reproducible Python package template with automated CI/CD, quality gates, security scanning, and release automation suitable for ECU validation workflows.

---

## **Overview**

This repository provides a standardized structure and pipeline for building, testing, and releasing Python libraries used across validation and test-orchestration systems.

Key features:

* Reproducible builds from a locked environment 🔒
* Strict PR quality gates (format, lint, type-check, tests, security)
* Automated semantic releases with changelog generation 🏷️
* Artifact publishing to Artifactory/GitHub Packages
* Traceability via JIRA and build metadata

---

## **Repository Structure**

```
src/<package>/        # Library source code
tests/unit/           # Unit tests
tests/integration/    # Integration tests
docs/                 # Usage + API documentation
.github/workflows/    # CI/CD workflows
ADRs/                 # Architecture Decision Records
CONTRIBUTING.md       # Contribution guidelines
RUNBOOK.md            # Release and operations guide
pyproject.toml        # Build configuration
```

---

## **Development Workflow**

### **1. Before creating a PR**

* Run pre-commit hooks
* Ensure formatting, linting, and unit tests pass locally

### **2. PR Checks (mandatory)**

CI validates:

* black formatting
* ruff linting
* mypy type-checking
* pytest with coverage ≥ 80%
* bandit static security scan
* dependency vulnerability scan

All checks must pass before merge.

---

## **Release Workflow**

Triggered by pushing a version tag (e.g., `v1.2.0`).
Pipeline performs:

1. Build (wheel + sdist) inside hermetic container
2. Full test suite + smoke tests
3. Changelog generation
4. Publication to staging → promotion to production 🚀
5. GitHub Release creation and JIRA update

Artifacts are immutable once published.

---

## **Requirements**

* Python versions: see CI matrix
* Package manager: Poetry or setuptools (defined in ADR-001)
* Access to Artifactory or GitHub Packages

---

## **Getting Started**

1. Clone the repo
2. Install dependencies
3. Run tests
4. Use the package or extend modules as needed

Documentation for local development, releases, and decisions is available under:

* `CONTRIBUTING.md`
* `RUNBOOK.md`
* `ADRs/`

---

## **License** 

Project license to be defined by the organization.

---
