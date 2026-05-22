# 🚀 Advanced GitHub Actions Labs (Deep-Dive, Enterprise Level)

This document provides **highly advanced, production-grade labs** for mastering:

- Reusable Workflows
- Composite Actions
- Container-based Jobs
- GitHub Runners (hosted & self-hosted)
- Azure Integrations

Each lab contains:
- ✅ Concept
- ✅ Why it matters (real-world reasoning)
- ✅ Code walkthrough
- ✅ Improvements / extensions

---

# 🧪 LAB 1 — Enterprise Reusable Workflow Platform

## ✅ Concept
Reusable workflows using `workflow_call` allow central CI/CD logic to be shared.

## ✅ Why
- Eliminates duplication
- Enforces standardization
- Enables platform engineering models

## ✅ Code
```yaml
# .github/workflows/reusable-ci.yml
name: Reusable CI
on:
  workflow_call:
    inputs:
      runtime:
        required: true
        type: string

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Running with ${{ inputs.runtime }}"
```

## ✅ Use It
```yaml
jobs:
  ci:
    uses: org/platform/.github/workflows/reusable-ci.yml@main
    with:
      runtime: "node"
```

## ✅ Improvements
- Add matrix support
- Add secrets + OIDC auth
- Add artifact outputs

---

# 🧪 LAB 2 — Composite Actions as Internal Libraries

## ✅ Concept
Composite actions bundle steps into reusable logic blocks.

## ✅ Why
- Avoid repetition
- Simplify workflows
- Build internal action libraries

## ✅ Code
```yaml
# action.yml
name: Build Pipeline
runs:
  using: "composite"
  steps:
    - run: npm ci
      shell: bash
    - run: npm test
      shell: bash
```

## ✅ Usage
```yaml
- uses: ./.github/actions/build
```

## ✅ Improvements
- Add input parameters
- Add conditional execution
- Version the action

---

# 🧪 LAB 3 — Container-based Workflows

## ✅ Concept
Run jobs inside containers for reproducibility.

## ✅ Why
- Eliminates environment drift
- Portable CI/CD

## ✅ Code
```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: node:20
    steps:
      - run: node -v
```

## ✅ Improvements
- Use private container registry (Azure ACR)
- Add service containers (DB, Redis)

---

# 🧪 LAB 4 — Self-Hosted Runners on Azure

## ✅ Concept
Run workloads on your own machines.

## ✅ Why
- Custom compute (GPU, memory)
- Network isolation

## ✅ Setup
```bash
# Install runner
./config.sh
./run.sh
```

## ✅ Workflow
```yaml
runs-on: [self-hosted, linux]
```

## ✅ Improvements
- Auto-scale runners (VMSS)
- Ephemeral runners

---

# 🧪 LAB 5 — Hybrid Workflow (Hosted + Self-hosted)

## ✅ Concept
Mix runners per job.

## ✅ Why
- Optimize cost
- Use specialized hardware only when required

## ✅ Code
```yaml
jobs:
  light:
    runs-on: ubuntu-latest

  heavy:
    runs-on: [self-hosted, gpu]
```

## ✅ Improvements
- Dynamic runner selection
- Cost-based routing

---

# 🧪 LAB 6 — Container Build + Push (Azure ACR)

## ✅ Concept
Build container and push to registry.

## ✅ Code
```yaml
- uses: azure/login@v2
- uses: azure/docker-login@v2
- run: docker build -t myapp .
- run: docker push myapp
```

## ✅ Why
- Production delivery pipeline

## ✅ Improvements
- Multi-arch builds
- Build cache optimization

---

# 🧪 LAB 7 — Multi-Repo Orchestration

## ✅ Concept
Trigger workflows across repos.

## ✅ Code
```yaml
- uses: peter-evans/repository-dispatch@v3
```

## ✅ Why
- Microservices orchestration

## ✅ Improvements
- Event-driven architecture

---

# 🧪 LAB 8 — Dynamic Matrix Pipelines

## ✅ Concept
Dynamic job generation.

## ✅ Code
```yaml
strategy:
  matrix: ${{ fromJson(inputs.matrix) }}
```

## ✅ Why
- Scale builds dynamically

## ✅ Improvements
- Generate matrix via scripts

---

# 🧪 LAB 9 — Ephemeral Azure Runners

## ✅ Concept
Spin runners per job.

## ✅ Why
- Security
- Cost optimization

## ✅ Improvements
- Integrate Azure VMSS
- Cleanup automation

---

# 🧪 LAB 10 — Policy-as-Code

## ✅ Concept
Enforce rules automatically.

## ✅ Why
- Compliance

## ✅ Improvements
- Integrate OPA

---

# 🧪 LAB 11 — OIDC Authentication

## ✅ Concept
GitHub → Azure trust without secrets.

## ✅ Code
```yaml
- uses: azure/login@v2
```

## ✅ Why
- Secure pipelines

## ✅ Improvements
- Organization-wide rollout

---

# 🧪 LAB 12 — Capstone

## ✅ Build System
- Reusable workflows
- Composite actions
- Containers
- Azure deploy
- Self-hosted runners

## ✅ Goal
Simulate enterprise DevOps platform

---

# 💡 Tips
- Use logs for debugging
- Enable ACTIONS_RUNNER_DEBUG
- Track performance metrics

---

✅ End of Advanced Labs
