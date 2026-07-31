<h1 align="center">Story-Driven Landing Pages</h1>

<p align="center">
  <strong>Build landing pages as product demonstrations—not decorative brochures.</strong>
</p>

<p align="center">
  <code>$build-story-driven-landing-page</code>
</p>

---

This skill is a reusable playbook for building **distinctive, evidence-led
landing pages** with the same level of intentionality as Proofjury—without
copying its branding, copy, assets, or signature visual identity.

It supports **React**, **Next.js**, and comparable frontend stacks.

## The core idea

Most landing-page builders start with a list of sections:

```text
Hero → Feature cards → Testimonials → Pricing → CTA
```

This skill starts with a product story:

```text
Audience → Existing behavior → Tension → Product intervention
         → Evidence → Outcome → CTA
```

| Typical landing page | Story-driven landing page |
|---|---|
| Starts with a layout template | Starts with product truth |
| Describes features | Demonstrates the mechanism |
| Uses motion as decoration | Uses motion to explain cause and effect |
| Makes broad claims | Places evidence beside each claim |
| Shrinks desktop for mobile | Designs mobile as its own experience |
| Treats a passing build as completion | Verifies the complete rendered story |

## What the skill does

- **Establishes product truth** before visual implementation.
- **Builds a narrative spine** from hook through proof and resolution.
- **Chooses the minimum viable motion level** instead of adding effects by
  default.
- **Creates a semantic visual system** for typography, surfaces, structure,
  emphasis, and evidence.
- **Implements maintainable scene architecture** in the existing frontend
  stack.
- **Requires real mobile and reduced-motion behavior.**
- **Verifies the experience** at critical scroll states, not only the hero and
  footer.

## The narrative spine

Use five to eight scenes, depending on what the product can honestly support:

| Scene | Purpose |
|---|---|
| **1. Hook** | Introduce one protagonist and one sharp promise. |
| **2. Momentum** | Show the existing workflow or pressure building. |
| **3. Tension** | Make the failure, cost, or gap concrete. |
| **4. Interruption** | Demonstrate the product changing the trajectory. |
| **5. Proof** | Show real output, evidence, or before-and-after behavior. |
| **6. Compounding value** | Explain memory, reuse, collaboration, or scale. |
| **7. Differentiation** | Show why the mechanism is structurally different. |
| **8. Resolution** | Present the desired outcome and conversion action. |

> Every scene answers one question and introduces at most one primary visual
> idea.

## Motion is a tool, not the idea

The skill selects the simplest motion tier that carries the story:

| Tier | Appropriate use |
|---|---|
| **Editorial** | Typography, layout, CSS transitions, and small reveals |
| **Cinematic DOM/SVG** | Selective pinning, scene timelines, paths, and decisive impacts |
| **Atmospheric WebGL** | One lightweight visual atmosphere connected to story state |

Continuous travel can follow scroll progress. Decisive moments—such as a
verdict, collision, snap, or success state—use short time-based animations at
explicit thresholds.

WebGL is optional. A weak product story does not become stronger because it has
a shader.

## What it refuses to produce

The skill actively pushes back against:

- unsupported metrics, customers, testimonials, or integrations;
- fake terminal output and decorative evidence;
- interchangeable feature-card grids;
- gradient headlines and glass panels used without product rationale;
- identical fade-up animation on every section;
- desktop timelines forced into hostile mobile layouts;
- inaccessible experiences that hide content without animation;
- copied reference-site branding or signature metaphors.

## Use it

Invoke the skill directly:

```text
Use $build-story-driven-landing-page to design and implement a distinctive,
scroll-driven landing page for my product.
```

It should also activate for requests such as:

```text
Build a landing page for my product.

Redesign this homepage so it does not look generic.

Create a cinematic, scroll-driven launch site.

Add stronger storytelling and motion to this Next.js landing page.
```

## What is included

| File | Role |
|---|---|
| [`SKILL.md`](SKILL.md) | Core operating rules and implementation workflow |
| [`references/story-system.md`](references/story-system.md) | Product truth, scene design, evidence, copy, and originality |
| [`references/motion-implementation.md`](references/motion-implementation.md) | GSAP, Lenis, SVG, theme transitions, WebGL, and cleanup |
| [`references/verification.md`](references/verification.md) | Viewport, accessibility, performance, conversion, and diff checks |
| [`agents/openai.yaml`](agents/openai.yaml) | Skill-list metadata and default invocation prompt |

## Completion standard

A successful production build is necessary, but it is not enough.

Before calling a landing page complete, the skill requires:

- lint, type, test, and production-build checks where available;
- desktop, mobile, and reduced-motion inspection;
- verification before, during, and after decisive scroll thresholds;
- keyboard, focus, overflow, console, CTA, and form-state checks;
- a final review for invented proof, copied identity, unused machinery, and
  unrelated changes.

The finished page should remain understandable when every animation is removed.
