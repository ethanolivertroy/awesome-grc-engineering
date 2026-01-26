# Awesome List Stack & Tooling Research

**Research Date:** 2026-01-26
**Project:** Awesome GRC Engineering
**Goal:** Identify the canonical tools, automation, and conventions to build THE reference for GRC engineering community

---

## Executive Summary

Creating a successful awesome list requires strict adherence to [sindresorhus/awesome](https://github.com/sindresorhus/awesome) conventions, automated quality checks, and ongoing maintenance. This stack focuses on three pillars:

1. **Compliance** - Meet official awesome list requirements
2. **Automation** - CI/CD for continuous quality
3. **Maintainability** - Tools to reduce manual overhead

**Critical Success Factor:** Quality over quantity. Awesome lists are curated, not collected.

---

## 1. Core Conventions & Requirements

### 1.1 Official Guidelines
**Source:** [sindresorhus/awesome](https://github.com/sindresorhus/awesome)

#### Repository Requirements
- **Repository age:** Minimum 30 days from first real commit or open-source date
- **Default branch:** Must be named `main` (not `master`)
- **GitHub topics:** Must include both `awesome-list` and `awesome` topics
- **License:** CC0-1.0 recommended (Creative Commons, public domain)

#### Naming Conventions
- **Repo name:** Lowercase slug format - `awesome-grc-engineering`
- **Title:** Title case format - `# Awesome GRC Engineering`
- **Consistent terminology:** Use correct naming (e.g., "Node.js" not "NodeJS" or "node.js")

#### Content Structure
- **Succinct description** at the top (e.g., "Curated resources for GRC engineering practices and tooling")
- **Awesome badge** immediately after main heading
- **Table of Contents** section (labeled "Contents")
- **Contribution guidelines** in `contributing.md`
- **No hard-wrapping** in markdown
- **No CI badges** in readme
- **Footnotes section** for non-critical content

#### Formatting Rules
**Critical:** Consistent formatting = credibility

- **List item format:** `- [Title](url) - Description starts with uppercase and ends with period.`
- **Separator:** Dash between link and description
- **Capitalization:** Description starts with uppercase
- **Punctuation:** Description ends with period
- **Descriptions optional** only if title is self-explanatory
- **Entry placement:** Add new items to bottom of relevant category
- **URLs:** Should end with `#readme` for GitHub repos

**Rationale:** These rules ensure readability and consistency across all awesome lists. They're enforced by `awesome-lint`.

### 1.2 Submission Requirements (for main awesome list)
When ready to submit your list to the main awesome repository:

- **Review 2+ PRs:** Provide substantive feedback (not just "looks good")
- **Wait 30 days:** Let your list mature before submission
- **PR title format:** "Add Name of List" (exclude "Awesome")
- **Verification:** Comment "unicorn" to prove you read all guidelines

**Rationale:** These barriers ensure only quality, maintained lists get included.

---

## 2. Linting & Validation

### 2.1 awesome-lint (REQUIRED)
**Tool:** [sindresorhus/awesome-lint](https://github.com/sindresorhus/awesome-lint)
**Version:** v2.2.2 (October 2025)
**Language:** Node.js
**License:** MIT

#### Why Use It
Official linter for awesome lists. Enforces all conventions automatically. Non-negotiable requirement for inclusion in main awesome repository.

#### Installation
```bash
npx awesome-lint
```

No installation needed - use via npx for always-latest version.

#### What It Checks
- **General Markdown rules:** List markers, indentation, formatting
- **Awesome-specific rules:**
  - Awesome badge presence and placement
  - List item format (link - description)
  - Trailing slashes in URLs
  - GitHub topics configuration
  - Repository age (30 days minimum)
  - Default branch name (`main`)

#### Common Violations & Fixes

| Violation | Error | Fix |
|-----------|-------|-----|
| `awesome-badge` | Missing Awesome badge | Add `[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)` after title |
| `awesome-list-item` | Description formatting | Format as: `[Title](url) - Description.` |
| `unordered-list-marker-style` | Wrong marker | Use `-` for all list items |
| `trailing-slash` | URLs end with `/` | Remove trailing slashes |
| `awesome-git-repo-age` | Repo too new | Wait 30 days before submission |
| `awesome-github` | Missing topics | Add `awesome-list` and `awesome` topics to repo |

#### Rule Control
Use HTML comments to control linting:

```markdown
<!-- lint disable rule-name -->
Content to skip
<!-- lint enable rule-name -->

<!-- lint ignore rule-name -->
Single node exception
```

**Use sparingly.** Disabling rules usually indicates non-compliance.

#### CI/CD Integration
See Section 4.2 for GitHub Actions workflow.

**What NOT to Use:**
- Generic Markdown linters (markdownlint, remark-lint) - awesome-lint already includes markdown rules
- Custom validation scripts - awesome-lint is the standard

---

## 3. Automation Tools

### 3.1 Table of Contents Generation

#### doctoc (RECOMMENDED)
**Tool:** [thlorenz/doctoc](https://github.com/thlorenz/doctoc)
**Language:** Node.js
**Stars:** 4.2k+

##### Why doctoc
- **Auto-updates:** Maintains TOC between marker comments
- **Platform compatibility:** GitHub, GitLab, Bitbucket, Ghost
- **Flexible placement:** Insert anywhere via markers
- **Pre-commit integration:** Auto-update TOC before commits
- **Dry-run mode:** CI verification without file changes

##### Installation
```bash
npm install -g doctoc
```

##### Basic Usage
```bash
# Generate TOC for readme
doctoc README.md

# Batch update all markdown files
doctoc .

# Dry run for CI
doctoc . --dryrun
```

##### Configuration Options
```bash
# Custom title
doctoc README.md --title "**Table of Contents**"

# Remove title
doctoc README.md --notitle

# Control heading levels
doctoc README.md --minlevel 2 --maxlevel 4

# Update existing TOCs only
doctoc README.md --update-only
```

##### TOC Placement
Insert these markers where you want the TOC:

```markdown
<!-- START doctoc -->
<!-- END doctoc -->
```

doctoc automatically updates content between markers.

##### Pre-commit Hook
Add to `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/thlorenz/doctoc
    rev: v2.2.0
    hooks:
      - id: doctoc
```

##### CI Integration
```yaml
# Verify TOC is up-to-date
- name: Check TOC
  run: |
    npm install -g doctoc
    doctoc . --dryrun
```

Returns exit code 1 if updates needed.

**Alternatives Considered:**
- **markdown-toc (jonschlinkert):** More stars (4.7k), but doctoc has better CI integration
- **md-toc (Python):** Different language adds dependency complexity
- **Manual TOC:** Maintenance burden, prone to staleness

**Rationale:** doctoc is the de facto standard for awesome lists. The marker-based approach prevents TOC drift.

### 3.2 Link Checking

#### lychee (REQUIRED)
**Tool:** [lycheeverse/lychee](https://github.com/lycheeverse/lychee)
**GitHub Action:** [lycheeverse/lychee-action](https://github.com/lycheeverse/lychee-action)
**Version:** v2.7.0 (October 2025)
**Language:** Rust
**Stars:** 2.1k+

##### Why lychee
- **Fast:** Written in Rust, async/stream-based
- **Comprehensive:** Checks Markdown, HTML, reStructuredText, text files
- **Rate limit handling:** Built-in caching prevents GitHub/API rate limits
- **Format support:** Markdown, JSON, CSV output
- **Active maintenance:** Regular updates, latest 2025

##### Features
- Email address validation
- Local file checking
- Retry logic for transient failures
- Custom headers (for authenticated APIs)
- Exclude patterns via `.lycheeignore`
- Cache support (mitigates rate limiting)

##### GitHub Actions Workflow
See Section 4.3 for complete configuration.

##### Caching Setup
Critical for avoiding rate limits:

```yaml
- name: Restore lychee cache
  uses: actions/cache@v4
  with:
    path: .lycheecache
    key: cache-lychee-${{ github.sha }}
    restore-keys: cache-lychee-

- name: Run lychee
  uses: lycheeverse/lychee-action@v2
  with:
    args: "--cache --max-cache-age 1d ."
```

##### Link Exclusion
Create `.lycheeignore` with regex patterns:

```
# Exclude localhost
http://localhost
http://127\.0\.0\.1

# Exclude URLs requiring authentication
https://private\.example\.com/.*

# Exclude rate-limited APIs
https://api\.github\.com/.*
```

##### Performance
Representative scan: 576 links in ~1 minute

**Alternatives Considered:**
- **awesome-bot:** Older, Ruby-based, less maintained
- **broken-link-checker:** Slower, Node.js
- **linkchecker:** Python, more features but complexity
- **markdown-link-check:** Node.js, popular but slower

**Rationale:** lychee is the fastest, most reliable, and actively maintained. Rust performance + caching = best choice for large lists.

**What NOT to Use:**
- Manual link checking - doesn't scale
- Browser extensions - can't be automated
- Online services - external dependencies, rate limits

---

## 4. CI/CD Automation

### 4.1 GitHub Actions (REQUIRED)
**Platform:** GitHub Actions
**Cost:** Free for public repositories

#### Why GitHub Actions
- **Native integration:** Works seamlessly with GitHub repos
- **Free for public repos:** No cost for awesome lists
- **Awesome list standard:** Most awesome lists use GHA
- **Rich ecosystem:** Pre-built actions for common tasks

### 4.2 awesome-lint Workflow

**File:** `.github/workflows/awesome-lint.yml`

```yaml
name: Awesome Lint

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

jobs:
  awesome-lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5
        with:
          fetch-depth: 0  # Required for repo age validation

      - name: Run awesome-lint
        run: npx awesome-lint
```

**Key Configuration:**
- `fetch-depth: 0` - Enables repository age validation
- Runs on PR and push - Catches issues early
- No caching needed - npx always uses latest version

### 4.3 Link Checking Workflow

**File:** `.github/workflows/link-check.yml`

```yaml
name: Link Check

on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly on Sunday
  pull_request:
    branches: [main]
  workflow_dispatch:  # Manual trigger

jobs:
  linkChecker:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5

      - name: Restore lychee cache
        uses: actions/cache@v4
        with:
          path: .lycheecache
          key: cache-lychee-${{ github.sha }}
          restore-keys: cache-lychee-

      - name: Link Checker
        uses: lycheeverse/lychee-action@v2
        with:
          args: '--cache --max-cache-age 1d --verbose --no-progress .'
          fail: true  # Fail on broken links
          jobSummary: true  # GitHub job summary

      - name: Create Issue From File
        if: failure()
        uses: peter-evans/create-issue-from-file@v5
        with:
          title: 'Broken Links Detected'
          content-filepath: ./lychee/out.md
          labels: |
            automated
            broken-links
```

**Key Features:**
- **Scheduled checks:** Weekly verification prevents link rot
- **PR checks:** Validates new links before merge
- **Manual trigger:** On-demand via workflow_dispatch
- **Caching:** Prevents rate limiting
- **Auto-issue creation:** Broken links create GitHub issues
- **Job summary:** Results visible in Actions UI

**Configuration Options:**
- `fail: true` - Fail workflow on broken links (recommended for PRs)
- `fail: false` - Don't fail (recommended for scheduled runs)
- `jobSummary: true` - Write results to GitHub job summary

### 4.4 TOC Update Workflow

**File:** `.github/workflows/toc.yml`

```yaml
name: TOC Generator

on:
  push:
    branches: [main]
    paths:
      - 'README.md'

jobs:
  generateTOC:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Generate TOC
        run: |
          npm install -g doctoc
          doctoc README.md

      - name: Commit TOC
        uses: stefanzweifel/git-auto-commit-action@v5
        with:
          commit_message: 'docs: update table of contents'
          file_pattern: 'README.md'
```

**Alternative Approach:** Use pre-commit hooks instead to update TOC locally before push.

### 4.5 Dependabot Configuration

**File:** `.github/dependabot.yml`

```yaml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: ".github/workflows"
    schedule:
      interval: "weekly"
    labels:
      - "dependencies"
      - "github-actions"
```

**Rationale:** Keeps GitHub Actions up-to-date automatically. Critical for security.

---

## 5. Badge Standards

### 5.1 Required Badge
**Awesome Badge (REQUIRED)**

```markdown
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
```

Must appear immediately after the main heading.

**Source:** [awesome.re](https://awesome.re)

### 5.2 Optional Badges

#### Shields.io
**Service:** [shields.io](https://shields.io/)
**Repository:** [badges/shields](https://github.com/badges/shields)

Common optional badges for awesome lists:

```markdown
<!-- License -->
![License](https://img.shields.io/github/license/username/awesome-grc-engineering)

<!-- Link Check Status -->
![Link Check](https://github.com/username/awesome-grc-engineering/workflows/Link%20Check/badge.svg)

<!-- Contributors -->
![Contributors](https://img.shields.io/github/contributors/username/awesome-grc-engineering)

<!-- Last Commit -->
![Last Commit](https://img.shields.io/github/last-commit/username/awesome-grc-engineering)
```

**Badge Styles:**
- Default: `?style=flat`
- Flat square: `?style=flat-square`
- For the badge: `?style=for-the-badge` (larger, boxy design)
- Plastic: `?style=plastic`

**Recommended:** Use `?style=flat` or `?style=flat-square` for consistency with other awesome lists.

**What NOT to Include:**
- ❌ CI badges (explicitly forbidden by awesome list guidelines)
- ❌ Download/install counts (not relevant for lists)
- ❌ Social media badges (unprofessional)
- ❌ Personal badges (focus on content quality)

**Rationale:** Awesome badge is non-negotiable. Additional badges should add value without clutter. Less is more.

**Resources:**
- [badges/awesome-badges](https://github.com/badges/awesome-badges) - Curated badge collection
- [Simple Badges](https://badges.pages.dev/) - 3364+ badge options

---

## 6. Contribution Guidelines

### 6.1 CONTRIBUTING.md (REQUIRED)

**Requirement:** Must have a file named `contributing.md` in repo root.

#### Template Structure

Based on [sindresorhus/awesome contributing guidelines](https://github.com/sindresorhus/awesome/blob/main/contributing.md):

```markdown
# Contribution Guidelines

Please note that this project is released with a [Contributor Code of Conduct](code-of-conduct.md). By participating in this project you agree to abide by its terms.

---

## Adding to this list

Please ensure your pull request adheres to the following guidelines:

- Search previous suggestions before making a new one, as yours may be a duplicate.
- Make an individual pull request for each suggestion.
- Use title-casing for the section headers.
- Use the following format: `[Title](link) - Description.`
- Link additions should be added to the bottom of the relevant category.
- New categories or improvements to the existing categorization are welcome.
- Check your spelling and grammar.
- Make sure your text editor is set to remove trailing whitespace.
- The pull request and commit should have a useful title.
- The body of your commit message should contain a link to the repository.

Thank you for your suggestions!

## Updating your PR

A lot of times, making a PR adhere to the standards above can be difficult.
If the maintainers notice anything that we'd like changed, we'll ask you to
edit your PR before we merge it. There's no need to open a new PR, just edit
the existing one. If you're not sure how to do that,
[here is a guide](https://github.com/RichardLitt/knowledge/blob/master/github/amending-a-commit-guide.md)
on the different ways you can update your PR so that we can merge it.
```

#### Additional Sections for GRC Context

```markdown
## Quality Standards

For GRC tools and resources, please ensure:

- **Actively maintained:** Last commit within 6 months (unless mature/stable)
- **Documentation:** Clear README with setup instructions
- **Relevance:** Direct application to GRC engineering (not just compliance)
- **Production-ready:** Battle-tested in real GRC workflows (note maturity level)

## What qualifies as GRC Engineering?

This list focuses on *engineering* approaches to GRC:
- Automation and tooling
- Infrastructure as Code (IaC) for compliance
- Policy as Code
- Continuous compliance
- GRC APIs and integrations
- Security automation frameworks

*Not* included:
- General compliance consultancies
- GRC theory without implementation
- Enterprise vendors without engineering focus
- Paid-only solutions (unless exceptional)
```

### 6.2 Code of Conduct

**File:** `code-of-conduct.md`

**Template:** [Contributor Covenant](https://www.contributor-covenant.org/)

```markdown
# Contributor Covenant Code of Conduct

## Our Pledge
[Standard Contributor Covenant text]
```

Most awesome lists use the Contributor Covenant. Don't reinvent the wheel.

### 6.3 Pull Request Template

**File:** `.github/pull_request_template.md`

```markdown
## Proposed changes

Describe the changes in this PR.

## Types of changes

- [ ] Add new resource
- [ ] Remove resource
- [ ] Update existing resource
- [ ] Fix typo/grammar
- [ ] Improve structure/organization

## Checklist

- [ ] I have read the [contribution guidelines](contributing.md)
- [ ] The resource is awesome (high quality)
- [ ] The resource is actively maintained
- [ ] The description follows the format: `[Title](url) - Description.`
- [ ] The PR title follows the format: `Add Resource Name` or `Update Resource Name`
- [ ] I have checked for duplicate suggestions
```

**Rationale:** Template ensures contributors provide necessary information and follow standards.

**Resources:**
- [sindresorhus/awesome PR template](https://github.com/sindresorhus/awesome/blob/main/pull_request_template.md) - Official template
- [nayafia/contributing-template](https://github.com/nayafia/contributing-template) - Based on 40 FOSS projects
- [briandk's template](https://gist.github.com/briandk/3d2e8b3ec8daf5a27a62) - Adapted from Facebook

---

## 7. Documentation Standards

### 7.1 README Structure

Based on analysis of top awesome lists:

```markdown
# Awesome GRC Engineering [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated resources for GRC engineering: automation, policy as code, and continuous compliance

[Optional: Brief description expanding on tagline]

<!-- START doctoc -->
<!-- END doctoc -->

## Contents

- [Section 1](#section-1)
- [Section 2](#section-2)

## Section 1

- [Resource Name](url) - Description starting with uppercase and ending with period.

## Section 2

...

## Contributing

See [contributing.md](contributing.md).

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
```

### 7.2 Markdown Best Practices

#### List Formatting
```markdown
<!-- Good -->
- [Title](url) - Description starts uppercase and ends with period.

<!-- Bad -->
- [title](url) - description doesn't follow rules
* [Title](url) Description missing dash
- [Title](url)- Description missing space after dash
```

#### Indentation
- Use **2 spaces** for nested list items
- Use **4 spaces** for code blocks within lists

#### Line Length
- **No hard-wrapping** - Let editors handle wrapping
- Exception: Code blocks maintain original formatting

#### Headings
```markdown
# Main Title (H1) - Only one per document
## Major Section (H2)
### Subsection (H3)
```

### 7.3 Category Organization

For GRC Engineering context:

```markdown
## Contents

- [Awesome GRC Engineering](#awesome-grc-engineering)
  - [Contents](#contents)
  - [Governance](#governance)
  - [Risk Management](#risk-management)
  - [Compliance](#compliance)
  - [Policy as Code](#policy-as-code)
  - [Continuous Compliance](#continuous-compliance)
  - [Security Automation](#security-automation)
  - [Frameworks](#frameworks)
  - [Learning Resources](#learning-resources)
  - [Contributing](#contributing)

## Governance
Tools and frameworks for governance automation...

## Risk Management
Risk assessment and management automation...
```

**Principles:**
- Alphabetize sections within each category
- Group related items together
- Use flat hierarchy when possible (avoid deep nesting)
- Create new categories when section has 8+ items

---

## 8. Complete Setup Checklist

Use this checklist to ensure full compliance:

### Repository Setup
- [ ] Repository name: `awesome-grc-engineering`
- [ ] Default branch: `main`
- [ ] GitHub topics: `awesome-list`, `awesome`, `grc`, `compliance`, `governance`
- [ ] License: CC0-1.0
- [ ] Repository description: "Curated resources for GRC engineering"

### Files
- [ ] `README.md` with proper structure
- [ ] `contributing.md` with guidelines
- [ ] `code-of-conduct.md` (Contributor Covenant)
- [ ] `LICENSE` file (CC0)
- [ ] `.gitignore` (standard for Node.js projects)
- [ ] `.lycheeignore` (link exclusions)

### README Content
- [ ] Awesome badge after main heading
- [ ] Succinct description
- [ ] Table of contents (with doctoc markers)
- [ ] Well-organized sections
- [ ] All items follow format: `[Title](url) - Description.`
- [ ] Descriptions start uppercase, end with period
- [ ] Links end with `#readme` for GitHub repos
- [ ] Contributing section links to contributing.md
- [ ] License badge and section at bottom

### GitHub Actions
- [ ] `.github/workflows/awesome-lint.yml`
- [ ] `.github/workflows/link-check.yml`
- [ ] `.github/workflows/toc.yml` (optional if using pre-commit)
- [ ] `.github/dependabot.yml`
- [ ] `.github/pull_request_template.md`

### Pre-Commit Hooks (Optional)
- [ ] `.pre-commit-config.yaml` with doctoc

### Validation
- [ ] Run `npx awesome-lint` - passes with no errors
- [ ] Run `doctoc README.md` - TOC is up-to-date
- [ ] GitHub Actions all passing
- [ ] Repository at least 30 days old
- [ ] All links working (no 404s)

---

## 9. Maintenance Workflow

### Daily/Weekly Tasks
- **Monitor CI:** Check GitHub Actions for failures
- **Review PRs:** Evaluate contributions promptly
- **Triage issues:** Address broken links, suggestions

### Monthly Tasks
- **Link health:** Review link check results
- **Content audit:** Remove unmaintained/deprecated items
- **Category review:** Reorganize if sections grow large
- **Documentation:** Update contributing guidelines if patterns emerge

### Quarterly Tasks
- **Dependency updates:** Review Dependabot PRs
- **Tooling review:** Check for new/better automation tools
- **Community engagement:** Post updates to GRC communities

### Continuous
- **Quality over quantity:** Resist urge to add everything
- **Stay opinionated:** This is a *curated* list
- **Engage contributors:** Provide helpful feedback on PRs

---

## 10. Anti-Patterns (What NOT to Do)

### Content Anti-Patterns
- ❌ **Adding everything:** Curate ruthlessly
- ❌ **Including unmaintained projects:** Check last commit date
- ❌ **Self-promotion without quality:** Avoid conflict of interest
- ❌ **Blockchain/crypto items:** Explicitly forbidden by awesome guidelines
- ❌ **Paid-only solutions:** FOSS preferred (note exceptions)
- ❌ **Marketing content:** Focus on engineering value
- ❌ **Dead links:** Verify before adding

### Technical Anti-Patterns
- ❌ **Manual TOC maintenance:** Automate with doctoc
- ❌ **Skipping awesome-lint:** Required for compliance
- ❌ **No link checking:** Links rot quickly
- ❌ **Custom validation:** awesome-lint is standard
- ❌ **CI badges in readme:** Explicitly forbidden
- ❌ **Hard-wrapped markdown:** Let editors handle wrapping

### Process Anti-Patterns
- ❌ **Submitting too early:** Wait 30 days minimum
- ❌ **Ignoring PR feedback:** Address maintainer comments
- ❌ **Poor PR descriptions:** Explain what and why
- ❌ **Batch adding without review:** Quality check each item
- ❌ **Defensive about rejections:** Maintainer judgment is final

---

## 11. Success Metrics

How to know if your awesome list is succeeding:

### Quantitative
- **Stars:** Community interest indicator
- **Forks:** Active users and contributors
- **Contributors:** Diverse maintainer base
- **PR activity:** Regular community additions
- **Link health:** >95% links working

### Qualitative
- **Cited in documentation:** Other projects reference your list
- **Community discussion:** Mentioned in GRC communities
- **Quality over quantity:** 50 great items > 500 mediocre ones
- **Maintained structure:** Categories remain organized
- **Active discussion:** Issues/PRs have thoughtful conversation

### Leading Indicators
- **First month:** 10-20 quality resources
- **First quarter:** 50+ resources, 5+ contributors
- **First year:** 100+ resources, included in sindresorhus/awesome

---

## 12. Recommended Tech Stack Summary

### Essential Tools
| Category | Tool | Version | Rationale |
|----------|------|---------|-----------|
| Linting | awesome-lint | v2.2.2+ | Official, required standard |
| Link checking | lychee | v2.7.0+ | Fast, reliable, Rust-based |
| TOC generation | doctoc | v2.2.0+ | Auto-update, marker-based |
| CI/CD | GitHub Actions | N/A | Free, native, standard |
| Badges | Shields.io | N/A | Most comprehensive |

### Optional Tools
| Category | Tool | Use Case |
|----------|------|----------|
| Pre-commit | pre-commit | Local validation before push |
| Issue automation | peter-evans/create-issue-from-file | Auto-create issues from link failures |
| Auto-commit | stefanzweifel/git-auto-commit-action | Auto-commit TOC updates |

### Dependencies
- **Node.js:** 20+ (for awesome-lint, doctoc)
- **Git:** Any recent version
- **GitHub account:** Required for hosting

---

## 13. Migration Path (If Starting Fresh)

If creating from scratch:

### Week 1: Foundation
1. Create repository with proper naming
2. Add LICENSE (CC0)
3. Create basic README structure
4. Add awesome badge
5. Configure GitHub topics
6. Create contributing.md
7. Add code-of-conduct.md

### Week 2: Content
8. Add initial 20-30 high-quality resources
9. Organize into logical categories
10. Write descriptions following format
11. Add TOC with doctoc

### Week 3: Automation
12. Set up awesome-lint workflow
13. Configure lychee link checking
14. Add Dependabot
15. Create PR template
16. Test all workflows

### Week 4: Polish
17. Fix all awesome-lint errors
18. Verify all links work
19. Refine categories
20. Document maintenance process

### Week 5-12: Maturation
21. Add 2-5 resources weekly
22. Engage with community
23. Accept quality PRs
24. Monitor CI health

### Month 4: Submission
25. Review guidelines one final time
26. Run complete validation
27. Submit PR to sindresorhus/awesome
28. Respond to feedback promptly

---

## 14. Key Resources

### Official Documentation
- [sindresorhus/awesome](https://github.com/sindresorhus/awesome) - Main repository
- [Awesome manifesto](https://github.com/sindresorhus/awesome/blob/main/awesome.md) - Philosophy
- [Contributing guidelines](https://github.com/sindresorhus/awesome/blob/main/contributing.md) - Submission requirements
- [Create list guide](https://github.com/sindresorhus/awesome/blob/main/create-list.md) - Setup instructions
- [Pull request template](https://github.com/sindresorhus/awesome/blob/main/pull_request_template.md) - Submission checklist

### Tools
- [awesome-lint](https://github.com/sindresorhus/awesome-lint) - Official linter
- [lychee](https://github.com/lycheeverse/lychee) - Link checker
- [lychee-action](https://github.com/lycheeverse/lychee-action) - GitHub Action for lychee
- [doctoc](https://github.com/thlorenz/doctoc) - TOC generator
- [Shields.io](https://shields.io/) - Badge service
- [awesome-actions](https://github.com/sdras/awesome-actions) - GitHub Actions catalog

### Templates
- [awesome-list-template](https://github.com/jthegedus/awesome-list-template) - Complete starter template
- [nayafia/contributing-template](https://github.com/nayafia/contributing-template) - Contributing guide template
- [Contributor Covenant](https://www.contributor-covenant.org/) - Code of Conduct

### Community
- [awesome-list topic](https://github.com/topics/awesome-list) - All awesome lists
- [badges/awesome-badges](https://github.com/badges/awesome-badges) - Badge resources
- [mntnr/awesome-contributing](https://github.com/mntnr/awesome-contributing) - Contributing guides

---

## 15. Quality Gate Verification

Before proceeding to roadmap planning, verify:

### Conventions
- ✅ Current with 2026 sindresorhus/awesome guidelines
- ✅ All naming conventions documented
- ✅ Formatting rules with examples
- ✅ Repository requirements specified

### Tooling
- ✅ awesome-lint configuration provided
- ✅ lychee setup with caching
- ✅ doctoc integration documented
- ✅ GitHub Actions workflows complete

### Rationale
- ✅ Every tool choice explained (WHY not just WHAT)
- ✅ Alternatives considered and rejected
- ✅ Anti-patterns documented
- ✅ Success metrics defined

### Actionability
- ✅ Version numbers specified
- ✅ Complete code examples
- ✅ Step-by-step checklist
- ✅ Migration timeline provided

---

## Conclusion

Creating a successful awesome list requires:

1. **Strict adherence** to sindresorhus/awesome conventions
2. **Automated quality checks** via awesome-lint and lychee
3. **Ongoing maintenance** through CI/CD and community engagement
4. **Ruthless curation** - quality over quantity

The tooling stack is deliberately minimal:
- awesome-lint (required)
- lychee (link checking)
- doctoc (TOC generation)
- GitHub Actions (automation)

Avoid the temptation to over-engineer. These tools, combined with the official guidelines, are battle-tested across thousands of awesome lists.

**Next Steps:** Use this STACK.md to inform your .planning/ROADMAP.md, breaking implementation into phases with clear milestones.

---

**Research Sources:**
- [sindresorhus/awesome](https://github.com/sindresorhus/awesome)
- [sindresorhus/awesome-lint](https://github.com/sindresorhus/awesome-lint)
- [lycheeverse/lychee-action](https://github.com/lycheeverse/lychee-action)
- [thlorenz/doctoc](https://github.com/thlorenz/doctoc)
- [sdras/awesome-actions](https://github.com/sdras/awesome-actions)
- [badges/awesome-badges](https://github.com/badges/awesome-badges)
- [Shields.io](https://shields.io/)

**Research Date:** 2026-01-26
**Verified:** All tools and guidelines current as of January 2026
**Ready for:** Roadmap planning and implementation
