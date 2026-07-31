---
name: build-story-driven-landing-page
description: Design, implement, or refactor distinctive product landing pages using evidence-led storytelling, scene-based composition, restrained scroll choreography, semantic theme transitions, and production-quality responsive, accessible, and performant behavior. Use for landing pages, marketing homepages, launch sites, cinematic or scroll-driven product stories, Proofjury-style experiences, and requests for polished non-generic web UI in React, Next.js, or comparable frontend stacks.
---

# Build Story-Driven Landing Pages

Build an original product story rather than a collection of fashionable
sections. Borrow interaction systems from references, never their identity,
copy, assets, evidence, or signature metaphor.

## Operating rules

- Inspect repository instructions, the existing stack, product copy, routes,
  design tokens, and reusable components before editing.
- If the user requests analysis or critique only, report findings without
  changing files.
- If the user requests implementation, carry it through responsive behavior,
  reduced motion, form states, validation, and final diff review.
- If a reference repository or site is provided, inspect both source structure
  and rendered behavior when possible. Separate verified behavior from
  inference.
- Preserve existing architecture and dependencies unless the story genuinely
  needs a different approach. Ask before adding a production dependency.
- Write product-specific copy from verified facts. Never invent customers,
  metrics, integrations, testimonials, command output, or technical proof.
- Keep the result original. Do not reproduce Proofjury's courtroom, gate,
  rubber-stamp, amber-light, or paper-record combination unless the user is
  deliberately working on that brand.

## Required workflow

### 1. Establish product truth

Identify:

- audience and their decision context;
- single conversion goal;
- product promise;
- concrete mechanism that makes the promise credible;
- strongest real evidence available;
- one object or idea that can act as the page's protagonist;
- constraints such as static export, CMS, analytics, forms, or deployment.

Do not begin visual implementation until the page can be summarized as:

> For [audience], move [protagonist] through [tension] to [verified outcome],
> proving it with [evidence], then ask for [conversion].

When the product is underspecified, inspect the repository and make conservative
assumptions. Ask one targeted question only if a missing answer would materially
change the page.

### 2. Write the narrative spine

Use five to eight scenes. Adapt this sequence rather than treating it as a
mandatory template:

1. **Hook** — introduce the protagonist and one sharp promise.
2. **Momentum** — show the existing workflow or pressure building.
3. **Tension** — make the failure, cost, or gap concrete.
4. **Interruption** — demonstrate the product changing the trajectory.
5. **Proof** — show receipts, output, before/after behavior, or mechanism.
6. **Compounding value** — explain memory, scale, collaboration, or reuse.
7. **Differentiation** — state why the mechanism is structurally different.
8. **Resolution** — show the desired outcome and present the CTA.

Every scene must answer one question and introduce at most one primary visual
idea. Read [references/story-system.md](references/story-system.md) before
writing scene copy or choosing a metaphor.

### 3. Choose the minimum viable motion tier

Choose the simplest tier that carries the story:

- **Editorial:** strong typography, layout, CSS transitions, and small reveals.
- **Cinematic DOM/SVG:** scene timelines, selective pinning, scrubbed diagrams,
  and one or two time-based impacts.
- **Atmospheric WebGL:** one lightweight shader or 3D stage that responds to the
  same story state as the DOM.

Do not use WebGL to compensate for weak structure. Do not animate every
element. Motion must communicate travel, causality, interruption, state change,
or hierarchy.

### 4. Define the visual grammar

Create a small semantic system:

- two or three typography roles;
- one surface system;
- one structural line system;
- one emphasis color;
- semantic success and failure colors;
- a spacing and width rhythm;
- a distinct visual treatment for evidence.

If the story changes state, define worlds with semantic tokens such as
`--surface`, `--ink`, `--body`, `--line`, and `--accent`. Change token values,
not every component class.

Avoid generic landing-page defaults unless the product specifically calls for
them:

- purple gradient blobs;
- gradient headline text;
- repeated glass cards;
- fake dashboard screenshots;
- unsupported metric strips;
- interchangeable feature-icon grids;
- motion that consists only of identical fade-ups;
- vague copy such as "reimagine," "unlock," or "transform" without a mechanism.

### 5. Implement a scene architecture

Keep the route composition simple. Prefer:

```text
app/page.tsx
app/globals.css
lib/story.ts
components/experience/
components/scenes/
components/ui/
```

- Keep verified copy and evidence in a typed content module.
- Give each scene one component and one scoped motion context.
- Use stable `data-scene` and `data-*` hooks for animation and verification.
- Keep global scrolling, tickers, pointer state, and font refresh logic in one
  experience root.
- Keep navigation and CTAs semantic and functional without animation.
- Render meaningful final-state HTML before client motion initializes.

Read [references/motion-implementation.md](references/motion-implementation.md)
when using GSAP, smooth scrolling, SVG path motion, world transitions, or
WebGL.

### 6. Choreograph cause and effect

Separate motion by purpose:

- Map continuous travel and reveals to scroll progress.
- Trigger impacts, stamps, verdicts, snaps, and other decisive moments as
  short time-based animations at explicit thresholds.
- Pin only when the scene needs controlled reading time.
- Return to normal document flow after an intense sequence.
- Let one protagonist, line, light, or state travel across scenes to create
  continuity.
- Give decorative motion less energy than story motion.
- Keep scroll-path state outside React rendering.

Ensure cleanup for every timeline, listener, ticker, observer, media query, and
graphics context.

### 7. Design mobile and reduced motion intentionally

- Treat 375 px as a real layout, not a shrunken desktop.
- Replace complex pinned tracks with natural flow when space or scroll length
  becomes hostile.
- Keep decisive visuals inside the viewport after their animation settles.
- Use fluid type with bounded sizes and readable line lengths.
- Make touch targets at least 44 CSS pixels where practical.
- Under `prefers-reduced-motion: reduce`, do not instantiate smooth scrolling
  or decorative WebGL. Remove pins, typing, shaking, and continuous motion.
- Ensure the reduced-motion document reads correctly from top to bottom with
  all important content visible.

### 8. Finish the conversion path

- Repeat the primary CTA only at meaningful decision points.
- Make external destinations, form endpoints, and no-JavaScript behavior real.
- Include loading, success, error, disabled, and fallback states for forms.
- Do not ship placeholder form IDs, dead buttons, or fake interactive controls.
- Keep the final CTA a resolution of the narrative, not an unrelated banner.

### 9. Verify the complete story

Read [references/verification.md](references/verification.md), then:

- run the relevant lint, type, test, and production-build commands;
- inspect desktop, mobile, and reduced-motion rendering;
- inspect key scroll thresholds rather than only the top and bottom;
- check console errors, horizontal overflow, focus visibility, and CTA/form
  states;
- review the final diff for accidental scope, copied identity, invented proof,
  and unused machinery.

Do not claim the page is complete from a successful build alone.

## Output contract

Before meaningful edits, state the narrative assumption and a short plan.

After implementation, report:

- the story and visual system created;
- key files changed;
- behavior at desktop, mobile, and reduced motion;
- checks run with exact outcomes;
- any unverified external integration or remaining blocker.

Keep the explanation specific to the product. Do not describe a generic
"modern landing page."
