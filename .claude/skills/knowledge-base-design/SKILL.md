---
name: knowledge-base-design
description: Design and structure knowledge bases using information architecture principles, L&D frameworks, and content strategy. Use when planning documentation structure, organizing content hierarchies, designing navigation, creating taxonomy systems, or auditing existing knowledge bases. Integrates with GitBook workflow.
---

# Knowledge Base Design

Strategic frameworks and tactical guidance for designing effective knowledge bases.

---

## Design Process

Follow this 5-phase workflow:

| Phase | Activities | Output |
|-------|------------|--------|
| **1. Research** | Content audit, journey mapping | Requirements doc |
| **2. Structure** | IA design, taxonomy, navigation hierarchy | Site map + taxonomy |
| **3. Content Strategy** | Content types, templates, interlinking plan | Content model |
| **4. Implementation** | Create structure in GitBook, migrate/write content | Live knowledge base |
| **5. Iteration** | Analytics review, user feedback, refinement | Improvement backlog |

---

## Documentation Frameworks

### Diátaxis Framework

Popular framework that organizes content into four categories:

| Category | Purpose | User Mode | Example |
|----------|---------|-----------|---------|
| **Tutorials** | Learning-oriented | Study | "Build your first app" |
| **How-to guides** | Task-oriented | Work | "How to reset password" |
| **Reference** | Information-oriented | Work | API docs, config options |
| **Explanation** | Understanding-oriented | Study | "How authentication works" |

Use as-is or adapt for your use case. See: `references/ia-frameworks.md`

### Documentation Types

| Type | Purpose | Orientation |
|------|---------|-------------|
| API docs/reference | Explore and use APIs | Reference |
| Quickstart | Get users running fast | Learning |
| Tutorials | Practical knowledge acquisition | Learning |
| How-to guides | Achieve specific tasks | Task |
| Changelog/release notes | Show what's new | Reference |
| FAQs/help center | Common questions | Support |

---

## Quick Decision Framework

Use **LATCH** to choose your primary organization:

| If users... | Organize by... | Example |
|-------------|----------------|---------|
| Need location-specific info | **Location** | Regional guides, office directories |
| Look up specific terms | **Alphabet** | Glossaries, API parameters |
| Follow sequences | **Time** | Onboarding steps, release history |
| Browse by topic | **Category** | Feature docs, department wikis |
| Progress through levels | **Hierarchy** | Beginner → Advanced paths |

**Most knowledge bases use Category as primary, with Time or Hierarchy for sequences.**

---

## Knowledge Base Types

Quick guidance by context:

### Internal Wiki / Team Docs

- Organize by team or function
- Include process documentation
- Version control for policies
- See: `references/content-strategy.md` → Content Types

### Customer Help Center

- Organize by user task/problem
- Prominent search
- Troubleshooting-heavy
- See: `references/taxonomy-patterns.md` → Audience-Based Organization

### Educational / L&D Content

- Learning paths with progression
- Mix formats (70:20:10 model)
- Prerequisites and sequencing
- See: `references/content-strategy.md` → 70:20:10 Framework

### Product Documentation

- Feature-based organization
- Clear getting started path
- Reference + how-to balance
- See: `references/ia-frameworks.md` → Hub-and-Spoke Model

---

## GitBook Integration

This skill complements the existing `gitbook` skill.

### KB Directory Structure & Audience

6 directories by audience and purpose. **No subdirectories within these folders.**

| Directory | Audience | Purpose | Content Types |
|-----------|----------|---------|---------------|
| **clarity-academy/** | Prospects (public) | SEO marketing - free educational resources | Coding guides, industry education, best practices |
| **help-center/** | Clients only | Support for existing clients | Payer alerts, EHR guides, tool guides |
| **company-hub/** | Internal employees | Company operations | Employee onboarding, brand, team, processes |
| **developer/** | Internal developers | Engineering docs | Technical documentation |
| **clarityos/** | All audiences | Product documentation | RCM services, ClarityPay, patient services |
| **updates/** | All audiences | Product updates | New features, changelog, release notes |

### Content Routing Rules

**Ask these questions in order:**

1. **Is this for employees only?** → `company-hub/`
2. **Is this technical/engineering?** → `developer/`
3. **Is this client support?** → `help-center/`
4. **Is this educational content for prospects?** → `clarity-academy/`
5. **Is this product documentation?** → `clarityos/`
6. **Is this a product update?** → `updates/`

### Common Routing Mistakes

| Content | Wrong | Correct |
|---------|-------|---------|
| Employee onboarding | clarityos | company-hub |
| Payer policy alerts | clarity-academy | help-center |
| Public coding education | help-center | clarity-academy |
| Internal processes | help-center | company-hub |
| Conference/event info | updates | context/projects/ |
| EHR-specific guides | clarity-academy | help-center |

### KB Types by Space

| Space | KB Type | Primary Organization |
|-------|---------|---------------------|
| Company Hub | Internal Wiki | Category (by team/function) |
| Developer | Internal Wiki + Reference | Category + Hierarchy |
| ClarityOS | Product Documentation | Category (features) + Time (onboarding) |
| Clarity Academy | Educational | Hierarchy (learning paths) |
| Help Center | Customer Help | Category (topics) + User Tasks |
| Updates | Changelog | Time (reverse chronological) |

### Structure Implementation

Once design is complete, use the `gitbook` skill for:
- Creating SUMMARY.md navigation
- Page creation and formatting
- GitBook-specific syntax (hints, tabs)
- File naming conventions

### Page Structure Requirements

Every page must include:

```markdown
---
description: Brief description for SEO and page display
---

# Page Title

Content...

---

## Related Documents

- [Link](file.md) - Description

---

*Last updated: Month Year*
```

| Element | Required | Purpose |
|---------|----------|---------|
| YAML frontmatter with `description` | Yes | SEO, page summaries |
| Single H1 title | Yes | Page heading |
| Horizontal rules between sections | Yes | Visual separation |
| Related Documents section | Yes | Cross-linking |
| Last updated date | Yes | Content freshness |

---

## Reference Files

Consult these for detailed guidance:

| Reference | When to Use |
|-----------|-------------|
| `references/ia-frameworks.md` | Choosing organization method, navigation design, depth decisions |
| `references/taxonomy-patterns.md` | Designing categories, tag systems, validating with users |
| `references/content-strategy.md` | Planning content types, user journeys, writing templates |
| `references/assessment-checklist.md` | Auditing existing KB, measuring health, planning improvements |

### GitBook References

Also see in the `gitbook` skill:
- `references/ia-best-practices.md` — GitBook-specific IA guidance
- `references/gitbook-syntax.md` — Hints, tabs, code blocks, formatting

### Official GitBook Docs

For content creation, consult `.gitbook-reference/creating-content/`:

| Resource | Path | Use For |
|----------|------|---------|
| Content blocks | `blocks/` | Hints, tabs, code blocks, tables, embeds |
| Page structure | `content-structure/page.md` | Pages, subpages, page groups |
| Formatting | `formatting/` | Inline formatting, markdown |
| Reusable content | `reusable-content.md` | Snippets, synced blocks |

---

## Starting a New Knowledge Base

### Step 1: Define Scope

Answer these questions:
- Who is the primary audience?
- What are their top 5 tasks/questions?
- What content exists already?
- What's the expected content volume (now vs 1 year)?

### Step 2: Choose Structure

Based on answers, select:
- Primary organization (LATCH)
- Depth (typically 3-4 levels max)
- Top-level categories (5-7 recommended)

### Step 3: Create Taxonomy

- Draft category names (user language)
- Validate with card sort or stakeholder review
- Document in taxonomy spec

### Step 4: Design Content Model

- Identify needed content types
- Create templates for each type
- Plan interlinking strategy

### Step 5: Build in GitBook

Use `gitbook` skill for implementation:
- Create folder structure
- Build SUMMARY.md
- Create template pages
- Migrate existing content

---

## Auditing an Existing Knowledge Base

### Quick Assessment (15 min)

Use `references/assessment-checklist.md` → Quick Health Check

### Full Audit (4+ hours)

1. **Findability audit** - Navigation + search testing
2. **Structure review** - Category balance, depth consistency
3. **Content quality** - Accuracy, freshness, completeness
4. **Analytics review** - Top pages, search queries, feedback

### Common Issues to Look For

| Issue | Symptom | Fix |
|-------|---------|-----|
| Orphan pages | Pages not in navigation | Add to SUMMARY.md |
| Dead ends | No outbound links | Add related links |
| Imbalanced categories | One huge, several tiny | Restructure |
| Stale content | No updates >12 months | Audit + refresh |
| Jargon navigation | Users can't find content | Rename with user language |

---

## AI-Friendly Documentation

Modern docs are read by both humans and AI. Clean structure improves AI answers and increases chances of being cited.

### AI Writing Best Practices

| Practice | Why |
|----------|-----|
| Clear, descriptive headings | Improves chunking and retrieval |
| Short, focused sections | Easier to cite accurately |
| Consistent terminology | Reduces confusion |
| Key facts in text (not just images) | AI can read text, not screenshots |
| Explicit links between topics | Provides retrieval context |
| Version info near content | Avoids outdated answers |

### AI-Friendly Elements

- **llms.txt** - Overview of site structure for AI tools
- **Markdown format** - Machine-readable content
- **Reusable patterns** - Steps, examples, FAQs

---

## Key Principles

1. **User mental models over org structure** - Organize how users think, not how your company is structured

2. **Shallow and wide over deep and narrow** - Prefer more top-level options with less nesting

3. **Consistency enables prediction** - Same patterns let users guess where content lives

4. **Multiple paths to content** - Navigation + search + internal links all work together

5. **Start simple, evolve with content** - Don't over-architect for content that doesn't exist yet

6. **Cross-reference, don't duplicate** - Link to content instead of repeating it

---

## Reference Implementation: Company Hub

The `company-hub/` space serves as a reference implementation for internal wikis:

### Structure Pattern

```
Getting Started (onboarding flow)
About Us (team, history, communication)
Our Business (positioning, customers, metrics, trends)
Brand Guidelines (voice, visual, terminology)
Department Guides (role-specific onboarding)
Operations (tools, processes)
```

### Learnings Applied

| Principle | Application |
|-----------|-------------|
| **Department guide parity** | Every major department should have an onboarding guide |
| **User-centric section names** | "About Us" vs "Who We Are", "Department Guides" vs "Marketing" |
| **Industry context in business** | Move trends/market content to business section, not department |
| **Cross-linking minimum** | Every page should have 3+ inbound links |

### Cross-Linking Audit Checklist

When auditing a KB for cross-linking:

1. Run a link analysis to identify pages with <3 inbound links
2. Check that onboarding pages link to brand/voice guidelines
3. Verify Related Documents section includes all logically connected pages
4. Ensure reciprocal links (if A links to B, B should link to A where sensible)
5. Landing page should link to all key starting points
