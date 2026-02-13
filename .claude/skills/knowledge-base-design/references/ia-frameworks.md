# Information Architecture Frameworks

Core principles for structuring knowledge bases effectively.

---

## LATCH Framework

Five fundamental ways to organize information (Richard Saul Wurman):

| Method | Best For | Example |
|--------|----------|---------|
| **Location** | Geographic or spatial content | Office guides by region, store locators |
| **Alphabet** | Reference lookups, glossaries | API reference, terminology |
| **Time** | Sequential processes, history | Release notes, onboarding steps |
| **Category** | Topical groupings | Product features, department docs |
| **Hierarchy** | Importance or complexity levels | Beginner → Advanced guides |

### Choosing Your Primary Organization

1. **Start with user mental models** - How do users think about this content?
2. **Support with secondary organization** - Add search, tags, or filters
3. **Avoid mixing primary methods** - Pick one, be consistent

---

## Diátaxis Framework

Popular documentation framework that organizes content by user need and mode:

| Category | Purpose | User Mode | Structure |
|----------|---------|-----------|-----------|
| **Tutorials** | Learning-oriented | Study | Step-by-step lessons with exercises |
| **How-to guides** | Task-oriented | Work | Goal-focused procedures |
| **Reference** | Information-oriented | Work | Technical descriptions, specs |
| **Explanation** | Understanding-oriented | Study | Conceptual discussions |

### When to Use Each

| User Need | Content Type |
|-----------|--------------|
| "I want to learn" | Tutorial |
| "I want to achieve X" | How-to guide |
| "I need to look up Y" | Reference |
| "I want to understand why" | Explanation |

### Applying Diátaxis

- **Don't mix types** on single pages — link between them instead
- **Tutorials** should be completable by beginners
- **How-to guides** assume user knows what they want
- **Reference** should be comprehensive and scannable
- **Explanation** provides context, not instructions

Use as-is or adapt for your use case. The framework is a starting point, not a rigid rule.

---

## Hub-and-Spoke Model

Category landing pages that link to related content:

```
[Hub: Getting Started]
    ├── Spoke: Account Setup
    ├── Spoke: First Project
    ├── Spoke: Invite Team Members
    └── Spoke: Configuration Basics
```

### Hub Page Best Practices

- Brief overview (2-3 sentences max)
- Clear visual hierarchy of spokes
- Progress indicators for sequential content
- "Next steps" at bottom

### When to Use

- Onboarding sequences
- Feature categories
- Learning paths
- Troubleshooting by topic

---

## Hierarchical vs Faceted Taxonomy

### Hierarchical (Tree Structure)

```
Products
├── Software
│   ├── Desktop
│   └── Mobile
└── Hardware
    ├── Computers
    └── Accessories
```

**Use when:**
- Content has clear parent-child relationships
- Users navigate top-down
- Categories are stable over time

### Faceted (Multiple Dimensions)

Content tagged with multiple independent attributes:

| Article | Type | Audience | Product |
|---------|------|----------|---------|
| Setup Guide | How-to | New Users | ClarityOS |
| API Auth | Reference | Developers | Platform |

**Use when:**
- Users approach content from different angles
- Content spans multiple categories
- Search/filter is primary navigation

---

## Depth Guidelines

### The 3-Click Rule (Adapted)

Users should reach any content within **3-4 navigation actions**:

| Level | Content Type | Example |
|-------|--------------|---------|
| 1 | Category | "Billing" |
| 2 | Subcategory | "Payment Methods" |
| 3 | Article | "Add a Credit Card" |
| 4 | Section (within article) | "Troubleshooting" |

### Signs of Too Much Depth

- Categories with only 1-2 items
- Users can't predict where content lives
- Duplicate navigation paths to same content

### Signs of Too Little Depth

- Category pages with 20+ items
- No logical grouping of related content
- Scrolling replaces navigation

---

## Progressive Disclosure

Surface essentials first, reveal details on demand.

### Article Level

```markdown
# Feature Name

Brief description of what this does.

## Quick Start
Essential steps only.

## Detailed Configuration
Full options (collapsed by default or linked).

## Advanced Topics
Edge cases, integrations (separate page or expandable).
```

### Navigation Level

1. **Top nav**: Major categories only (5-7 max)
2. **Sidebar**: Subcategories within current section
3. **In-page**: Related links, "See also" sections

### Implementation Tips

- Use expandable sections for optional details
- Link to reference docs rather than inline everything
- Default to simplest path, offer alternatives

---

## Polyhierarchy

When content legitimately belongs in multiple places:

### Approaches

| Method | Pros | Cons |
|--------|------|------|
| **Canonical + Links** | Single source of truth | Users may miss alternate paths |
| **Duplicate with Sync** | Multiple entry points | Maintenance burden |
| **Tags/Filters** | Flexible discovery | Requires search behavior |

### Recommended: Canonical + Cross-Links

1. Place article in primary location
2. Add "See also" links from secondary locations
3. Use consistent cross-reference format:

```markdown
{% hint style="info" %}
Looking for [Topic]? See [Link to canonical location].
{% endhint %}
```

---

## Navigation Patterns

### Global Navigation

Persistent across all pages:
- Home/logo
- Major sections (5-7 max)
- Search
- User account

### Local Navigation

Context-specific:
- Sidebar for current section
- Breadcrumbs showing location
- Previous/Next for sequential content

### Contextual Navigation

Within content:
- Related articles
- Prerequisites
- "Was this helpful?" with alternatives

---

## Mental Model Alignment

### Discovery Techniques

1. **User interviews**: "Where would you look for X?"
2. **Search log analysis**: What terms do users try?
3. **Support ticket patterns**: What can't they find?
4. **Card sorting**: Let users group content

### Common Misalignments

| Internal Thinking | User Thinking |
|-------------------|---------------|
| "Billing Settings" | "Change my payment" |
| "API Documentation" | "Connect to other tools" |
| "Knowledge Base" | "Help" or "Support" |

### Resolution

- Use user language in navigation
- Add synonyms to search index
- Create multiple paths to same content
