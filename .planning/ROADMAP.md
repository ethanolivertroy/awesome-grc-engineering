# Roadmap: Awesome GRC Engineering

## Overview

This roadmap transforms 33 v1 requirements into the canonical reference for GRC engineering. Starting with foundation and automation (Phase 1), we build out core tool curation (Phase 2), expand to learning resources and frameworks (Phase 3), and finish with community building and launch preparation (Phase 4). Each phase delivers complete, verifiable capabilities that build toward becoming THE resource the GRC engineering community points to.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3, 4): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: Foundation & Infrastructure** - Repository setup with automation and compliance
- [ ] **Phase 2: Core Tools Curation** - Curated tool sections with opinionated commentary
- [ ] **Phase 3: Learning & Frameworks** - Educational resources and compliance framework guides
- [ ] **Phase 4: Community & Launch** - Community resources, quality validation, and public launch

## Phase Details

### Phase 1: Foundation & Infrastructure
**Goal**: Repository passes awesome-lint validation with automated quality gates and proper documentation structure
**Depends on**: Nothing (first phase)
**Requirements**: FOUND-01, FOUND-02, FOUND-03, FOUND-04, FOUND-05, FOUND-06, FOUND-07, FOUND-08, FOUND-09
**Success Criteria** (what must be TRUE):
  1. Repository passes awesome-lint validation without errors
  2. GitHub Actions automatically validate PRs for formatting and broken links
  3. Table of contents auto-generates from README structure via doctoc
  4. CONTRIBUTING.md clearly documents submission criteria aligned with GRC Engineering Manifesto
  5. Repository is properly configured with required files (LICENSE, CODE_OF_CONDUCT) and GitHub topics
**Plans**: 3 plans

Plans:
- [ ] 01-01-PLAN.md — Create core files (LICENSE, README skeleton, contributing.md, code-of-conduct.md)
- [ ] 01-02-PLAN.md — Create GitHub Actions workflows (awesome-lint, lychee, toc, dependabot, PR template)
- [ ] 01-03-PLAN.md — Validate and verify (run awesome-lint, generate TOC, configure GitHub topics)

### Phase 2: Core Tools Curation
**Goal**: Users can discover curated GRC engineering tools with opinionated commentary explaining why each matters
**Depends on**: Phase 1
**Requirements**: TOOL-01, TOOL-02, TOOL-03, TOOL-04, TOOL-05, TOOL-06
**Success Criteria** (what must be TRUE):
  1. README contains Policy-as-Code section with 5-10 tools (OPA, Kyverno, Sentinel, etc.)
  2. README contains Security scanners section with 5-10 tools (Prowler, Trivy, Checkov, etc.)
  3. README contains Open-source GRC platforms section with 3-5 tools
  4. README contains Evidence automation section with 5-8 tools (SBOM, audit logging)
  5. Every tool entry includes opinionated commentary on WHY it matters for GRC engineering
  6. Every tool entry has dual-audience tag (engineer-friendly, GRC-professional-friendly, or both)
**Plans**: TBD

Plans:
- [ ] 02-01: TBD (will be defined during phase planning)

### Phase 3: Learning & Frameworks
**Goal**: Users can find educational resources to bridge GRC-engineering gap and framework-specific automation guides
**Depends on**: Phase 2
**Requirements**: LEARN-01, LEARN-02, LEARN-03, LEARN-04, LEARN-05, FRAME-01, FRAME-02, FRAME-03, FRAME-04, FRAME-05
**Success Criteria** (what must be TRUE):
  1. README contains GRC Engineering fundamentals section linking to manifesto and philosophy resources
  2. README contains Books & courses section with audience labels (GRC→technical vs technical→GRC)
  3. README contains Blogs & newsletters section featuring key practitioner voices
  4. README contains Podcasts & videos section with conference talks and episodes
  5. README contains framework sections for SOC 2, NIST, FedRAMP, and ISO 27001 with engineering-focused resources
  6. Each learning resource has brief description of what users will learn
  7. Each framework section includes automation guides and implementation resources (not just policy)
**Plans**: TBD

Plans:
- [ ] 03-01: TBD (will be defined during phase planning)

### Phase 4: Community & Launch
**Goal**: Repository meets quality gates and is launched to GRC engineering community with community resource discovery
**Depends on**: Phase 3
**Requirements**: COMM-01, COMM-02, COMM-03, QUAL-01, QUAL-02, QUAL-03, QUAL-04, QUAL-05
**Success Criteria** (what must be TRUE):
  1. README contains Communities & forums section (Discord, Slack, forums)
  2. README contains Conferences & events section with GRC engineering relevance
  3. README contains Related awesome lists section linking complementary resources
  4. Repository contains minimum 50 curated resources total
  5. Repository contains maximum 100 resources (quality over quantity constraint met)
  6. All resources verified to align with GRC Engineering Manifesto principles
  7. All links verified working before launch
  8. No vendor-sponsored or marketing content included in curated list
**Plans**: TBD

Plans:
- [ ] 04-01: TBD (will be defined during phase planning)

## Progress

**Execution Order:**
Phases execute in numeric order: 1 → 2 → 3 → 4

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Foundation & Infrastructure | 0/3 | Planned | - |
| 2. Core Tools Curation | 0/TBD | Not started | - |
| 3. Learning & Frameworks | 0/TBD | Not started | - |
| 4. Community & Launch | 0/TBD | Not started | - |
