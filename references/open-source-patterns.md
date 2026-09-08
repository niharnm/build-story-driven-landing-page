# Open-Source Reference Patterns

Use this catalog when the user supplies a reference site, asks for an uncommon
interaction, or needs a new motion direction. It is a study guide, not a parts
bin.

## Contents

1. Reference-study method
2. Product story and proof
3. Fail-open DOM motion
4. Scroll progress and timelines
5. Optional smooth scrolling
6. Shared WebGL
7. Isolated motion mechanics
8. Rejection gates

## 1. Reference-study method

Inspect the reference's source and live result when both are available. Create
this brief before adapting it:

| Source | Admired result | Underlying system | Product fit | Required correction | License and reuse limit |
| --- | --- | --- | --- | --- | --- |

Choose two to four compatible patterns. Do not assemble a page from unrelated
effects. Preserve the current product's identity, content, evidence, and stack.

For each live reference, check:

- desktop and narrow mobile composition;
- normal scrolling and restored mid-page scrolling;
- reduced motion and no-JavaScript content visibility;
- keyboard focus, headings, landmarks, and touch targets;
- console and network failures;
- CTA, form, download, and account destinations;
- drift between the deployed brand and the default branch.

Check the repository license before reusing code, assets, or copy. When a
license is missing, unclear, or incompatible, extract only general ideas and
write an original implementation.

## 2. Product story and proof

### Proofjury

[Proofjury at the audited commit](https://github.com/kevincui1034/proofjury/tree/2254e465c8a6aa23af895d514dcea23140ad84dd)
is a strong reference for carrying one product-native object through a complete
page. Its [product brief](https://github.com/kevincui1034/proofjury/blob/2254e465c8a6aa23af895d514dcea23140ad84dd/landing/PRODUCT.md#L7-L35)
defines the audience, mechanism, proof, tone, anti-references, motion, and
conversion before layout. The [route](https://github.com/kevincui1034/proofjury/blob/2254e465c8a6aa23af895d514dcea23140ad84dd/landing/app/page.tsx#L13-L55)
then moves a deploy command through focused scenes and places readable evidence
after the most controlled motion sequence.

Adapt:

- one native protagonist that changes state;
- one visitor question and one main visual idea per scene;
- evidence after tension and intervention;
- statically scoped visual chapters;
- continuous travel separated from short threshold-triggered impacts.

Correct:

- verify the deployed brand and commit, not only the local build;
- reject placeholder form endpoints and dead actions;
- cache geometry and batch DOM reads before writes;
- remove empty compact-scroll intervals;
- announce form results and provide practical touch targets.

GitHub reports no repository-level license for the audited landing source. Study
its structure, but do not copy its code, court identity, stamp, paper system,
copy, or assets without clear permission.

### OpenStatus

[OpenStatus](https://github.com/openstatusHQ/openstatus/tree/00da67be4e96facc5881aac781902f56acfd891f)
is a strong reference for a product-led page that does not depend on heavy
motion. Its [home content](https://github.com/openstatusHQ/openstatus/blob/00da67be4e96facc5881aac781902f56acfd891f/apps/web/src/content/pages/home.mdx#L34-L79)
connects a specific promise, price, real product image, customer proof,
mechanism, and no-signup demo in one readable sequence. Its
[FAQ](https://github.com/openstatusHQ/openstatus/blob/00da67be4e96facc5881aac781902f56acfd891f/apps/web/src/content/mdx-components/details.tsx#L5-L30)
uses native `details` and `summary` elements.

Adapt the evidence order and semantic restraint. OpenStatus is AGPL-3.0, so
check obligations before copying implementation code.

## 3. Fail-open DOM motion

[Satus](https://github.com/darkroomengineering/satus/tree/2c448ec22834090a35bd932d26cbd0e084e3b6bf)
is a strong engineering reference. Its [architecture guide](https://github.com/darkroomengineering/satus/blob/2c448ec22834090a35bd932d26cbd0e084e3b6bf/ARCHITECTURE.md#L81-L100)
makes motion opt-in and separates CSS reveals from GSAP work. Its
[`useReveal` hook](https://github.com/darkroomengineering/satus/blob/2c448ec22834090a35bd932d26cbd0e084e3b6bf/lib/hooks/use-reveal.ts#L94-L132)
keeps server-rendered content visible without JavaScript, avoids replaying a
late hydration entrance, honors reduced motion, and disconnects its observer.
Its [GSAP integration](https://github.com/darkroomengineering/satus/blob/2c448ec22834090a35bd932d26cbd0e084e3b6bf/components/effects/gsap.tsx#L83-L110)
scopes and reverts page-specific work.

Adapt fail-open content, route-level opt-in, scoped selectors, and complete
teardown. Satus is MIT licensed.

## 4. Scroll progress and timelines

[BSMNT Scrollytelling](https://github.com/basementstudio/scrollytelling/blob/0c26959b106d9e81931c30af7dfeebfd83d0a379/docs/pages/index.mdx#L17-L38)
models a scene as normalized progress from zero to one. Use that progress to
map explicit beat intervals instead of scattering viewport arithmetic across
components. Its image-sequence API is useful, but its
[eager preload implementation](https://github.com/basementstudio/scrollytelling/blob/0c26959b106d9e81931c30af7dfeebfd83d0a379/scrollytelling/src/image-sequence-canvas.tsx#L48-L114)
needs a bounded cache and cancellable loading before production use. The
repository's [license](https://github.com/basementstudio/scrollytelling/blob/0c26959b106d9e81931c30af7dfeebfd83d0a379/LICENSE)
is MIT for project-authored code, with bundled GSAP files governed by
GreenSock's standard license. Check the relevant file before reuse.

[Motion scroll documentation](https://motion.dev/docs/scroll) separates
scroll-linked values from triggered entrances. Use Motion values rather than
React state for hot progress. Define the target, container, and offsets
explicitly.

[GSAP React](https://github.com/greensock/react) is the reference for scoped
setup and context cleanup. Put one ScrollTrigger on a scene timeline rather
than one on every child tween. Use linear interpolation for scroll-linked
progress. Use eased time only for triggered events.

## 5. Optional smooth scrolling

[Lenis](https://github.com/darkroomengineering/lenis) is useful when the page
has a demonstrated need for one shared smooth-scroll layer. Keep native
scrolling by default. If Lenis is used, retain anchors and nested scrolling,
connect it to the existing frame clock, disable it for reduced motion, remove
its listeners, and call `destroy()` during teardown.

## 6. Shared WebGL

[r3f-scroll-rig](https://github.com/14islands/r3f-scroll-rig/tree/123663599e4b31af56f1845a19132d17e6a9b81f)
is the strongest reference here for DOM-aligned WebGL. It uses one
[global canvas with an error fallback](https://github.com/14islands/r3f-scroll-rig/blob/123663599e4b31af56f1845a19132d17e6a9b81f/src/components/GlobalCanvas.tsx#L84-L155),
tracks DOM bounds, and [hides offscreen scene content](https://github.com/14islands/r3f-scroll-rig/blob/123663599e4b31af56f1845a19132d17e6a9b81f/src/components/ScrollScene.tsx#L65-L108).
Its [texture hook](https://github.com/14islands/r3f-scroll-rig/blob/123663599e4b31af56f1845a19132d17e6a9b81f/src/hooks/useImageAsTexture.ts#L11-L22)
uses the DOM image's responsive `currentSrc` rather than loading an unrelated
graphics asset. The repository is MIT licensed.

Adapt the one-canvas model, DOM proxy elements, viewport gating, responsive
sources, and an explicit failure state. Keep meaningful content in semantic
HTML.

Proofjury's [small OGL stage](https://github.com/kevincui1034/proofjury/blob/2254e465c8a6aa23af895d514dcea23140ad84dd/landing/components/gl/stage.ts#L13-L98)
is a useful lower-cost reference: one triangle, capped pixel density, no
unnecessary antialiasing, one shared ticker, offscreen pause, and full context
cleanup.

## 7. Isolated motion mechanics

[Magic UI](https://github.com/magicuidesign/magicui/tree/1246d6d404c556f03867fc6d447f2867eee8a42b)
is useful for studying one effect at a time. Its
[scroll-velocity row](https://github.com/magicuidesign/magicui/blob/1246d6d404c556f03867fc6d447f2867eee8a42b/apps/www/registry/magicui/scroll-based-velocity.tsx#L91-L151)
measures with ResizeObserver, pauses offscreen and in hidden tabs, cleans up,
and [hides duplicated content](https://github.com/magicuidesign/magicui/blob/1246d6d404c556f03867fc6d447f2867eee8a42b/apps/www/registry/magicui/scroll-based-velocity.tsx#L180-L200)
from assistive technology.

Use it as a mechanic reference, not a page system. Its audited velocity effect
reduces amplification but retains base motion under reduced motion, so add a
true static state. The repository is MIT licensed.

## 8. Rejection gates

Reject or repair a reference pattern when it:

- leaves the first render blank until an intro ends;
- hides primary content until JavaScript initializes;
- lacks `header`, `main`, navigation, headings, or named controls;
- turns reduced motion into slower continuous motion instead of a static mode;
- creates a new frame loop, smooth-scroll owner, or WebGL canvas per section;
- reads layout after writing styles during the same frame;
- recalculates SVG geometry on every update;
- forces desktop pins, blank intervals, or horizontal tracks onto mobile;
- has placeholder actions, stale deployment content, or untested production
  routes;
- copies a brand system or signature interaction without a product reason.

The final design may be less animated than its references. Coherence,
readability, evidence, and reliable behavior take priority over effect count.
