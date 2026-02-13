# Mintlify Documentation Project

## Project Overview

This is a Mintlify documentation site. Pages are written in MDX (Markdown + JSX components). Configuration lives in `docs.json`.

## Commands

- `mint dev` — Start local dev server at http://localhost:3000
- `mint install` — Install dependencies
- `npx mint dev` — Alternative if `mint` is not globally installed

## Project Structure

```
/
├── docs.json          # Site configuration (navigation, theme, colors, logo)
├── index.mdx          # Landing page
├── quickstart.mdx     # Quickstart guide
├── essentials/        # Core documentation pages
├── api-reference/     # API documentation (if applicable)
└── images/            # Static images and logos
```

## Writing Conventions

- **File format:** MDX with YAML frontmatter (`title`, `description`)
- **Heading hierarchy:** Start content with h2 (`##`), never h1 (title comes from frontmatter)
- **Voice:** Second person ("you"), active voice, present tense
- **Navigation:** All pages must be listed in `docs.json` `navigation` to appear on the site

## Mintlify Components

Use these built-in components in MDX files:

- `<Note>` / `<Warning>` / `<Tip>` / `<Info>` — Callout boxes
- `<Steps>` + `<Step>` — Sequential instructions
- `<CodeGroup>` — Tabbed code examples for multiple languages
- `<Tabs>` + `<Tab>` — Tabbed content sections
- `<Card>` + `<CardGroup>` — Linked cards for navigation
- `<Accordion>` + `<AccordionGroup>` — Collapsible content
- `<Frame>` — Image wrapper with caption support
- `<ParamField>` / `<ResponseField>` — API parameter documentation
- `<RequestExample>` / `<ResponseExample>` — API code examples

## Configuration (`docs.json`)

- `$schema`: Always set to `"https://mintlify.com/docs.json"` for editor autocomplete
- `theme`: Visual theme (e.g., `"mint"`, `"maple"`)
- `colors.primary`: Brand color in hex
- `navigation`: Defines all site navigation — tabs, groups, and page references
- `logo`: Light/dark logo SVGs in `/images/`
- Page paths in navigation match file paths without the `.mdx` extension

## Key Rules

- Every MDX file needs frontmatter with at least `title` and `description`
- Internal links use relative paths without `.mdx` extension
- Images go in `/images/` and are referenced as `/images/filename.png`
- Code blocks must specify a language tag
- Run `mint dev` to preview changes locally before committing
