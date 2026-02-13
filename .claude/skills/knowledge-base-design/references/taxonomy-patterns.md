# Taxonomy and Categorization Patterns

Practical guidance for designing category systems and tag hierarchies.

---

## MECE Principle

**Mutually Exclusive, Collectively Exhaustive** - The gold standard for categorization.

### Mutually Exclusive

Each item belongs in exactly one category at its level:

| Good | Bad |
|------|-----|
| Billing, Account, Features | Billing, Payments, Account (overlap) |
| Desktop App, Mobile App, Web App | Apps, Mobile, Desktop (overlap) |

### Collectively Exhaustive

Categories cover all possible content:

| Good | Bad |
|------|-----|
| Getting Started, Using Features, Troubleshooting, Reference | Getting Started, Features (missing support content) |

### When Perfect MECE Isn't Possible

- Use tags for cross-cutting concerns
- Create "Other" or "General" category (use sparingly)
- Accept some polyhierarchy with clear canonical locations

---

## Category Design Principles

### Size Balance

Aim for similar-sized categories:

| Issue | Solution |
|-------|----------|
| One huge category, several tiny | Split large, merge small |
| Categories with 1-2 items | Promote items up, merge categories |
| Categories with 30+ items | Split into subcategories |

**Target**: 5-12 items per category level

### Naming Conventions

| Do | Don't |
|----|-------|
| Use user language | Use internal jargon |
| Be specific | Be vague ("Miscellaneous") |
| Use parallel structure | Mix verbs and nouns |
| Keep concise (2-4 words) | Write sentences |

**Examples:**

| Bad | Good |
|-----|------|
| "Stuff About Billing" | "Billing & Payments" |
| "How to Get Started" | "Getting Started" |
| "FAQ" | Distribute to relevant categories |

### Parallel Structure

Categories at same level should follow same pattern:

```markdown
# Good (all nouns)
- Account Settings
- Billing Options
- Team Management

# Good (all gerunds)
- Getting Started
- Managing Projects
- Troubleshooting Issues

# Bad (mixed)
- Account Settings
- How to Bill
- Teams
```

---

## Tag Systems

### Flat Tags

Simple labels without hierarchy:

```
Tags: beginner, video, quick-start, billing
```

**Best for:**
- Cross-cutting themes
- Content format indicators
- Audience markers

### Hierarchical Tags

Tags with parent-child relationships:

```
Product: ClarityOS > Reports > Custom Reports
Audience: External > Clients > Enterprise
```

**Best for:**
- Product/feature associations
- Complex audience segmentation
- Multi-dimensional filtering

### Tag Governance

| Rule | Rationale |
|------|-----------|
| Define tag vocabulary upfront | Prevents tag sprawl |
| Assign tag owner | Someone approves new tags |
| Review quarterly | Remove unused, merge duplicates |
| Limit tags per article (5-7) | Forces prioritization |

### Tag Anti-Patterns

| Pattern | Problem | Solution |
|---------|---------|----------|
| Too many tags | Nothing is findable | Strict vocabulary, limits |
| Synonym tags | Dilutes results | Canonical tags + aliases |
| Orphan tags | Used once, forgotten | Minimum usage threshold |
| Overlapping tags | "billing" + "payments" | Merge or differentiate clearly |

---

## Card Sorting Method

User research technique for validating taxonomy.

### Open Card Sort

Users group items and name groups themselves.

**When to use:** Early design, discovering user mental models

**Process:**
1. Write each content item on a card (30-60 items)
2. Ask users to group related cards
3. Ask users to name each group
4. Analyze patterns across multiple users

### Closed Card Sort

Users sort items into predefined categories.

**When to use:** Validating proposed structure

**Process:**
1. Define your categories
2. Give users content items to sort
3. Measure agreement on placement
4. Identify problematic items (low agreement)

### Tree Testing

Users find items in proposed navigation.

**When to use:** Testing findability of structure

**Process:**
1. Build navigation tree (no content)
2. Give users tasks: "Find how to reset password"
3. Track paths taken, success rate
4. Identify problem areas

### Sample Size

| Method | Minimum Users | Ideal |
|--------|---------------|-------|
| Open sort | 15 | 30+ |
| Closed sort | 15 | 30+ |
| Tree test | 50 | 100+ |

---

## Content Type Taxonomy

Categorizing by content purpose:

| Type | Purpose | Structure |
|------|---------|-----------|
| **Concept** | Explain what/why | Definition, context, examples |
| **How-to** | Step-by-step instruction | Prerequisites, steps, verification |
| **Reference** | Look up details | Tables, specs, parameters |
| **Troubleshooting** | Solve problems | Symptom, cause, solution |

### Mixing Content Types

**Don't** put all types on one page.

**Do** link between related types:

```
[How-to: Set Up SSO]
  → Links to [Concept: What is SSO?]
  → Links to [Reference: SSO Configuration Options]
  → Links to [Troubleshooting: SSO Login Failures]
```

---

## Audience-Based Organization

### Segmentation Options

| Dimension | Examples |
|-----------|----------|
| Role | Admin, User, Developer |
| Experience | Beginner, Intermediate, Advanced |
| Use case | Sales, Support, Operations |
| Plan/tier | Free, Pro, Enterprise |

### Implementation Approaches

**Separate sections:**
```
/docs/admin/
/docs/users/
/docs/developers/
```

**Filtered views:**
Same content, filtered by audience tag

**Hybrid:**
Shared basics + audience-specific advanced content

### Audience Overlap

When content serves multiple audiences:
1. Write for primary audience
2. Add callouts for others: "Admins: See also [Admin Guide]"
3. Use role-based hints: `{% hint %}For developers: ...{% endhint %}`

---

## Common Taxonomy Pitfalls

### Over-Categorization

**Symptom:** Deep hierarchies, many empty categories

**Fix:** Flatten structure, merge sparse categories

### Under-Categorization

**Symptom:** Long lists, no grouping, users scroll endlessly

**Fix:** Group by theme, add subcategories

### Organization Mirroring

**Symptom:** Navigation matches org chart, not user needs

**Fix:** Reorganize around user tasks and topics

### Premature Optimization

**Symptom:** Complex taxonomy for small content set

**Fix:** Start simple, add structure as content grows

### Taxonomy Debt

**Symptom:** Structure made sense initially, now outdated

**Fix:** Schedule regular audits, evolve with content

---

## Taxonomy Evolution

### When to Restructure

- Content volume doubled since last structure
- New product/feature area doesn't fit
- User feedback indicates findability issues
- Search analytics show failed queries

### Migration Approach

1. **Audit current state** - Document what exists
2. **Analyze usage** - What's accessed, what's orphaned
3. **Design new structure** - With user input
4. **Map old to new** - Every item has a destination
5. **Implement redirects** - Preserve bookmarks
6. **Communicate change** - Notify users
7. **Monitor** - Track findability metrics post-migration
