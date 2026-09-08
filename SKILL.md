---
name: build-story-driven-landing-page
description: Audit, design, implement, or refactor evidence-led product landing pages with product storytelling, scene sequencing, and purposeful scroll animation. Use for marketing homepages, launch sites, and conversion pages in React, Next.js, Astro, or static HTML/CSS/JS when product proof and responsive motion must work together. Do not use for dashboards, application screens, or components outside a marketing page.
---

# Build Story-Driven Landing Pages

Build an original product story, not a stack of fashionable sections. Make the
product's real mechanism visible, place proof beside claims, and use motion only
when it improves understanding.

## Select the scope

- **Audit or strategy:** inspect the current page, product evidence, and rendered
  behavior. Report findings and a proposed story without editing files.
- **Focused refactor:** preserve the current brand, page structure, conversion
  path, analytics, and working interactions. Change only the weak or affected
  scenes.
- **Full build:** establish product truth, plan the scene sequence, implement the
  page, and verify the rendered result.

Do not force a full rebuild onto a small request. Do not treat a dashboard,
application workflow, or component outside a marketing page as a landing-page
story.

## Load guidance only when needed

| Need | Read |
| --- | --- |
| New copy, a new metaphor, or reordered scenes | [references/story-system.md](references/story-system.md) |
| A supplied reference site or a new motion direction | [references/open-source-patterns.md](references/open-source-patterns.md) |
| Nontrivial scroll motion, GSAP, smooth scrolling, SVG paths, or WebGL | [references/motion-implementation.md](references/motion-implementation.md) |
| Audit work or final implementation checks | [references/verification.md](references/verification.md) |

For a full build, read the story and verification references. Read the motion
reference only if the selected tier needs it.

When the user supplies a reference site, inspect both its source and rendered
behavior when access permits. Record what works, why it works, what fits the
current product, and what must be corrected or rejected. Inspect desktop,
mobile, reduced motion, console output, and real action destinations. Check the
license before reusing code or assets.

## Full-build workflow

### 1. Establish product truth

Record:

- audience, traffic source, and decision context;
- what the visitor already knows and their main unresolved objection;
- single conversion goal;
- product promise and the mechanism that makes it credible;
- strongest real evidence and its source;
- one native object or idea that can carry the story;
- constraints such as the existing stack, brand system, static export, CMS,
  analytics, forms, and deployment.

Anchor every factual claim to repository content, supplied material, product
behavior, or an approved source. Never invent customers, metrics, integrations,
testimonials, command output, or technical proof.

Summarize the concept as:

> For [audience], move [protagonist] through [tension] to [verified outcome],
> prove it with [evidence], then ask for [conversion].

If a missing fact would materially change the result, ask one targeted
question. Otherwise state a conservative assumption and continue.

### 2. Plan only supported scenes

Use as many scenes as the product can honestly support. Do not pad the page to
reach a fixed count. Treat hook, existing behavior, tension, intervention,
proof, compounding value, differentiation, and resolution as a menu.

Before implementation, create a compact scene matrix:

| Scene | Visitor question | Claim and source | Evidence | Visual object | Motion purpose | Mobile fallback | Reduced-motion state | CTA relevance |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

Every scene answers one question and introduces at most one primary visual
idea. Remove any scene that repeats a claim or lacks useful proof.

### 3. Choose a motion tier

Choose the simplest tier that explains the story:

- **Editorial:** typography, layout, CSS transitions, and small local reveals.
- **DOM or SVG:** selective pinning, scrubbed diagrams, paths, and short
  threshold effects.
- **Atmospheric WebGL:** one lightweight visual atmosphere driven by the same
  story state as the document.

Reuse the repository's existing motion and scroll system. Prefer CSS or the Web
Animations API for simple transitions. Add a dependency only with approval.

For each nontrivial animation, record its comprehension purpose, input, start
and end states, reverse behavior, mobile fallback, reduced-motion state, and
cleanup owner. Remove animation with no clear explanatory purpose.

### 4. Define the visual grammar

Start from the existing brand and design system. Add only the missing semantic
roles for typography, surfaces, structure, emphasis, success, failure, spacing,
width, and evidence.

When the story changes visual state, update a small token set such as
`--surface`, `--ink`, `--body`, `--line`, and `--accent`; do not scatter one-off
theme classes across components.

Reject defaults that are not tied to the product:

- gradient headlines or decorative blobs;
- repeated glass cards;
- fake dashboards or terminal output;
- unsupported metric strips;
- interchangeable feature-icon grids;
- the same fade-up effect on every section;
- vague claims without a mechanism.

Reference sites may inform pacing, hierarchy, and interaction structure. Never
copy their identity, wording, assets, evidence, or signature metaphor.

### 5. Implement within the existing architecture

Follow the host repository's routing, component, styling, data, and animation
conventions. Split a scene into its own component only when its markup or
lifecycle benefits from isolation. Create a content module only when copy is
reused or complex enough to justify one.

- Keep meaningful final-state HTML present before client motion initializes.
- Keep navigation and conversion actions semantic and functional without
  animation.
- Use stable `data-*` hooks when motion or browser checks need them.
- Keep hot scroll values outside component render cycles.
- Own global scrolling, tickers, pointer state, and measurement refresh in one
  experience-level integration.
- Clean up timelines, listeners, observers, ticker callbacks, media queries,
  delayed work, and graphics contexts.

### 6. Design mobile and reduced motion as real modes

- Inspect at 375 CSS pixels or the product's smallest supported width.
- Replace hostile pins and horizontal tracks with natural document flow.
- Keep settled visuals inside the viewport and controls at practical touch
  sizes. Aim for a 44 by 44 CSS pixel hit area without inflating the visible
  control.
- Under `prefers-reduced-motion: reduce`, skip smooth scrolling, decorative
  WebGL, pins, typing, shaking, and continuous motion.
- Keep the complete story and every primary action visible with animation
  disabled or failed.

### 7. Complete the conversion path

Repeat the primary action only at meaningful decision points. Verify every
destination. If the page contains a form, implement and test loading, success,
error, disabled, repeat-submission, and no-JavaScript behavior as applicable.
Announce asynchronous results to assistive technology. Do not add form states
to pages without forms.

### 8. Verify the rendered story

Use [references/verification.md](references/verification.md). Run the
repository's relevant checks, inspect representative viewports and story
checkpoints, exercise keyboard and reduced-motion behavior, inspect console and
network output, and review the final diff.

Record each result as pass, fail, unverified, or not applicable with direct
evidence or a specific scope reason. A build or source inspection alone does
not prove rendered behavior, accessibility, or speed.

## Output contract

Before a full build, state the product-story assumption and a short plan. After
implementation, report:

- the story and visual system created;
- key files changed;
- desktop, mobile, and reduced-motion behavior;
- checks run with exact outcomes;
- measured speed or bundle changes when available;
- any external integration or behavior that remains unverified.

Keep the report specific to the product. Do not describe the result as a generic
modern landing page.
