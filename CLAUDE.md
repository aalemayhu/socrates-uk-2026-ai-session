# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file [reveal.js](https://revealjs.com) slide deck: **"Programming the agent — the .claude setup behind 2anki"**. The talk walks through how the 2anki/server repo programs Claude Code via `.claude/` files (rules, agents, commands, skills, hooks). This repo is *only* the presentation, not the 2anki codebase it describes.

## Run / preview

No build, no package manager, no tests. Vendored deps only.

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

Open over HTTP, not `file://` — reveal.js uses `hash: true` routing and loads `vendor/` assets relative to the page.

## Structure

- `index.html` — the entire deck: inline `<style>` design system + all slides as `<section>` elements + `Reveal.initialize(...)` at the bottom. Everything lives here.
- `vendor/reveal.js`, `vendor/reveal.css` — pinned reveal.js 5.1.0 (minified). Do not hand-edit; replace wholesale to upgrade.
- `assets/trio-flow.svg` — the kaizen-loop diagram on the trio slide.

## Editing slides

- Each slide is a `<section>`. Section dividers use `class="sec"`; the title slide uses `class="title-slide"`. Add a new slide by inserting a `<section>` in document order — reveal.js orders by DOM position.
- All styling is the CSS in `<head>`. Reuse existing classes (`.cards .cols-N` grid, `.card`, `.chip[.blue/.green/.pink/.amber]`, `.code` with `.c` comment / `.b` bold spans, `.foot`, `.eyebrow`, `.stat-card`/`.statnum`). Don't add inline ad-hoc styling when a class exists.
- Fixed canvas is `1280×720` (set in both `Reveal.initialize` and the `section` height). Content must fit one screen — there is no scroll. Section dividers and the title set `data-slide-number="false"` to drop the page number.
- `:root` CSS vars (`--ink`, `--gray`, `--line`, accent `--blue/--green/--pink/--amber`, `--mono`, `--serif`) are the palette. Change a color there, not per-rule.

## Content accuracy

The deck quotes specific counts from the 2anki `.claude/` setup (10 rules, 13 agents, 18 commands, 7 skills, 14 hooks). These appear in multiple slides (title agenda, anatomy 1.2, by-the-numbers 1.3). If one count changes, update every occurrence so the deck stays consistent.
