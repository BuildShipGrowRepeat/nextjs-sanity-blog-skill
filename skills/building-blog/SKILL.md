---
name: building-blog
description: Use when adding a blog to a Next.js + Sanity site, building a blog section from scratch, integrating Sanity CMS for editorial content, or setting up an SEO-optimized article surface. Triggers on phrases like "add a blog", "build the blog", "create blog section", "set up blog with Sanity", "integrate Sanity CMS", "blog architecture", or any new-blog scoping conversation on a Next.js project.
---

# Building a Blog (Next.js + Sanity)

## Overview

Universal workflow for adding a blog to a Next.js site backed by Sanity CMS. Targets a corporate blog: SEO-first, i18n-ready, performance-budgeted, accessibility-compliant.

**SKILL.md is the orchestrator. The spec lives in the two reference files.**

## Files

- `blog-technical-requirements.md` — §0 intake questionnaire (30+ questions) → §1 Project Profile → §2–§20 universal spec → checklist. Edit only §0 answers and §1 per project.
- `blog-image-style-guide.md` — universal template for AI-generated hero imagery via Gemini 3 Pro Image (Nano Banana Pro). Intake questions on top, aesthetic skeleton in the middle, three example slots at the bottom.

## Workflow

### Step 1 — Scan the host project (before asking anything)

Read what's already there. Pre-filling answers from detected values is much better than asking the user. Look for:

- `package.json` — Next.js version, `next-intl`, Sanity packages, Tailwind, `framer-motion`
- `next.config.{ts,js,mjs}` — existing `images.formats`, i18n config
- `src/messages/**`, `src/i18n/**`, `messages/**` — current locale set
- `src/app/[locale]/**` or `app/[locale]/**` — routing pattern
- `tailwind.config.*`, `globals.css`, design-system files — tokens, fonts
- `CLAUDE.md`, `AGENTS.md`, `GEMINI.md` — project conventions and approved overrides
- Existing `sanity-studio/` or `studio/` folder
- `app/layout.{tsx,jsx}` — fonts, analytics, motion config
- `public/brand/**`, `public/logo*` — publisher logo
- `sitemap.ts`, `robots.ts` — existing routes
- `.env*` files — names of already-set env vars (do not log secret values)

Record findings as a brief "Detected" list before the questionnaire.

### Step 1.5 — Fetch the latest docs for the stack you'll touch

Spec opinions can drift from upstream reality. Before implementing, pull current docs for the libraries you will actually use on this project. Do not skip this — the spec was last audited at a fixed point in time, and Next.js / Sanity / next-intl ship breaking changes more often than this skill is updated.

Use [`context7`](https://context7.com) if it is available in the environment (it is the fastest way to read current library docs); otherwise fall back to the library's official docs site via `WebFetch`. Cross-check against the spec when you reach the matching section.

Minimum docs to read for any blog build:

- **Next.js** — App Router, `generateStaticParams`, `generateMetadata`, dynamic `params` (sync vs Promise in 15/16), image config, `revalidateTag`, `unstable_cache` deprecation status
- **Sanity v3** (`@sanity/client`, `next-sanity`) — `client.fetch` options, draft mode + `stega` rules, `defineQuery`, GROQ projection patterns, image URL builder
- **next-intl** (only if multi-locale) — App Router setup, `getTranslations`, `getMessages`, `setRequestLocale`, hreflang patterns
- **@portabletext/react** — current component override API, plugin packages
- **@sanity/image-url** — params, hotspot/crop behaviour, `auto=format`

Also check, just-in-time, when you hit the matching spec section:

- **Hero image generator** — Gemini 3 Pro Image (Nano Banana Pro) — current model name, image generation endpoint, supported sizes/aspect ratios, JSON schema for `responseModalities`
- **JSON-LD** — Google's [Article structured data](https://developers.google.com/search/docs/appearance/structured-data/article) page for current required fields
- **CWV thresholds** — `web.dev` Core Web Vitals page for current LCP/INP/CLS "good" cutoffs

If the docs contradict the spec, the docs win. Note the contradiction in the project profile (§1) and proceed against the docs.

### Step 2 — Run the intake questionnaire

Open `blog-technical-requirements.md` and walk through §0.

- **Claude Code:** use `AskUserQuestion`. Group related questions into single calls (max 4 per call). Pre-fill recommended answers from the scan.
- **Codex / CLIs without an interactive picker:** list questions numerically in plain text, ask the user to answer in batches of 5–10. Show recommended answers from the scan.
- **Headless / non-interactive:** apply universal defaults to whatever the prompt did not explicitly cover; list every assumption.

Write the answers into §1 "Project Profile" (in a project-local copy under `docs/blog/`, not in the universal source).

### Step 3 — Produce the high-level plan

Use the plan template at the end of §0. One page. Phases, locked-in scope, out-of-scope items, open decisions. **Wait for explicit user approval. Do not start coding.**

### Step 4 — Implement against the spec

Follow §2–§20 in order. §19 (Pass/Fail Checklist) is the definition of done. The image style guide drives §20 if AI-generated hero images are in scope.

## When NOT to use this skill

- Static / MDX-only blogs (no CMS) — different stack, different patterns
- High-velocity news publishers — sitemap chunking and editor tooling become primary concerns
- Documentation sites — use a docs framework instead
- Marketing landing pages that aren't really a blog

## Recommended companion skills

- `frontend-design` — if the visual identity is unclear or the site is mid-greenfield, brainstorm direction first
- `superpowers:brainstorming` — for scope conversations beyond what §0 captures
- `superpowers:writing-plans` — to expand the high-level plan into a per-phase implementation plan before coding
