<h1 align="center">Story-Driven Landing Pages</h1>

<p align="center">
  <strong>Turn real product mechanics and proof into a landing page people can follow.</strong>
</p>

<p align="center">
  <a href="https://skills.sh/niharnm/build-story-driven-landing-page/build-story-driven-landing-page">
    <img src="https://skills.sh/b/niharnm/build-story-driven-landing-page" alt="skills.sh installs">
  </a>
</p>

An Agent Skill for designing, building, or refactoring product landing pages
whose copy, layout, motion, and conversion path tell one coherent story. It is
made for React, Next.js, Astro, static HTML/CSS/JS, and comparable web stacks,
while following the host repository's existing architecture and design system.

The skill starts from product truth, connects every claim to evidence, and uses
animation only when it explains cause, state, or progress. It does not generate
a dressed-up section template.

## Install

```bash
npx skills add niharnm/build-story-driven-landing-page \
  --skill build-story-driven-landing-page
```

Then ask your agent:

```text
Use $build-story-driven-landing-page to turn my product's real mechanism and
proof into a responsive landing page with purposeful motion.
```

[View the skill on skills.sh](https://skills.sh/niharnm/build-story-driven-landing-page/build-story-driven-landing-page)

## When it fits

Use it for:

- a new product landing page or marketing homepage;
- a launch site that must explain an unfamiliar mechanism;
- a generic homepage that needs a stronger story and clearer proof;
- a scroll-directed product demonstration;
- an audit of a marketing page's story, proof, motion, mobile behavior, or
  conversion path;
- a focused refactor of weak scenes, motion, mobile behavior, or conversion.

Do not use it for dashboards, application screens, or components outside a
marketing page.

## The core idea

Most landing-page generators start with a section list:

```text
Hero -> feature cards -> testimonials -> pricing -> CTA
```

This skill starts with a product decision:

```text
Audience -> existing behavior -> tension -> product intervention
         -> real proof -> outcome -> CTA
```

| Typical generated page | Story-driven page |
| --- | --- |
| Starts from a layout pattern | Starts from product truth and visitor context |
| Describes features | Demonstrates the product mechanism |
| Adds motion for decoration | Uses motion to explain cause and state |
| Separates claims from proof | Places evidence beside each claim |
| Shrinks desktop for mobile | Gives compact and reduced-motion modes their own behavior |
| Stops after a passing build | Inspects the complete rendered story |

## What the skill makes the agent do

1. **Choose the right scope.** Audit, focused refactor, and full-build requests
   do not receive the same amount of work.
2. **Write a product-truth brief.** Audience, traffic source, objection,
   mechanism, proof, and conversion are explicit before layout begins.
3. **Plan a sourced scene sequence.** Every scene records its visitor question,
   claim source, evidence, visual object, motion purpose, and static fallback.
4. **Use the simplest useful motion tier.** CSS, DOM or SVG timelines, and
   optional WebGL are choices, not defaults.
5. **Verify what shipped.** Desktop, mobile, reduced motion, keyboard behavior,
   console output, conversion paths, and measured speed are checked with direct
   evidence when the environment permits it.

## Proofjury as a reference

[Proofjury](https://github.com/kevincui1034/proofjury) is one benchmark for the
method. Its landing page makes a deploy command the protagonist, builds pressure
through concrete failure evidence, stages the product's intervention, changes
visual worlds at the verdict, and ends with the successful state.

The transferable lesson is not its courtroom identity. It is the alignment of
product mechanism, evidence, visual hierarchy, and motion energy. The skill
explicitly prevents copying a reference site's branding, wording, assets, or
signature metaphor.

See [open-source reference patterns](references/open-source-patterns.md) for a
broader set of implementation sources and the rules extracted from them.

## Motion tiers

| Tier | Use |
| --- | --- |
| **Editorial** | Typography, composition, CSS transitions, and small local reveals |
| **DOM or SVG** | Selective pinning, scene timelines, paths, and decisive threshold effects |
| **Atmospheric WebGL** | One lightweight visual atmosphere connected to the same story state |

Continuous motion can follow scroll progress. A decisive event, such as a
collision, verdict, snap, merge, or success state, should be a short time-based
effect at an explicit threshold. The distinction keeps the event legible at
different scroll speeds.

WebGL is optional. It does not repair a weak product story.

## What it refuses to make

- unsupported metrics, customers, testimonials, or integrations;
- fake terminal output or decorative evidence;
- interchangeable feature-card grids;
- copied reference-site identity;
- the same fade-up animation on every section;
- desktop pins forced into a poor mobile layout;
- content hidden when animation fails or reduced motion is enabled;
- placeholder form IDs, dead links, or fake controls.

## Included guidance

| File | Role |
| --- | --- |
| [`SKILL.md`](SKILL.md) | Scope routing, constraints, and the full-build workflow |
| [`references/story-system.md`](references/story-system.md) | Product truth, scene planning, evidence, copy, and originality |
| [`references/motion-implementation.md`](references/motion-implementation.md) | Library choice, responsive motion, scroll timing, SVG, media, and optional WebGL |
| [`references/open-source-patterns.md`](references/open-source-patterns.md) | Source-backed patterns from strong public implementations |
| [`references/verification.md`](references/verification.md) | Browser evidence, accessibility, speed, conversion, and diff checks |
| [`agents/openai.yaml`](agents/openai.yaml) | Skill-list metadata and default prompt |

## Completion standard

A production build is necessary when the project provides one, but it is not
enough. The agent must also inspect representative viewports, key scroll states,
reduced-motion output, keyboard focus, console and network output, real action
destinations, and the final diff. Every result is reported as pass, fail,
unverified, or not applicable, with evidence or a specific scope reason.

The page must remain understandable when every animation is removed.
