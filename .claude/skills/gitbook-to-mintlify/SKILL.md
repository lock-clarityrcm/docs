---
name: gitbook-to-mintlify
description: Migrate and refactor GitBook documentation into Mintlify format. Use when converting GitBook repos, pages, or syntax to Mintlify MDX components and structure.
---

# GitBook to Mintlify Migration

Migrate documentation from GitBook to Mintlify. This skill covers file structure, navigation, content syntax, API docs, and asset handling.

## Before you start

1. **Invoke the `mintlify` skill** for Mintlify component reference and writing standards
2. **Read the GitBook source** — identify `SUMMARY.md`, `.gitbook.yaml`, `book.json`, and content files
3. **Inventory the content** — count pages, identify block types used, locate assets in `.gitbook/assets/`
4. **Check for OpenAPI specs** — if the GitBook site has `{% swagger %}` or `{% openapi %}` blocks, locate the spec file

## Migration checklist

- [ ] Convert `SUMMARY.md` to `docs.json` navigation
- [ ] Rename `.md` files to `.mdx` and add frontmatter
- [ ] Move `.gitbook/assets/` to `/images/` (and `/files/` for non-image assets)
- [ ] Fix all asset paths (relative `.gitbook/assets/` → root-relative `/images/`)
- [ ] Convert all GitBook block syntax (`{% %}` tags) to Mintlify components
- [ ] Convert HTML blocks (cards, figures, details) to Mintlify components
- [ ] Migrate API documentation (swagger/openapi blocks → OpenAPI spec or ParamField)
- [ ] Convert reusable content (`.gitbook/includes/`) to `/snippets/`
- [ ] Clean up GitBook artifacts (`&#x20;`, `<mark>` tags, `data-size` attributes)
- [ ] Run `mint broken-links` and `mint validate`

## File structure mapping

| GitBook | Mintlify | Notes |
|---------|----------|-------|
| `README.md` | `index.mdx` | Add `title` frontmatter |
| `SUMMARY.md` | `docs.json` navigation | Convert list hierarchy to JSON |
| `.gitbook.yaml` | `docs.json` | Merge config settings |
| `book.json` | `docs.json` | Legacy — merge relevant settings |
| `.gitbook/assets/` | `/images/` | Move all assets, update paths |
| `.gitbook/includes/` | `/snippets/` | Convert to MDX snippet format |
| `GLOSSARY.md` | Dedicated page or `<Tooltip>` | No direct equivalent |
| `chapter/README.md` | `chapter/index.mdx` | Section landing pages |
| `*.md` | `*.mdx` | All content files |

## Navigation conversion

### GitBook SUMMARY.md format

```markdown
# Summary

## Getting Started

* [Introduction](README.md)
* [Quick Start](getting-started/quickstart.md)
    * [Installation](getting-started/quickstart/installation.md)

## API Reference

* [Overview](api/README.md)
* [Users](api/users.md)
```

### Mintlify docs.json equivalent

```json
{
  "navigation": {
    "tabs": [
      {
        "tab": "Docs",
        "groups": [
          {
            "group": "Getting Started",
            "pages": [
              "index",
              "getting-started/quickstart",
              {
                "group": "Quickstart",
                "pages": ["getting-started/quickstart/installation"]
              }
            ]
          },
          {
            "group": "API Reference",
            "pages": [
              "api-docs/index",
              "api-docs/users"
            ]
          }
        ]
      }
    ]
  }
}
```

### Conversion rules

- `## Headings` in SUMMARY.md → `"group"` objects in docs.json
- Nested bullet lists → nested `"group"` objects or flat page arrays
- Link text in SUMMARY.md → `title` in frontmatter (GitBook uses SUMMARY.md for titles, not the file's H1)
- `README.md` in subdirectories → `index.mdx` in that directory
- Root `README.md` → `index.mdx` (site homepage)
- Cannot use `api` as a top-level folder name in Mintlify (Next.js reserved) — rename to `api-docs` or `api-reference`

## Frontmatter conversion

GitBook pages have minimal frontmatter. Mintlify requires at least `title`.

### GitBook source

```markdown
---
description: How to authenticate API requests
---

# Authentication
```

### Mintlify output

```yaml
---
title: "Authentication"
description: "How to authenticate API requests"
---
```

### Rules

- **Title**: Extract from SUMMARY.md link text (preferred) or from the first H1 in the file. Remove the H1 from the body since Mintlify renders the title from frontmatter.
- **Description**: Keep the `description` field as-is.
- **Hidden pages**: `hidden: true` maps directly.
- **Icons, covers, layout**: These are GitBook UI-only settings with no markdown representation — skip or set manually.

## Block syntax conversion

### Hints / Callouts

**GitBook:**
```markdown
{% hint style="info" %}
This is an info hint.
{% endhint %}

{% hint style="success" %}
Operation completed successfully.
{% endhint %}

{% hint style="warning" %}
This action cannot be undone.
{% endhint %}

{% hint style="danger" %}
This will delete all data permanently.
{% endhint %}
```

**Mintlify:**
```mdx
<Note>
This is an info hint.
</Note>

<Check>
Operation completed successfully.
</Check>

<Warning>
This action cannot be undone.
</Warning>

<Danger>
This will delete all data permanently.
</Danger>
```

**Mapping:** `info` → `<Note>`, `success` → `<Check>`, `warning` → `<Warning>`, `danger` → `<Danger>`

### Tabs

**GitBook:**
```markdown
{% tabs %}
{% tab title="Python" %}
```python
import requests
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
fetch('/api')
```
{% endtab %}
{% endtabs %}
```

**Mintlify:**
```mdx
<Tabs>
  <Tab title="Python">
    ```python
    import requests
    ```
  </Tab>
  <Tab title="JavaScript">
    ```javascript
    fetch('/api')
    ```
  </Tab>
</Tabs>
```

If all tabs contain only code blocks, consider using `<CodeGroup>` instead of `<Tabs>`.

### Code blocks with metadata

**GitBook:**
````markdown
{% code title="config.js" overflow="wrap" lineNumbers="true" %}
```javascript
const config = { debug: true };
```
{% endcode %}
````

**Mintlify:**
````mdx
```javascript config.js
const config = { debug: true };
```
````

The `title` attribute becomes the filename after the language identifier. `overflow` and `lineNumbers` have no direct Mintlify equivalent — Mintlify handles these automatically.

### Legacy code tabs

**GitBook (legacy):**
````markdown
{% code-tabs %}
{% code-tabs-item title="example.py" %}
```python
print("hello")
```
{% endcode-tabs-item %}
{% code-tabs-item title="example.js" %}
```javascript
console.log("hello")
```
{% endcode-tabs-item %}
{% endcode-tabs %}
````

**Mintlify:**
````mdx
<CodeGroup>
```python example.py
print("hello")
```
```javascript example.js
console.log("hello")
```
</CodeGroup>
````

### Expandable / Details

**GitBook:**
```html
<details>
<summary>Click to expand</summary>

Hidden content here.

</details>
```

**Mintlify:**
```mdx
<Accordion title="Click to expand">
Hidden content here.
</Accordion>
```

For multiple expandables, wrap in `<AccordionGroup>`.

If the GitBook source uses `<details open>`, add `defaultOpen={true}` to the Accordion.

### Stepper / Steps

**GitBook:**
```markdown
{% stepper %}
{% step %}
### Install dependencies
Run `npm install` to get started.
{% endstep %}

{% step %}
### Configure settings
Edit `config.json` with your API key.
{% endstep %}
{% endstepper %}
```

**Mintlify:**
```mdx
<Steps>
  <Step title="Install dependencies">
    Run `npm install` to get started.
  </Step>
  <Step title="Configure settings">
    Edit `config.json` with your API key.
  </Step>
</Steps>
```

Extract the step title from the H3 heading inside each `{% step %}` block. Remove the heading from the body.

### Embeds

**GitBook:**
```markdown
{% embed url="https://www.youtube.com/watch?v=abc123" %}
Video caption
{% endembed %}
```

**Mintlify:**
```mdx
<iframe
  className="w-full aspect-video rounded-xl"
  src="https://www.youtube.com/embed/abc123"
  title="Video caption"
  frameBorder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowFullScreen
/>
```

For non-video embeds, convert to a standard markdown link or `<Card>` with `href`.

Note: Convert YouTube `watch?v=ID` URLs to `embed/ID` format.

### Content references / Page links

**GitBook (modern):**
```markdown
{% content-ref url="guides/authentication.md" %}
[Authentication Guide](guides/authentication.md)
{% endcontent-ref %}
```

**GitBook (legacy):**
```markdown
{% page-ref page="guides/authentication.md" %}
```

**Mintlify:**
```mdx
<Card title="Authentication Guide" href="/guides/authentication" />
```

Or use a standard link if a card is too prominent: `[Authentication Guide](/guides/authentication)`

### File attachments

**GitBook:**
```markdown
{% file src="../.gitbook/assets/guide.pdf" %}
Download the guide
{% endfile %}
```

**Mintlify:**
```mdx
[Download the guide](/files/guide.pdf)
```

Move the file to a `/files/` directory in the Mintlify project.

### Reusable content / Includes

**GitBook:**
```markdown
{% include "../../.gitbook/includes/shared-warning.md" %}
```

**Mintlify:**
```mdx
import SharedWarning from '/snippets/shared-warning.mdx';

<SharedWarning />
```

Convert the included `.md` file to an `.mdx` snippet. Use arrow function exports for parameterized snippets.

### Images

**GitBook block image:**
```markdown
![Alt text](../.gitbook/assets/screenshot.png)
```

**GitBook image with caption (HTML):**
```html
<figure><img src="../.gitbook/assets/screenshot.png" alt="Alt text"><figcaption><p>Caption text</p></figcaption></figure>
```

**GitBook inline image:**
```html
<img src="../.gitbook/assets/icon.png" alt="" data-size="line">
```

**Mintlify block image:**
```mdx
![Alt text](/images/screenshot.png)
```

**Mintlify image with caption:**
```mdx
<Frame caption="Caption text">
  <img src="/images/screenshot.png" alt="Alt text" />
</Frame>
```

**Mintlify inline image:**
```mdx
![](/images/icon.png)
```

### Cards

**GitBook** exports cards as HTML tables with `data-view="cards"`:
```html
<table data-view="cards">
<thead><tr>
  <th>Title</th>
  <th>Description</th>
  <th data-hidden data-card-target data-type="content-ref">Link</th>
  <th data-hidden data-card-cover data-type="files">Cover</th>
</tr></thead>
<tbody>
<tr>
  <td>Getting Started</td>
  <td>Learn the basics</td>
  <td><a href="getting-started.md">getting-started.md</a></td>
  <td><a href=".gitbook/assets/cover.png">cover.png</a></td>
</tr>
<tr>
  <td>API Reference</td>
  <td>Full API docs</td>
  <td><a href="api/README.md">api/README.md</a></td>
  <td></td>
</tr>
</tbody>
</table>
```

**Mintlify:**
```mdx
<CardGroup cols={2}>
  <Card title="Getting Started" href="/getting-started" img="/images/cover.png">
    Learn the basics
  </Card>
  <Card title="API Reference" href="/api-docs">
    Full API docs
  </Card>
</CardGroup>
```

Parse the `<td>` cells to extract title, description, link, and cover image.

### Math / LaTeX

**GitBook block:**
```markdown
$$
E = mc^2
$$
```

**GitBook inline:**
```markdown
The formula is $$E = mc^2$$ in physics.
```

**Mintlify:**
```mdx
<Latex>E = mc^2</Latex>
```

### Drawings

**GitBook:**
```html
<img src=".gitbook/assets/diagram.drawing.svg" alt="" class="gitbook-drawing">
```

**Mintlify:**
```mdx
![Diagram](/images/diagram.svg)
```

Move the `.drawing.svg` file to `/images/`. Consider converting to a Mermaid diagram if the drawing is simple enough.

## API documentation conversion

### From `{% swagger %}` blocks

**GitBook:**
```markdown
{% swagger baseUrl="https://api.example.com" path="/v1/users" method="get" summary="List Users" %}
{% swagger-description %}
Returns a paginated list of users.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Bearer token
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
Page number
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```json
{ "users": [{ "id": "123", "name": "John" }] }
```
{% endswagger-response %}
{% endswagger %}
```

**Mintlify (manual approach):**
```mdx
---
title: "List Users"
api: "GET https://api.example.com/v1/users"
---

Returns a paginated list of users.

<ParamField header="Authorization" type="string" required>
  Bearer token
</ParamField>

<ParamField query="page" type="integer">
  Page number
</ParamField>

<ResponseExample>
```json
{ "users": [{ "id": "123", "name": "John" }] }
```
</ResponseExample>
```

**Mintlify (OpenAPI approach — preferred):** If multiple swagger blocks exist, extract them into an OpenAPI spec file and use `openapi:` frontmatter. This is more maintainable.

### From `{% openapi %}` blocks

**GitBook:**
```markdown
{% openapi src="./openapi.json" path="/pet" method="post" %}
{% endopenapi %}
```

**Mintlify:**
```yaml
---
title: "Create Pet"
openapi: "openapi.json POST /pet"
---
```

Add `"openapi": "openapi.json"` to `docs.json` if not already present.

## Cleanup tasks

After converting all blocks, clean up GitBook-specific artifacts:

### Remove emoji spacing entities
GitBook appends `&#x20;` after emoji codes. Remove them:
- `🚀&#x20;` → `🚀`
- `:rocket:&#x20;` → `:rocket:`

### Remove colored text markup
```html
<mark style="color:red;">important</mark>
```
Convert to bold (`**important**`) or remove the markup entirely. Mintlify has no inline color support.

### Remove `data-size` attributes
```html
<img src="..." data-size="line">
<img src="..." data-size="original">
```
Convert to standard markdown images. Remove `data-size`.

### Fix list markers
GitBook normalizes unordered lists to `*`. Mintlify convention uses `-`:
- `* item` → `- item`

### Remove GitBook-specific CSS classes
- `class="gitbook-drawing"` — remove
- `class="button primary"` — convert to `<Card>` or remove

### Fix heading hierarchy
GitBook pages often start with H1 (`# Title`). In Mintlify, the title comes from frontmatter. Remove the leading H1 and ensure content starts with H2 (`##`).

## Asset migration

1. Copy `.gitbook/assets/` contents to `/images/` (for images) and `/files/` (for PDFs, ZIPs, etc.)
2. Find-and-replace all relative asset paths:
   - `../.gitbook/assets/` → `/images/`
   - `.gitbook/assets/` → `/images/`
   - `../../.gitbook/assets/` → `/images/`
3. Rename files with spaces (GitBook allows `logo (1).png`) to kebab-case (`logo-1.png`)
4. Images max 5MB in Mintlify — check sizes
5. Rename `*.drawing.svg` files to remove `.drawing` suffix

## Validation

After migration, run:

```bash
mint validate        # Check for build errors
mint broken-links    # Verify all internal links work
mint dev             # Preview locally at localhost:3000
```

Common post-migration issues:
- Missing pages in `docs.json` navigation (pages won't appear in sidebar)
- Broken internal links (paths changed during migration)
- Unclosed JSX tags (MDX is stricter than plain Markdown)
- Unescaped `{`, `<`, `>` characters in prose (need escaping in MDX)
- Images with spaces in filenames (rename to kebab-case)

## Quick reference: Block conversion table

| GitBook syntax | Mintlify component |
|---|---|
| `{% hint style="info" %}` | `<Note>` |
| `{% hint style="success" %}` | `<Check>` |
| `{% hint style="warning" %}` | `<Warning>` |
| `{% hint style="danger" %}` | `<Danger>` |
| `{% tabs %}` / `{% tab title="..." %}` | `<Tabs>` / `<Tab title="...">` |
| `{% code title="..." %}` | `` ```lang filename `` |
| `{% code-tabs %}` (legacy) | `<CodeGroup>` |
| `<details>` / `<summary>` | `<Accordion title="...">` |
| `{% stepper %}` / `{% step %}` | `<Steps>` / `<Step title="...">` |
| `{% embed url="..." %}` | `<iframe>` or markdown link |
| `{% content-ref url="..." %}` | `<Card href="...">` or link |
| `{% page-ref page="..." %}` | Markdown link |
| `{% file src="..." %}` | Markdown link to `/files/` |
| `{% include "..." %}` | `import` + `<Snippet />` |
| `{% swagger %}` | `api:` frontmatter + `<ParamField>` |
| `{% openapi src="..." %}` | `openapi:` frontmatter |
| `<table data-view="cards">` | `<CardGroup>` / `<Card>` |
| `<figure>` / `<figcaption>` | `<Frame caption="...">` |
| `<img class="gitbook-drawing">` | `![alt](/images/file.svg)` |
| `$$ math $$` | `<Latex>math</Latex>` |
| `<mark style="color:...">` | `**bold**` or remove |
| `:emoji:&#x20;` | `:emoji:` |
| `GLOSSARY.md` | Dedicated page or `<Tooltip>` |
