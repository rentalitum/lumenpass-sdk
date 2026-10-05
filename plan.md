# LumenPass SDK — Wave Program Execution Plan

## 1. Executive Summary

The **Wave Program** is an open-source development and community acceleration framework designed to scale contributions across the LumenPass SDK ecosystem. Operating on cyclical sprints, maintainers formulate tightly scoped, independent issues that contributors pick up, implement, and validate. This plan defines the operational lifecycle, governance standards, contributor workflows, and strategic roadmap milestones for upcoming waves.

---

## 2. Operating Model

The core architecture of the Wave Program is driven by asynchronous, parallel execution:

```
[Maintainer Scoping] ➔ [Issue Publication] ➔ [Contributor Claiming] ➔ [CI Validation] ➔ [Review & Merge]
```

### 2.1 Role Responsibilities

- **Maintainers**: Curate sprint backlogs, define issue specifications, verify cryptographic and architectural invariants, conduct peer reviews, and orchestrate releases.
- **Contributors**: Claim scoped issues, implement solutions within defined boundaries, provide automated test suites, and adhere to documentation and typing standards.

---

## 3. Sprint Cycle Lifecycle

Each Wave consists of structured 2-to-3 week sprint cycles divided into five distinct phases:

### Phase 1: Issue Curation & Scoping (Pre-Sprint)
Maintainers author issues following the **Standard Issue Specification**:
1. **Problem Statement**: Precise operational context and target behavior.
2. **Implementation Boundaries**: Explicit package targets (`@lumenpass/core` vs. `@lumenpass/sdk`) and allowed file modifications.
3. **Acceptance Criteria**: Verifiable functional expectations and edge cases.
4. **Independence Requirement**: Guaranteed zero dependency on concurrent unmerged PRs.
5. **Labels**: Categorized by scope (`wave:core`, `wave:sdk`, `stellar`, `good-first-issue`).

### Phase 2: Assignment & Claiming
- Issues are claimed via GitHub comments and formally assigned by maintainers.
- Contributor concurrency limit: maximum **1 active issue per contributor** to guarantee delivery velocity and open access.
- Inactive claim timeout: issues unclaimed after 72 hours of inactivity are automatically unassigned and recycled.

### Phase 3: Development & Quality Gates
Contributors develop in dedicated feature branches on their forks and validate locally:
- **Type Safety**: Zero compiler warnings or errors (`pnpm typecheck`).
- **Build Verification**: Clean ESM and `.d.ts` compilation (`pnpm build`).
- **Deterministic Testing**: 100% test pass rate with regression coverage (`pnpm test`).
- **Architectural Rules**: Zero EVM dependencies, Stellar/Soroban-first primitives, and mandatory secret redaction.

### Phase 4: Review, CI & Merge
- Pull requests trigger automated validation matrices via GitHub Actions.
- Maintainers review code for contract integrity, performance, and documentation parity.
- Approved pull requests are merged through fast-forward or automated squashes.

### Phase 5: Release & Retrospective
- Automated changelog generation and semantic versioning (`@lumenpass/core`, `@lumenpass/sdk`).
- Contributor attribution, metric evaluation (throughput, review latency), and backlog grooming for the next wave.

---

## 4. Strategic Wave Roadmap

### Wave 1: Core Foundation & Hardening
- **Objective**: Solidify transport layer, error hierarchies, and account validation.
- **Key Deliverables**:
  - Soroban contract invocations and transaction builders.
  - Enhanced cache policies and in-flight request deduplication.
  - Complete test parity across Node.js 20, 22, and 24.

### Wave 2: Community & Guild Management
- **Objective**: Expand high-level client resources and access enforcement.
- **Key Deliverables**:
  - Full Guilds CRUD resource and cursor pagination generators.
  - Multi-tier access policy engine supporting on-chain credential checks.
  - End-to-end integration test harness for Stellar testnet and standalone nodes.

### Wave 3: Ecosystem Tooling & Developer Experience
- **Objective**: Accelerate third-party dApp integration and developer onboarding.
- **Key Deliverables**:
  - React and Svelte hooks for seamless wallet/client instantiation.
  - Interactive CLI utility for configuration diagnostics and pass inspection.
  - Comprehensive cookbook with runnable Soroban contract examples.

---

## 5. Governance & Code Standards

1. **Non-Breaking Contracts**: Public APIs must maintain backward compatibility once stabilized. Deprecations require scheduled migration paths and alias retention.
2. **Deterministic Behavior**: All parsing, sanitization, and encoding routines must produce reproducible results without platform leaks.
3. **Security Invariants**: API keys, Stellar private seeds, and bearer tokens must never be logged, transmitted, or leaked into git history.
