# Knowledge Base Assessment Checklist

Evaluation and audit tools for knowledge base health.

---

## Quick Health Check

Run through these questions for a rapid assessment:

### Findability (5 minutes)

- [ ] Can you find the main help/docs entry point in under 3 seconds?
- [ ] Is search prominently available?
- [ ] Can you reach any article within 3-4 clicks from home?
- [ ] Does the navigation make sense without reading article content?
- [ ] Are category names user-language (not internal jargon)?

### Structure (5 minutes)

- [ ] Is there a clear landing page explaining what's available?
- [ ] Are categories roughly equal in size (no giant vs tiny)?
- [ ] Is nesting depth consistent (not 2 levels in one area, 5 in another)?
- [ ] Can you predict where content will be before clicking?
- [ ] Are there breadcrumbs or other location indicators?

### Content (5 minutes)

- [ ] Do articles have clear, descriptive titles?
- [ ] Is there a mix of content types (how-to, concept, reference)?
- [ ] Are articles interlinked (not dead ends)?
- [ ] Is there an obvious "getting started" path for new users?
- [ ] Are dates visible showing content freshness?

**Score:** Count checkmarks. 12-15 = Healthy, 8-11 = Needs work, <8 = Major issues

---

## Detailed Findability Audit

### Navigation Testing

| Test | Method | Pass Criteria |
|------|--------|---------------|
| 3-click test | Pick 10 random articles, navigate from home | 80%+ reachable in 3 clicks |
| Prediction test | Ask users where they'd look for X | 70%+ correct predictions |
| Return navigation | From deep page, return to section home | Clear path exists |

### Search Effectiveness

| Metric | Target | How to Measure |
|--------|--------|----------------|
| Search usage | >30% of sessions | Analytics |
| Zero results | <5% of searches | Search logs |
| First-click success | >60% | Search analytics |
| Query-to-click match | >70% | Compare query to clicked title |

### Common Search Problems

| Issue | Indicator | Fix |
|-------|-----------|-----|
| Content exists, not found | High zero-results for existing topics | Improve titles, add synonyms |
| Wrong results first | Users click result #3-5 | Adjust search weighting |
| Users refine queries | Multiple searches per session | Better content matching |

---

## Structure Health Check

### Category Analysis

```markdown
For each top-level category, document:

| Category | Sub-items | Depth Levels | Avg Items/Level |
|----------|-----------|--------------|-----------------|
| Getting Started | 8 | 2 | 4 |
| Features | 45 | 3 | 15 |
| API Reference | 120 | 4 | 30 |
```

**Red flags:**
- Any category with <3 items (merge up)
- Any category with >20 items at same level (split)
- Depth variance >2 levels across categories

### Orphan Page Detection

Pages without inbound links:

```bash
# Conceptual process:
1. List all pages in SUMMARY.md
2. Grep all .md files for internal links
3. Find pages never linked to
```

**Target:** 0 orphan pages (every page reachable via link + nav)

### Dead End Detection

Pages without outbound links:

**Target:** <10% of articles are dead ends

### Circular Link Detection

A → B → C → A chains without exit:

**Target:** 0 circular-only paths (every loop has an exit)

### Duplicate Content Check

| Type | How to Find | Resolution |
|------|-------------|------------|
| Exact duplicates | File comparison | Delete one, redirect |
| Near duplicates | Search similar titles | Merge or differentiate |
| Overlapping topics | Manual review | Split responsibilities |

---

## Consistency Review

### Naming Consistency

| Element | Check | Example |
|---------|-------|---------|
| Category names | Same grammatical structure | All nouns OR all gerunds |
| Article titles | Same pattern per type | "How to X" vs "Xing" |
| UI references | Match actual product | "Settings" not "Preferences" |

### Formatting Consistency

| Element | Standard | Audit Method |
|---------|----------|--------------|
| Headings | Sentence case | Sample 20 articles |
| Code blocks | Language specified | Grep for unmarked code blocks |
| Lists | Consistent punctuation | Sample review |
| Images | Alt text present | Find images without alt |

### Structural Consistency

| Element | Standard | Audit Method |
|---------|----------|--------------|
| How-to articles | Prerequisites → Steps → Verify | Template check |
| Reference articles | Consistent table format | Sample review |
| All articles | Intro paragraph present | First paragraph check |

---

## Content Quality Audit

### Accuracy Check

| Test | Method | Frequency |
|------|--------|-----------|
| Technical accuracy | SME review | Quarterly for top content |
| Link validity | Automated checker | Weekly |
| Screenshot currency | Compare to current UI | With each release |
| Code example testing | Run examples | Quarterly |

### Completeness Check

For each major feature/topic:

- [ ] Concept article exists (what is it?)
- [ ] How-to article exists (how to use it?)
- [ ] Reference article exists (all options documented?)
- [ ] Troubleshooting coverage (common issues addressed?)

### Freshness Audit

```markdown
| Age Bucket | Article Count | Action |
|------------|---------------|--------|
| <3 months | 45 | Current |
| 3-6 months | 30 | Review if product changed |
| 6-12 months | 25 | Audit needed |
| >12 months | 15 | Priority audit |
```

---

## User Feedback Analysis

### Feedback Collection Points

| Method | What It Measures | Implementation |
|--------|------------------|----------------|
| "Was this helpful?" | Article effectiveness | End of each article |
| Feedback form | Specific issues | Link in unhelpful flow |
| Support ticket tagging | Content gaps | Tag tickets that needed docs |
| Search behavior | Findability | Analytics |

### Feedback Triage

| Signal | Priority | Action |
|--------|----------|--------|
| Multiple "not helpful" on same article | High | Review and revise |
| Support tickets citing missing docs | High | Create content |
| Low engagement on important topic | Medium | Improve discoverability |
| Feedback requesting advanced content | Low | Add to roadmap |

### NPS/Satisfaction Benchmarks

| Rating | Target |
|--------|--------|
| "Helpful" rate | >80% |
| Documentation NPS | >30 |
| Self-service success | >70% |

---

## Analytics Integration

### Key Metrics Dashboard

| Metric | Source | Target |
|--------|--------|--------|
| Total page views | Analytics | Baseline + growth |
| Unique visitors | Analytics | Baseline + growth |
| Search usage % | Analytics | >30% |
| Avg. time on page | Analytics | 2-4 min for how-tos |
| Bounce rate | Analytics | <50% |
| Support deflection | Support + Analytics | >20% reduction |

### Content Performance Tiers

| Tier | Criteria | Management |
|------|----------|------------|
| Top 10% | Highest traffic | Prioritize accuracy, freshness |
| Middle 60% | Normal traffic | Standard maintenance |
| Bottom 30% | Low traffic | Audit for relevance, consolidate |

### Search Analytics Setup

Track and review:
- Top 50 search queries weekly
- Zero-result queries weekly
- Search-to-click paths monthly

---

## Iteration Triggers

### When to Make Small Updates

| Signal | Action |
|--------|--------|
| Single negative feedback | Review article |
| Minor product change | Update affected screenshots/steps |
| Broken link detected | Fix immediately |
| Outdated terminology | Search and replace |

### When to Restructure Section

| Signal | Threshold |
|--------|-----------|
| Multiple related articles with issues | 3+ articles in same area |
| Category size imbalance | 2x size difference vs siblings |
| User findability complaints | 5+ similar complaints |
| New major feature | Doesn't fit existing structure |

### When to Overhaul Knowledge Base

| Signal | Threshold |
|--------|-----------|
| Overall satisfaction score drop | >10% decrease |
| Support ticket volume spike | >25% increase citing docs |
| Major product pivot | Core functionality changed |
| Company rebrand | Terminology, voice changes |

---

## Audit Schedule Template

### Weekly (15 minutes)

- [ ] Check link validator results
- [ ] Review "not helpful" feedback
- [ ] Scan top search queries

### Monthly (1 hour)

- [ ] Review analytics trends
- [ ] Update content for recent releases
- [ ] Process accumulated feedback
- [ ] Check for orphan pages

### Quarterly (4 hours)

- [ ] Full category balance review
- [ ] Consistency audit (sample)
- [ ] Top 20 articles accuracy review
- [ ] Search effectiveness analysis
- [ ] Stakeholder feedback collection

### Annually (1-2 days)

- [ ] Complete content inventory
- [ ] Full freshness audit
- [ ] User research (card sorts, interviews)
- [ ] Structure evaluation
- [ ] Strategic planning for next year

---

## Audit Report Template

```markdown
# Knowledge Base Audit Report

**Date:** YYYY-MM-DD
**Auditor:** Name
**Scope:** [Full / Section / Specific issue]

## Executive Summary

- Overall health score: X/15
- Critical issues: X
- Improvement opportunities: X

## Findings

### Critical (Fix immediately)

1. [Issue]: [Impact]: [Recommendation]

### Important (Fix within 30 days)

1. [Issue]: [Impact]: [Recommendation]

### Nice to Have (Backlog)

1. [Issue]: [Impact]: [Recommendation]

## Metrics Snapshot

| Metric | Current | Previous | Target |
|--------|---------|----------|--------|
| | | | |

## Recommended Actions

| Priority | Action | Owner | Due |
|----------|--------|-------|-----|
| 1 | | | |
| 2 | | | |

## Next Audit

Scheduled: YYYY-MM-DD
Focus areas: [Based on this audit]
```
