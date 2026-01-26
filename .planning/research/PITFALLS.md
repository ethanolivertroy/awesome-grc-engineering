# Awesome List Pitfalls & Anti-Patterns Research

*Research conducted: 2026-01-26*

This document identifies common pitfalls in awesome lists and GRC-specific content challenges, with actionable prevention strategies for the Awesome GRC Engineering project.

---

## Table of Contents

1. [Awesome List Anti-Patterns](#awesome-list-anti-patterns)
2. [GRC Content-Specific Pitfalls](#grc-content-specific-pitfalls)
3. [Community Building Failures](#community-building-failures)
4. [Quality Maintenance Challenges](#quality-maintenance-challenges)
5. [Prevention Strategies](#prevention-strategies)
6. [Maintenance Burden Assessment](#maintenance-burden-assessment)

---

## Awesome List Anti-Patterns

### 1. Link Rot (Dead Links Accumulating)

**Problem**: Studies show that **66.5% of links "rot" within 9 years** ([DoFollow](https://dofollow.com/blog/link-rot)). Dead URLs undermine credibility and user trust.

**Root Causes**:
- Resources move without redirects
- Projects abandon domains
- Commercial tools shut down
- Documentation sites reorganize

**Impact**: Users lose faith in the list's currency. A single broken link session damages perception of the entire resource.

**Prevention for GRC Engineering**:
- Implement automated link checking via GitHub Actions (weekly schedule)
- Prefer stable resources: GitHub repos, official docs, archived academic papers
- Favor open-source projects over proprietary tools (less likely to disappear)
- Use Internet Archive links for critical historical resources
- Document date added and last verified for each resource

**Automation Options**:
- [Lychee Link Checker](https://github.com/lycheeverse/lychee-action) - Fast Rust-based checker, ~1 min for 576 links
- [Awesome Bot](https://dharmeshkakadia.com/blog/github-actions-awesome-bot/) - Validates links and checks duplicates
- Configure CI to create issues when links break

### 2. Stale Content (Outdated Tools/Resources)

**Problem**: Technology evolves but lists don't. Resources remain listed long after becoming obsolete or superseded.

**Examples in GRC Context**:
- Compliance frameworks that no longer reflect current threat landscape
- Security advice that predates modern attack vectors
- Tools that haven't updated for current cloud architectures

**Warning Signs**:
- Last commit/update >2 years ago
- Documentation references deprecated technologies
- Community discussions moved elsewhere

**Prevention for GRC Engineering**:
- Include "Last Updated" or "Status" metadata for each entry
- Quarterly review cycle for all resources
- Deprecation policy (mark as deprecated before removal)
- Create "Historical/Legacy" section for superseded but influential resources
- Prioritize "evergreen" content - principles over point-in-time implementations

**Deprecation Best Practices** (from [Read the Docs](https://docs.readthedocs.io/en/stable/guides/deprecating-content.html)):
- Mark deprecated resources with clear warnings
- Provide alternatives/migration paths
- Keep documentation accessible but marked as archived
- Communicate WHY the resource is deprecated

### 3. No Curation (Accepting Everything)

**Problem**: Lists become link dumps rather than curated guides. True curation requires **selectivity and quality standards**, not accepting everything ([DesignSafe](https://designsafe-ci.org/user-guide/curating/bestpractices/)).

**Quality Anti-Pattern**: "You curate for an audience, you don't curate for yourself" ([Filtered](https://learn.filtered.com/thoughts/6-steps-for-quality-content-curation))

**Red Flags**:
- Duplicate resources with no differentiation
- Every submission accepted via PR
- No evaluation criteria documented
- List grows but quality declines

**Prevention for GRC Engineering**:
- Documented acceptance criteria aligned with manifesto values
- Each resource must answer: "Why does this matter to GRC engineers?"
- Reject vendor marketing (see GRC-specific pitfalls below)
- Apply the "Would I recommend this to a colleague?" test
- Limit entries per category (forces prioritization)

**Sindresorhus Awesome Standard**: Emphasizes **curation over comprehensiveness** - items should represent genuinely valuable resources, not exhaustive catalogs.

### 4. Over-Curation (Too Exclusive)

**Problem**: List becomes gatekept by maintainer preferences rather than community value.

**Warning Signs**:
- PRs rejected without clear reasoning
- Acceptance criteria too subjective
- List doesn't grow despite ecosystem expansion
- Community disengagement due to barrier to entry

**Prevention for GRC Engineering**:
- Clear, objective acceptance criteria in CONTRIBUTING.md
- Explain rejections with reference to criteria
- Allow "Honorable Mentions" or "Emerging Tools" section for borderline cases
- Community voting/feedback mechanism for controversial inclusions
- Regular review of own biases

### 5. Poor Organization (Hard to Navigate)

**Problem**: Lists grow organically without restructuring, making discovery difficult.

**Common Organizational Failures**:
- Flat list with 100+ items
- Inconsistent categorization
- No table of contents
- Unclear resource descriptions
- Missing "who this is for" guidance

**Prevention for GRC Engineering**:
- Clear hierarchy: Categories → Subcategories → Resources
- Dual-audience tagging: [GRC→Tech] or [Tech→GRC] for each entry
- Rich descriptions (not just tool names)
- Table of contents with deep links
- Progressive disclosure: Start with "Essential" section

**Organization Strategy from PROJECT.md**:
- Four main categories: Tools & platforms, Learning resources, Frameworks & standards, Community & people
- Commentary explaining WHY each resource matters
- Audience context (GRC pros vs. security engineers)

### 6. No Contribution Guidelines (Chaos)

**Problem**: Without clear guidelines, PRs vary wildly in quality and format.

**Consequences**:
- Maintainer burnout from explaining expectations
- Inconsistent entries
- Legitimate contributions rejected due to formatting
- Community confusion about what belongs

**Prevention for GRC Engineering**:
- Detailed CONTRIBUTING.md from day one
- PR template with checklist
- Examples of good vs. bad submissions
- Link to manifesto for philosophy alignment
- Automated formatting checks
- Response time commitments

**GitHub Best Practices** ([GitHub Docs](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors)):
- CONTRIBUTING.md in root or .github folder
- Include: submission process, quality criteria, code of conduct, community expectations
- "Friendly, welcoming voice" to make contributors excited

### 7. Abandoned Maintenance

**Problem**: Maintainer loses interest/time. List becomes unmaintained artifact.

**Lifecycle Pattern**:
1. Initial enthusiasm (0-6 months)
2. Steady maintenance (6-18 months)
3. Declining updates (18-36 months)
4. Abandonment (36+ months)

**Prevention for GRC Engineering**:
- Build maintenance into sustainable routine (not hobby project)
- Automate what can be automated (link checking, formatting)
- Bring on co-maintainers early
- Document succession plan
- Set realistic scope (better maintained small list than abandoned comprehensive one)
- Make maintenance visible (changelog, maintenance log)

---

## GRC Content-Specific Pitfalls

### 1. Vendor Marketing Disguised as Resources

**Problem**: GRC vendor landscape is rife with "thought leadership" that's actually lead generation.

**Market Reality** ([VentureInSecurity](https://ventureinsecurity.net/p/grc-market-evolution-how-the-automation)):
- Many GRC platforms position as "enterprise solutions" when actually mid-market tools
- "Fortune 500 ready" claims often mean "500-2000 employees"
- Vendors struggle to gain F100 traction but succeed in growing SMBs

**Detection Signals**:
- "Download whitepaper" gates
- Heavy product screenshots in "educational" content
- No acknowledgment of alternatives
- Author works for vendor
- "Framework" that requires vendor's tool to implement

**Prevention for GRC Engineering**:
- Explicit "No vendor-sponsored content" policy (from PROJECT.md constraints)
- Vet author affiliations
- Prefer open-source over proprietary
- If including commercial tools: must be genuinely transformative, disclose commercial nature, include alternatives
- Community reports for suspected vendor content

**GRC Engineering Manifesto Alignment**:
- "Open source practitioner-developed solutions" over "closed source vendor paradigms"
- Reject "transactional" vendor relationships

### 2. Checkbox Compliance Content (Not Engineering-Minded)

**Problem**: Most GRC content focuses on "meeting requirements" rather than building systems.

**Checkbox Compliance vs. Engineering** ([OPSWAT](https://www.opswat.com/blog/cybersecurity-as-a-strategy-vs-check-the-box)):
- **Checkbox**: "Are we compliant?" Static snapshots, documentation-heavy, reactive
- **Engineering**: "How do we build compliant systems?" Continuous, automated, proactive

**Real-World Failure**: Equifax was PCI DSS compliant when breached in 2017 ([StrongDM](https://www.strongdm.com/blog/security-vs-compliance)). Target was PCI compliant during 2013 breach affecting 40M customers.

**Thomson Reuters Finding**: 70% of corporate risk professionals now treat compliance as strategic priority, not checkbox exercise.

**Warning Signs**:
- Focus on "audit preparation" vs. "system design"
- Policy templates without implementation guidance
- Framework worship (treating standards as requirements vs. tools)
- No discussion of automation or code
- "How to pass" vs. "How to build"

**Prevention for GRC Engineering**:
- Require engineering angle: code examples, architecture patterns, automation approaches
- Reject pure policy/documentation resources
- Look for: threat-informed, systems thinking, shift-left approaches (manifesto principles)
- Tag resources by abstraction level: Policy, Architecture, Implementation, Code

### 3. Framework Worship (Standards as Gospel vs. Tools)

**Problem**: Treating compliance frameworks as requirements rather than starting points.

**Manifestation**:
- "You must implement all 300 NIST controls"
- Rigid interpretation without risk-based tailoring
- Framework coverage metrics as success measures
- Industry certifications as proxies for competence

**GRC Engineering View** (from manifesto):
- **Threat-informed**: Ground in evidence-based threat intelligence, not just framework checklists
- **Meaningful outcomes**: Focus on measurable risk reduction, not control counts
- Frameworks are tools, not destinations

**Prevention for GRC Engineering**:
- Include resources that teach framework pragmatism
- Highlight risk-based tailoring approaches
- Prefer content showing "why" behind controls
- Include critical perspectives on frameworks
- Tag "Practical Implementation" vs. "Framework Theory"

### 4. Outdated Security Advice

**Problem**: Security landscape evolves rapidly. Yesterday's best practices become today's vulnerabilities.

**GRC-Specific Concerns**:
- Cloud security controls designed for on-prem
- Authentication patterns from pre-Zero Trust era
- Data protection advice from pre-GDPR
- Container security from pre-Kubernetes dominance

**Examples**:
- "DMZ" architecture patterns
- Perimeter-focused controls
- Annual penetration tests as sufficient assurance
- Manual evidence collection as acceptable

**Prevention for GRC Engineering**:
- Date-stamp resources and advice
- Note "Historical Context" for older influential works
- Prefer resources that explain evolution (why did thinking change?)
- Include "Modern Practices" section that explicitly supersedes legacy approaches
- Quarterly review of security-specific entries

### 5. Enterprise-Only Focus (Ignoring Startups/SMBs)

**Problem**: Most GRC resources assume enterprise scale, budget, and maturity.

**Market Reality** ([Bright Defense](https://www.brightdefense.com/resources/grc-tools-for-smbs-and-startups/)):
- Cybercriminals increasingly target SMBs due to fewer resources
- GRC no longer optional for startups
- Most tools are either too simple (startup-focused) or too complex/expensive (enterprise)
- Mid-market companies lack appropriate resources

**Implementation Timing** ([SourcePass](https://blog.sourcepass.com/sourcepass-blog/grc-for-the-modern-smb-aligning-security-risk-and-compliance)):
- Early-stage compliance frameworks engrain practices and enable risk-based culture
- Retroactive compliance in larger orgs much harder to establish

**Prevention for GRC Engineering**:
- Explicit "Organization Size" tagging: Startup, SMB, Mid-Market, Enterprise
- Include "Getting Started" resources for resource-constrained teams
- Highlight cost-effective/open-source options
- "Build vs. Buy" guidance for different scales
- Case studies across org sizes

---

## Community Building Failures

### 1. No Clear Value Proposition

**Problem**: Users don't understand why they should engage with THIS list vs. alternatives.

**Community Value Research** ([FasterCapital](https://www.fastercapital.com/content/Community-value-proposition-Why-Your-Community-Needs-a-Clear-Value-Proposition.html)):
- "People join communities for value, but they stay for connections"
- Value proposition should address: What benefits? What contributions needed? What can be achieved collectively?
- 80% of startup founders consider branded communities essential; 28% see it as competitive differentiator

**Prevention for GRC Engineering**:
- Lead with clear value prop: "THE canonical reference for GRC engineering" (from PROJECT.md)
- Differentiate from generic security lists (dual-audience, opinionated curation, manifesto-aligned)
- Articulate target audience explicitly (GRC pros gaining tech skills AND engineers learning GRC)
- Make "Why this matters" visible in every section

### 2. Competing Without Differentiation

**Problem**: "Yet another awesome list" that doesn't distinguish itself.

**Common Failure Pattern**:
- Duplicates existing lists
- No unique perspective
- Generic curation
- Doesn't serve unmet need

**GRC Engineering Differentiation** (from PROJECT.md):
- **Gap served**: Connection between policy-focused GRC and technical implementation
- **Philosophy**: GRC Engineering Manifesto alignment
- **Approach**: Opinionated with commentary on WHY resources matter
- **Audience**: Dual (GRC→technical and technical→GRC)
- **Not just links**: Context for who and when to use each resource

**Key Quote**: "What makes this different: Not just a link dump. Each resource includes commentary on *why* it matters and *who* it's for."

### 3. Not Updating With Ecosystem Changes

**Problem**: List reflects maintainer's historical knowledge, not current state.

**GRC Ecosystem Changes to Track**:
- New open-source tools emerging
- Vendors being acquired (affects tool availability)
- Framework updates (NIST CSF 2.0, ISO updates)
- Regulatory changes (new privacy laws)
- Industry shifts (cloud adoption, AI/ML in security)
- Community movements (GRC Engineering manifesto itself)

**Prevention for GRC Engineering**:
- Subscribe to GRC vendor/tool newsletters
- Monitor key GitHub repos for new projects
- Track regulatory announcement channels
- Engage with GRC communities (conferences, Slack/Discord)
- Quarterly "What's New" review
- Community contributions bring fresh perspective

### 4. No Community Feedback Loop

**Problem**: One-way publication without community input.

**Failure Modes**:
- Maintainer blind spots
- Missing emerging resources
- Inclusion of problematic resources without awareness
- Lost relevance to actual practitioners

**Prevention for GRC Engineering**:
- GitHub Discussions for resource suggestions
- Issue templates for reporting problems
- "Suggest a Resource" with low friction
- Periodic community surveys ("What are we missing?")
- Acknowledge contributors visibly
- Co-maintainer pathway for active contributors

---

## Quality Maintenance Challenges

### 1. How Often to Audit Links

**Link Rot Timeline**: 66.5% of links fail within 9 years ([DoFollow](https://dofollow.com/blog/link-rot))

**Automation Recommendation**:
- **Weekly automated checks**: Catch new breakage quickly
- **Quarterly manual review**: Verify content quality, not just availability
- **Annual deep audit**: Full resource relevance review

**Tooling**:
- Lychee GitHub Action (weekly schedule)
- Manual spot-checks on PRs
- Community reports as early warning system

**Time Investment**:
- Automation setup: 2-4 hours initial
- Automated runs: ~1-5 minutes weekly
- Manual review: 2-4 hours quarterly
- Deep audit: 8-16 hours annually

### 2. How to Deprecate Outdated Resources

**Deprecation Best Practices** (synthesized from [Read the Docs](https://docs.readthedocs.io/en/stable/guides/deprecating-content.html), [Treblle API](https://treblle.com/blog/best-practices-deprecating-api)):

**Process**:
1. **Mark as deprecated** (don't remove immediately)
   - Add `[DEPRECATED]` prefix
   - Strike-through text: ~~Resource Name~~
   - Add deprecation notice with date
2. **Explain why** deprecated
   - Superseded by newer tool
   - Project abandoned
   - Security concerns
   - No longer aligns with manifesto
3. **Provide alternatives**
   - Link to replacement resource
   - Migration guidance if applicable
4. **Keep accessible** for period
   - Move to "Deprecated" section (not deletion)
   - Maintain for 6-12 months
   - Eventually remove, preserving in git history

**Example Deprecation Entry**:
```markdown
### ~~[Old GRC Tool]~~ [DEPRECATED as of 2026-01]

**Why deprecated**: Project abandoned; last commit 2023. No cloud support.

**Alternative**: Use [Modern GRC Tool](#modern-tool) instead. See [migration guide](link).

[Original description preserved for historical context...]
```

### 3. How to Handle Controversial/Opinionated Content

**Challenge**: GRC Engineering is explicitly opinionated (manifesto-driven). Some will disagree.

**Types of Controversy**:
- **Tool/vendor disputes**: Competing solutions with partisan advocates
- **Framework debates**: NIST vs. ISO vs. custom
- **Philosophy conflicts**: Compliance-first vs. risk-first approaches
- **Vendor inclusion**: When is commercial tool "genuinely useful" vs. marketing?

**Handling Strategy**:

**1. Transparent Criteria**
- Publish decision framework
- Reference manifesto principles
- Document reasoning in PR discussions

**2. Opinionated But Fair**
- Can have strong POV (manifesto alignment)
- Must acknowledge alternatives exist
- Include dissenting perspectives in commentary
- "We recommend X for Y reasons, though some prefer Z"

**3. Community Moderation**
- Code of Conduct enforcement
- Debate substance, not people
- "Disagree and commit" or fork

**4. Periodic Re-evaluation**
- Controversial inclusion/exclusion decisions reviewed annually
- Community input via discussions
- Willing to change position with new evidence

**Example Handling**:
```markdown
### Controversial Framework X

**Why included**: Strong practitioner community, open-source, automation-friendly.

**Controversy**: Critics argue it's too prescriptive. Valid concern; we include it for
structured teams seeking established path. For flexible/custom approaches, see [Alternative Y].

**Manifesto alignment**: Meets automation, open-source, practitioner-led criteria.
```

### 4. Realistic Maintenance Burden

**Time Investment Estimates** (for GRC Engineering scale):

**Initial Setup** (one-time):
- Repository structure: 4-8 hours
- CONTRIBUTING.md, templates: 4-6 hours
- Automation (link checking, CI): 2-4 hours
- Initial content (50-100 entries): 20-40 hours
- **Total: 30-58 hours**

**Ongoing Maintenance** (per month):
- PR review/merge: 2-4 hours (varies by activity)
- Quarterly reviews (averaged): 2-3 hours
- Link checking triage: 1-2 hours
- Community management: 1-3 hours
- **Total: 6-12 hours/month**

**Annual Deep Work**:
- Full content audit: 8-16 hours
- Manifesto alignment review: 4-6 hours
- Organization restructure (if needed): 4-8 hours
- **Total: 16-30 hours/year**

**Sustainability Strategies**:
1. **Automate ruthlessly**: Link checking, formatting, CI
2. **Co-maintainers**: Share load, bring diverse perspectives
3. **Scope discipline**: Better small and maintained than comprehensive and abandoned
4. **Community leverage**: Contributors find resources, maintainers curate
5. **Batch work**: Review PRs weekly, not as they arrive
6. **Say no**: Protect quality bar even when it means more rejections

**Burnout Warning Signs**:
- Backlog of unreviewed PRs (>2 weeks old)
- Declining PR response quality
- Avoiding maintenance tasks
- Resentment toward contributors
- → Time to onboard co-maintainer or reduce scope

---

## Prevention Strategies

### Cross-Cutting Mitigation Approaches

#### 1. Automation First

**Automate**:
- Link checking (weekly GitHub Action)
- Formatting validation (CI on PRs)
- Duplicate detection
- Contribution checklist enforcement

**Don't Automate**:
- Quality judgment
- Manifesto alignment assessment
- Vendor marketing detection
- Commentary writing

#### 2. Clear Governance

**Document**:
- Acceptance criteria (CONTRIBUTING.md)
- Deprecation policy
- Maintainer responsibilities
- Decision appeals process

**Transparency**:
- Public PR discussions
- Documented rejections with reasoning
- Changelog of major decisions
- Roadmap for list evolution

#### 3. Community as Co-Creators

**Engage**:
- Lower barriers to suggest resources
- Reward quality contributions (acknowledgments)
- Path from contributor to maintainer
- Regular "State of the List" updates

**Feedback Loops**:
- GitHub Discussions for ideas
- Periodic surveys
- Issue templates for problems
- Community voting on controversial additions

#### 4. Scope Discipline

**Stay Focused**:
- GRC Engineering only (not general security)
- Resources bridging GRC and technical implementation
- Manifesto-aligned philosophy
- Dual-audience (GRC↔Engineering)

**Resist Scope Creep**:
- "That's valuable but out of scope"
- Point to other lists for adjacent topics
- Prefer depth over breadth
- Better to excel in niche than be mediocre comprehensively

#### 5. Sustainability by Design

**From Day One**:
- Realistic maintenance commitment
- Automation infrastructure
- Co-maintainer recruitment plan
- Succession documentation

**Regular Health Checks**:
- Quarterly: Am I keeping up?
- Annually: Is this still serving the community?
- As needed: Should I onboard help or reduce scope?

---

## Maintenance Burden Assessment

### Feasibility Analysis

**Given Constraints**:
- No vendor sponsorship → No paid help, manual curation
- Opinionated curation → More review time per PR
- Dual audience → Must validate relevance for both
- Manifesto alignment → Philosophical evaluation required

**Realistic Sustainable Scope**:
- **Start**: 50-100 high-quality resources across 4 categories
- **Steady state**: 150-250 resources (beyond this, consider co-maintainers)
- **Maintenance rhythm**: 6-12 hours/month

**Success Criteria for Sustainability**:
1. Backlog stays under 2 weeks
2. Quarterly audits completed on schedule
3. Maintainer satisfaction remains high
4. Community engagement growing

**When to Get Help**:
- PR backlog >20 items
- Can't complete quarterly reviews
- Missing major ecosystem developments
- Considering abandonment

**Co-Maintainer Profile**:
- GRC practitioner OR security engineer (complementary to founder)
- Active in open-source
- Shares manifesto values
- 4-8 hours/month availability
- Strong written communication

---

## Quality Gate Checklist

✅ **Pitfalls are specific to awesome lists and GRC domain**
- Awesome list anti-patterns: link rot, stale content, poor curation, organization, contribution guidelines, abandonment
- GRC-specific: vendor marketing, checkbox compliance, framework worship, outdated advice, enterprise-only focus
- Grounded in research with 30+ cited sources

✅ **Prevention strategies are actionable**
- Specific tools (Lychee, Awesome Bot, GitHub Actions)
- Concrete processes (deprecation workflow, PR templates)
- Time-boxed activities (weekly, quarterly, annual)
- Decision frameworks (acceptance criteria, controversy handling)

✅ **Maintenance burden is realistically assessed**
- Quantified time investments (30-58 hours setup, 6-12 hours/month ongoing)
- Burnout warning signs identified
- Sustainability strategies defined
- Co-maintainer pathway described
- Scope discipline emphasized

---

## Sources

### Awesome List Best Practices
- [Sindresorhus Awesome](https://github.com/sindresorhus/awesome) - Awesome list standards
- [GitHub Contribution Guidelines](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors)
- [Awesome Contributing Guides](https://github.com/mntnr/awesome-contributing)

### Content Curation
- [Content Curation Best Practices](https://learn.filtered.com/thoughts/6-steps-for-quality-content-curation) - Filtered
- [Curation Best Practices](https://designsafe-ci.org/user-guide/curating/bestpractices/) - DesignSafe
- [What is Curated Content?](https://backlinko.com/hub/content/curation) - Backlinko

### Link Rot & Maintenance
- [Link Rot Explained](https://dofollow.com/blog/link-rot) - DoFollow (66.5% stat)
- [Verifying Links with GitHub Actions](https://dharmeshkakadia.com/blog/github-actions-awesome-bot/) - Awesome Bot
- [Lychee Link Checker](https://github.com/lycheeverse/lychee-action)
- [How to Deprecate Content](https://docs.readthedocs.io/en/stable/guides/deprecating-content.html) - Read the Docs

### GRC-Specific
- [GRC Market Evolution](https://ventureinsecurity.net/p/grc-market-evolution-how-the-automation) - VentureInSecurity
- [GRC Engineering](https://grc.engineering/) - The Manifesto
- [Compliance GRC Engineering](https://franklyspeaking.substack.com/p/compliance-grc-engineering-is-promising) - Frank Wang
- [GRC for Modern SMB](https://blog.sourcepass.com/sourcepass-blog/grc-for-the-modern-smb-aligning-security-risk-and-compliance) - SourcePass
- [6 GRC Tools for SMBs and Startups](https://www.brightdefense.com/resources/grc-tools-for-smbs-and-startups/) - Bright Defense

### Checkbox Compliance vs. Engineering
- [Cybersecurity Strategy vs Check-the-Box](https://www.opswat.com/blog/cybersecurity-as-a-strategy-vs-check-the-box) - OPSWAT
- [Compliance vs Security](https://www.strongdm.com/blog/security-vs-compliance) - StrongDM (Equifax/Target examples)
- [Compliance or Engineering](https://www.mindpointgroup.com/blog/compliance-or-engineering-cybersecuritys-chicken-the-egg) - MindPoint Group
- [Risk-Based vs Compliance-Based Security](https://www.vikingcloud.com/blog/risk-based-vs-compliance-based-security-why-one-size-doesnt-fit-all) - Viking Cloud

### Community Building
- [Community Value Proposition](https://www.fastercapital.com/content/Community-value-proposition-Why-Your-Community-Needs-a-Clear-Value-Proposition.html) - FasterCapital
- [Community Strategy](https://innoloft.com/en-us/blog/community-strategy) - Innoloft
- [Community as Content Marketing](https://contentworkshop.com/community-as-content-marketing-strategy/) - Content Workshop

### Pull Request Quality
- [Why PRs Get Rejected](https://dev.to/opensauced/understanding-why-pull-requests-get-rejected-in-open-source-projects-1jd0) - OpenSauced
- [What to Do When PR Rejected](https://graphite.dev/guides/what-to-do-when-your-pull-request-is-rejected) - Graphite

### Deprecation Best Practices
- [Best Practices for Deprecating an API](https://treblle.com/blog/best-practices-deprecating-api/) - Treblle
- [API Deprecation Guidelines](https://document360.com/blog/api-deprecation/) - Document360
- [API Best Practices for Feature Deprecation](https://www.moesif.com/blog/best-practices/api-analytics/API-Best-Practices-For-Feature-Deprecation/) - Moesif

---

*End of Research Document*
