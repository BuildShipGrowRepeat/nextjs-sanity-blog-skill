# Next.js + Sanity Blog (Claude Code skill)

An opinionated, batteries-included spec for adding a blog to a Next.js website backed by Sanity CMS. Built as a Claude Code skill: install it, say "add a blog", and the agent walks 40 intake questions, scans your project, drafts a one-page plan for your approval, and then implements against a ~1100-line technical spec that already covers SEO, i18n, performance, accessibility, AI hero image generation, and a pass/fail checklist.

Aimed at corporate blogs at the 50 to 500 post scale. Organic-search-first. Optional AI authoring with human review inside Sanity Studio.

## What you actually get

- A 40-question intake that covers every fork that meaningfully changes the spec: locales, author model, category count, CMS workflow, analytics, consent, AI imagery, comments, search, sharing, dark mode, scheduled publishing, and the rest.
- A one-page plan template the agent fills from your answers and stops at, waiting for explicit sign-off before any code change.
- A 20-section technical spec to implement against: Sanity schema, URL structure, smart 404 for missing-locale slugs, hreflang rules, BlogPosting and FAQPage JSON-LD, OG, Atom feeds, sitemap, performance budgets tighter than Google's "good" baseline, WCAG 2.2 AA targets, font and motion rules, deletion webhook handling.
- A working TypeScript generator for AI hero images via Gemini 3 Pro Image (Nano Banana Pro), with locale-keyed slugs, idempotent re-runs, and a per-project style guide template.
- A pass/fail checklist that is the definition of done.

## Install

Two ways.

**As a Claude Code plugin** (recommended):

```
/plugin install BuildShipGrowRepeat/nextjs-sanity-blog-skill
```

**Manual**:

Clone the repo and drop the skill folder into your local Claude skills directory.

```
git clone https://github.com/BuildShipGrowRepeat/nextjs-sanity-blog-skill.git
cp -R nextjs-sanity-blog-skill/skills/building-blog ~/.claude/skills/
```

## How to use it

Once installed, say one of:

- "add a blog to this project"
- "set up a blog with Sanity"
- "build the blog section"

Claude will:

1. Scan your project (`package.json`, `next.config.*`, message files, design tokens, `CLAUDE.md`, existing Sanity studio folder if any) and pre-fill anything it can detect.
2. Walk the 40 intake questions, showing recommended defaults so you can move quickly. The agent groups related questions and uses interactive picks where the host environment supports them.
3. Hand you a one-page implementation plan and wait for your sign-off.
4. Build against the spec, phase by phase, finishing on the pass/fail checklist.

## What's in the spec

Three files, each readable on its own:

- `skills/building-blog/SKILL.md` — the orchestrator. Workflow, scan checklist, fallbacks for non-interactive environments.
- `skills/building-blog/blog-technical-requirements.md` — the engineering spec. §0 holds the intake questionnaire, §1 is the per-project profile filled from the answers, §2 to §20 is the universal spec that reads from §1, §21 is the pass/fail checklist.
- `skills/building-blog/blog-image-style-guide.md` — a brand-tailorable template for AI-generated hero images. The intake sits on top, and the agent helps you populate the topic table and worked examples for your domain.

## Stack assumptions

- Next.js, App Router. Tested against 14 and 15; Next.js 16 gotchas are documented inline (async `params`, uncached `fetch`, Turbopack, `stega` outside draft mode).
- Sanity v3. Studio either hosted at `*.sanity.studio` or embedded under `/studio`.
- `next-intl` for i18n on multilingual projects. Single-locale projects skip the i18n section entirely.
- Tailwind is assumed but not strictly required. The spec locks Tailwind-style classes in a handful of typography rules only.

If your stack is meaningfully different (Contentful, Payload, MDX-only, Astro, Remix), this skill is the wrong tool for direct execution. The questionnaire structure and the SEO section still work as a checklist. The rest does not transfer cleanly.

## What this is not

- Not a docs site generator. Use Nextra, Docusaurus, or Starlight.
- Not for news publishers at high content velocity. Past ~1000 posts, sitemap chunking and editorial workflow become primary concerns and this spec gets thin.
- Not a marketing landing page builder dressed up as a blog.
- Not a UI library or design system. It assumes you already have one.

## Why this exists

Every time you ask an AI to "add a blog to my Next.js site", you get a slightly different answer. Some answers ship without alt text on hero images. Some include tags by default even though tags will fragment a 100-post archive into thin pages Google ignores. Some forget hreflang on listing pages. Some over-engineer with `@sanity/document-internationalization` when the site has 50 posts that don't even share topics across locales.

This skill is what a careful, opinionated implementation looks like, written down once so you don't relitigate it on every project. The opinions have rationale inline. Where you disagree, override via the §0 intake. That is exactly what §0 is for.

## Roadmap (loose)

- Stack adapters as sibling skills: Payload, Contentful, MDX-only.
- Better recommended defaults for FR / DE / ES / IT / PT locale combinations.
- A small examples folder showing the spec applied to a real project (sanitized).
- A short walkthrough video.

## Contributing

Issues and PRs welcome. The spec is opinionated on purpose. Specifically interested in:

- Real-world results: "I shipped a blog with this and here is what broke or what I had to change."
- Counter-examples where a default in §2 to §20 is provably wrong for a common case.
- Translations of the questionnaire to other languages so non-English-speaking teams can use it natively.

See `CONTRIBUTING.md` once added; in the meantime, open an issue first to discuss.

## License

MIT. See `LICENSE`.

## Author

Vladimir Terekhov · [BuildShipGrowRepeat](https://github.com/BuildShipGrowRepeat) · vv@attractgroup.com

---

Keywords for search: next.js sanity blog, claude code skill, claude skill, nextjs sanity cms, blog seo checklist, next-intl blog, nano banana blog images, gemini 3 pro image blog, sanity studio blog, hreflang next.js, blog jsonld blogposting, ai blog generator, opinionated blog spec.
