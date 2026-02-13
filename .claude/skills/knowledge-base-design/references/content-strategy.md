# Content Strategy for Knowledge Bases

Planning content structure, user journeys, and article design.

---

## User Journey Mapping

Align content to where users are in their journey.

### Journey Stages

| Stage | User Mindset | Content Needs |
|-------|--------------|---------------|
| **Awareness** | "What is this?" | Overview, benefits, use cases |
| **Evaluation** | "Is this right for me?" | Comparisons, pricing, requirements |
| **Onboarding** | "How do I start?" | Setup guides, quick starts, tutorials |
| **Adoption** | "How do I do X?" | How-tos, feature guides, best practices |
| **Mastery** | "How do I do X better?" | Advanced guides, optimization, integrations |
| **Troubleshooting** | "Something's wrong" | Error resolution, FAQs, support contact |

### Mapping Content to Stages

Create a matrix:

| Content | Awareness | Onboarding | Adoption | Mastery | Troubleshooting |
|---------|:---------:|:----------:|:--------:|:-------:|:---------------:|
| Quick Start Guide | | ✓ | | | |
| Feature Overview | ✓ | | | | |
| API Reference | | | | ✓ | |
| Common Errors | | | | | ✓ |

### Gap Analysis

1. List all existing content
2. Map to journey stages
3. Identify sparse stages
4. Prioritize creation for gaps

---

## Content Types

### Concept Articles

**Purpose:** Explain what something is and why it matters

**Structure:**
```markdown
# [Concept Name]

Brief definition (1-2 sentences).

## Overview

What is this? Why does it exist? When would you use it?

## Key Components

Break down the main parts or aspects.

## How It Works

High-level explanation of mechanism.

## Examples

Real-world applications or use cases.

## Related Topics

- [Related Concept 1]
- [How-to: Implement This Concept]
```

### How-To Articles

**Purpose:** Guide users through a specific task

**Structure:**
```markdown
# How to [Accomplish Task]

Brief description of what this achieves.

## Prerequisites

- Requirement 1
- Requirement 2

## Steps

### 1. First Step

Explanation and details.

### 2. Second Step

Explanation and details.

### 3. Third Step

Explanation and details.

## Verify It Worked

How to confirm success.

## Next Steps

- [Related how-to]
- [Advanced configuration]

## Troubleshooting

Common issues and solutions.
```

### Reference Articles

**Purpose:** Provide lookup information

**Structure:**
```markdown
# [Reference Topic]

Brief context for when to use this reference.

## [Category 1]

| Parameter | Type | Description | Default |
|-----------|------|-------------|---------|
| param1 | string | Does X | "value" |
| param2 | boolean | Enables Y | false |

## [Category 2]

| Option | Description |
|--------|-------------|
| option1 | Explanation |
| option2 | Explanation |

## Examples

Code or configuration examples.

## See Also

- [Related reference]
- [How-to using this reference]
```

### Troubleshooting Articles

**Purpose:** Help users resolve problems

**Structure:**
```markdown
# Troubleshooting: [Problem Area]

## [Symptom/Error Message]

### Cause

Why this happens.

### Solution

Steps to fix.

---

## [Another Symptom]

### Cause

Why this happens.

### Solution

Steps to fix.

---

## Still Having Issues?

- Check [related troubleshooting]
- Contact [support channel]
```

---

## 70:20:10 Learning Framework

Applied to knowledge base design:

| Percentage | Learning Type | KB Application |
|------------|---------------|----------------|
| **70%** | Experiential (doing) | Interactive tutorials, sandbox environments, "try it" sections |
| **20%** | Social (others) | Community forums, shared examples, case studies |
| **10%** | Formal (study) | Documentation articles, video courses, certifications |

### Implementation Ideas

**70% - Learning by Doing:**
- Embedded code runners
- Step-by-step tutorials with checkpoints
- Sample projects to clone
- "Practice" sections in articles

**20% - Learning from Others:**
- Community-contributed examples
- User showcases
- Discussion links in articles
- "How others solved this" sections

**10% - Formal Learning:**
- Structured documentation
- Video tutorials
- Learning paths with completion tracking
- Certification programs

---

## Interlinking Strategy

### Link Types

| Type | Purpose | Example |
|------|---------|---------|
| **Prerequisite** | "Read this first" | Before API tutorial → Authentication basics |
| **Related** | "Similar topic" | Reports feature → Analytics feature |
| **Deep dive** | "Learn more" | Overview → Detailed reference |
| **Next step** | "Do this next" | Setup → First project |

### Linking Best Practices

| Do | Don't |
|----|-------|
| Link to specific sections | Link to long pages generically |
| Use descriptive link text | "Click here" or "Learn more" |
| Check links during updates | Leave broken links |
| Link bidirectionally | Create dead ends |

### Link Density Guidelines

- **Minimum:** 2-3 outbound links per article
- **Maximum:** 1 link per 100-150 words
- **Placement:** Intro, relevant sections, end (Next Steps)

### Orphan Prevention

Every article should have:
- At least one inbound link (someone points to it)
- At least one outbound link (it points somewhere)
- Entry in navigation (SUMMARY.md)

---

## Content Planning Process

### 1. Audit Existing Content

```markdown
| Article | Type | Stage | Last Updated | Quality | Keep/Update/Archive |
|---------|------|-------|--------------|---------|---------------------|
| Setup Guide | How-to | Onboarding | 2024-01 | Good | Keep |
| Old Feature | Reference | Adoption | 2022-06 | Outdated | Archive |
```

### 2. Identify Gaps

Compare audit to:
- User journey stages
- Feature coverage
- Support ticket themes
- Search query analysis

### 3. Prioritize Creation

| Priority | Criteria |
|----------|----------|
| High | Onboarding blockers, frequent support issues |
| Medium | Feature adoption, common questions |
| Low | Edge cases, advanced topics |

### 4. Create Content Calendar

```markdown
| Week | Article | Type | Owner | Status |
|------|---------|------|-------|--------|
| W1 | SSO Setup | How-to | Alice | Draft |
| W1 | Auth Concepts | Concept | Bob | Review |
| W2 | API Errors | Troubleshooting | Alice | Planned |
```

---

## Writing Guidelines

### Voice and Tone

| Aspect | Guideline |
|--------|-----------|
| **Perspective** | Second person ("you") |
| **Voice** | Active, not passive |
| **Tone** | Helpful, confident, concise |
| **Jargon** | Define on first use or avoid |

### Formatting Standards

| Element | Standard |
|---------|----------|
| Headings | Sentence case ("Getting started", not "Getting Started") |
| Lists | Parallel structure, punctuation consistent |
| Code | Syntax highlighting, copy button |
| Images | Alt text, max width 800px |

### Scannability

- Lead with the key information
- Use headings every 200-300 words
- Bullet points for lists of 3+ items
- Tables for comparisons
- Bold key terms (sparingly)

### Article Length Guidelines

| Type | Target Length | Notes |
|------|---------------|-------|
| Concept | 500-1000 words | Enough to explain, not overwhelm |
| How-to | 300-800 words | Depends on steps |
| Reference | Varies | As long as needed, well-organized |
| Troubleshooting | 200-500 per issue | Quick to scan |

---

## Content Maintenance

### Review Triggers

| Trigger | Action |
|---------|--------|
| Product update | Review related docs |
| Support spike | Check/improve relevant content |
| Quarterly | Audit top 20 articles |
| Annually | Full content audit |

### Freshness Indicators

Consider adding to articles:
- Last updated date
- Product version applicability
- "Was this helpful?" feedback

### Deprecation Process

1. Mark as outdated (banner at top)
2. Link to replacement content
3. Remove from navigation (keep URL for bookmarks)
4. Archive after 6 months (redirect to replacement)

---

## Metrics to Track

### Engagement Metrics

| Metric | Indicates |
|--------|-----------|
| Page views | Interest/need |
| Time on page | Engagement (or confusion) |
| Bounce rate | Content mismatch |
| Scroll depth | Content consumption |

### Effectiveness Metrics

| Metric | Indicates |
|--------|-----------|
| Search → click | Findability |
| Support ticket deflection | Self-service success |
| Task completion | How-to effectiveness |
| Feedback ratings | User satisfaction |

### Search Analytics

| Data Point | Action |
|------------|--------|
| Top queries | Ensure content exists, is findable |
| Zero-result queries | Content gaps |
| Query → page mismatch | SEO/titling issues |
