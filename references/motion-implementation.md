# Motion Implementation

## Contents

1. Architecture
2. Responsive motion contexts
3. Scroll versus time
4. Smooth scrolling
5. Scene hooks and cleanup
6. Theme transitions
7. SVG motion
8. WebGL atmosphere
9. Common failure modes

## 1. Architecture

Keep the route server-renderable and move motion into scoped client scenes.

```tsx
export default function Page() {
  return (
    <>
      <Nav />
      <ExperienceRoot />
      <main>
        <HookScene />
        <MomentumScene />
        <InterruptionScene />
        <ProofScene />
        <ResolutionScene />
      </main>
    </>
  );
}
```

Render final-state semantic markup. Inside layout-safe effects, set animated
initial states before the browser paints where the framework permits.

Keep:

- copy in a typed content module;
- scene animation inside the scene;
- global ticker and scrolling integration inside one root;
- hot scroll-path values in a mutable store rather than React state.

## 2. Responsive motion contexts

Use explicit full, compact, and reduced-motion contexts.

```ts
export const MQ = {
  full: "(min-width: 800px) and (prefers-reduced-motion: no-preference)",
  compact: "(max-width: 799.98px) and (prefers-reduced-motion: no-preference)",
  static: "(prefers-reduced-motion: reduce)",
} as const;
```

Do not rely on desktop timelines automatically fitting mobile. For compact
layouts:

- shorten or remove pins;
- prefer natural document flow;
- reveal sections locally;
- reduce travel distance and shake amplitude;
- confirm large overlays settle inside 375 px.

For static mode, create no timelines unless a tiny non-motion state correction
is essential.

## 3. Scroll versus time

Use scroll for continuous causality:

- travel;
- drawing paths;
- progressive comparison;
- entering or leaving a scene;
- theme-transition coverage.

Use time for decisive impacts:

- verdict;
- snap;
- stamp;
- success state;
- short shake;
- one-time reveal after a threshold.

A threshold-triggered impact remains legible even when the user scrolls quickly.
Track threshold crossings in the scrub timeline's update callback and reverse
the effect when the user crosses backward if reversibility matters.

Do not encode a sharp impact as two percent of a scrubbed timeline; it will feel
weak at slow speed and disappear at fast speed.

## 4. Smooth scrolling

If using Lenis with GSAP, run it from GSAP's ticker rather than creating another
animation loop:

```ts
const lenis = new Lenis({ autoRaf: false, anchors: true });
const raf = (seconds: number) => lenis.raf(seconds * 1000);

lenis.on("scroll", ScrollTrigger.update);
gsap.ticker.add(raf);
gsap.ticker.lagSmoothing(0);
```

Destroy Lenis and remove the ticker callback during cleanup. Do not instantiate
smooth scrolling under reduced motion.

Smooth scrolling is optional. Omit it when native scrolling already supports
the interaction or when the host application has its own scroll manager.

## 5. Scene hooks and cleanup

Scope selectors to the scene root and use stable data attributes.

```tsx
const ref = useRef<HTMLElement>(null);

useGSAP(() => {
  const root = ref.current!;
  const item = root.querySelector<HTMLElement>('[data-scene="item"]')!;
  const mm = gsap.matchMedia();

  mm.add(MQ.full, () => {
    const timeline = gsap.timeline({
      scrollTrigger: {
        trigger: root,
        start: "top top",
        end: "+=120%",
        pin: true,
        scrub: 0.7,
        invalidateOnRefresh: true,
      },
    });
    timeline.from(item, { autoAlpha: 0, y: 24 });
  });

  return () => mm.revert();
}, { scope: ref });
```

Clean up:

- match-media contexts;
- GSAP timelines and ScrollTriggers;
- pointer and resize listeners;
- ticker callbacks;
- IntersectionObservers;
- dynamically created canvases and graphics contexts.

After web fonts load, refresh measurements when split text, pins, or viewport
alignment depend on final font metrics.

## 6. Theme transitions

Define semantic tokens for each world:

```css
:root,
[data-world="night"] {
  --surface: #0b0e13;
  --ink: #f2f4f7;
  --body: #a8b0bd;
  --line: #252c37;
  --accent: #e9b949;
}

[data-world="paper"] {
  --surface: #f1ecdd;
  --ink: #20242c;
  --body: #424a57;
  --line: #d1c9b3;
  --accent: #7a5710;
}
```

Scope chapter wrappers statically so the document remains correct without
JavaScript. Flip the root world only for fixed chrome.

To avoid a flash:

1. Expand an opaque transition layer until it fully covers the viewport.
2. Flip the root token scope behind the cover.
3. Continue into the new statically scoped chapter.
4. Reset the root world during timeline cleanup.

Use the exact destination surface color for the cover.

## 7. SVG motion

Prefer SVG for diagrams, paths, gates, seals, and connectors.

- Draw paths using measured length or normalized `pathLength="1"`.
- Move glyphs with `getPointAtLength`.
- Use deterministic coordinates and tilts.
- Keep important text in the DOM; treat decorative SVG as `aria-hidden`.
- Test stretched view boxes because dash behavior can change.

When CSS centering and GSAP both need transforms, let GSAP own centering with
`xPercent` or `yPercent` so an `x` or `y` tween does not clobber it.

## 8. WebGL atmosphere

Use WebGL only after the CSS and DOM experience works.

Prefer:

- one fullscreen triangle;
- one fragment shader;
- no antialiasing when unnecessary;
- capped device-pixel ratio;
- lazy dynamic import;
- idle initialization;
- CSS fallback;
- rendering only while visible;
- a shared ticker;
- pointer input that is lerped rather than direct.

Keep the canvas decorative and `aria-hidden`. Never hide meaningful content
inside a shader.

Do not create WebGL under reduced motion. If context creation fails, keep the
CSS fallback visible.

## 9. Common failure modes

- **Pin jump after mobile URL-bar resize:** ignore non-dimensional mobile
  resizes or configure the scroll library appropriately.
- **Horizontal overflow:** use `overflow-x: clip`; avoid `hidden` when it breaks
  sticky positioning.
- **Split text reflow:** disable text balancing before splitting and revert the
  split after entrance.
- **Refresh changes state:** make threshold logic idempotent and reversible.
- **Animation flashes on load:** keep SSR markup meaningful and set initial
  states in the earliest framework-safe scoped effect.
- **Multiple animation loops:** drive smooth scrolling, DOM timelines, and
  decorative rendering from one ticker.
- **Scroll causes React renders:** move hot values to mutable objects or direct
  animation-library state.
- **Static export form fails:** use a real external form endpoint with loading,
  success, error, honeypot, and no-JavaScript fallback behavior.
