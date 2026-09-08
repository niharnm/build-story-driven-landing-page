# Verification

## Contents

1. Evidence record
2. Required automated checks
3. Viewport matrix
4. Story checkpoints
5. Accessibility
6. Performance and resilience
7. Content and conversion
8. Final diff review

## 1. Evidence record

For an audit or implementation, record what was actually inspected:

| Check | Surface or viewport | State | Direct evidence | Result | Blocker |
| --- | --- | --- | --- | --- | --- |

Use `pass`, `fail`, `unverified`, or `not applicable`. Every not-applicable
result needs a specific scope or product reason. A command result, browser
observation, screenshot, console or network record, or measured artifact is
direct evidence. Source inspection can prove code structure, but it cannot
prove rendered behavior, keyboard operation, accessibility, or runtime speed.

Capture pre-change evidence for any behavior the work intends to improve, then
repeat the same check under comparable conditions after the change.

## 2. Required automated checks

Run the repository's available equivalents of:

```text
lint
typecheck
unit or component tests
production build
```

Do not install or run broad fix commands merely to make checks green. Report
pre-existing failures separately from changes introduced by the task.

For static-export sites, confirm the route is emitted as static content and
that required runtime features do not depend on unavailable server routes.

## 3. Viewport matrix

At minimum inspect:

| Mode | Suggested viewport | What to verify |
|---|---:|---|
| Desktop | 1280 × 720 | pins, typography, fixed chrome, scene transitions |
| Tall desktop | 1440 × 900 | pacing and excess empty space |
| Mobile | 375 × 812 | wrapping, overlays, natural-flow fallbacks |
| Mobile wide | 390 × 844 | breakpoint stability and CTA/form layout |
| Reduced motion | desktop and mobile | no pins, canvas, shakes, or hidden content |

If the product targets a known device class, add its real viewport.

Check `documentElement.scrollWidth <= innerWidth` at every representative
viewport.

## 4. Story checkpoints

Do not verify only the hero and footer. Inspect every checkpoint that exists in
the selected motion tier and scope. Mark the others not applicable with a
specific reason. Inspect screenshots or live state at:

1. hero after entrance settles;
2. first continuous-scroll scene at mid-progress;
3. tension or evidence scene with partial disclosure;
4. the frame immediately before the decisive threshold;
5. the decisive effect after it settles;
6. the opaque world transition at full cover;
7. the first frame after the transition;
8. a proof artifact in its fully readable state;
9. the final CTA and all form states.

Scroll forward and backward across each discrete threshold that exists. For
pages with root theme changes, overlays, or shared state, confirm they do not
become stranded.

## 5. Accessibility

Confirm:

- exactly one meaningful `h1`;
- logical heading order;
- skip link or equivalent main-content navigation;
- visible keyboard focus;
- semantic links, buttons, forms, labels, and lists;
- important text remains DOM text;
- decorative canvas and SVG are `aria-hidden`;
- body text contrast meets WCAG AA;
- color is not the only signal for success or failure;
- touch targets are practical on mobile;
- primary navigation and conversion controls provide about 44 by 44 CSS pixels
  of hit area where the layout permits it;
- reduced-motion mode contains the complete story;
- no focusable control is hidden behind fixed chrome.

Keyboard-test all interactive controls. Do not infer accessibility from markup
alone.

## 6. Performance and resilience

Confirm:

- no console errors or repeated warnings;
- no duplicate requestAnimationFrame loops;
- graphics rendering pauses offscreen or when the document is hidden;
- WebGL is lazy and has a CSS fallback;
- device-pixel ratio is capped;
- scroll updates do not trigger React renders;
- listeners, observers, tickers, and contexts are cleaned up;
- font loading does not leave ScrollTrigger measurements stale;
- page content remains meaningful if animation initialization fails.
- image dimensions and responsive sources prevent layout shifts;
- below-fold media loads lazily and video pauses when it is not visible;
- motion media has a representative static state for reduced motion and failed
  playback.

Inspect the production bundle when adding a large motion or graphics
dependency. A visually impressive hero does not justify loading unused
libraries on every route.

When a runnable page and suitable tools exist, record:

- device, viewport, browser, cache state, and network or CPU conditions;
- LCP, CLS, and INP from comparable runs where those metrics are meaningful;
- transferred bytes and route-level bundle changes;
- long tasks or main-thread work introduced by scroll and media behavior.

Use repeat runs or a representative trace when results are noisy. Do not claim
a speed improvement from source inspection, a build result, or one unmatched
measurement.

## 7. Content and conversion

Confirm:

- claims match repository or product evidence;
- example output is real or clearly labeled as illustrative;
- CTAs point to real destinations;
- external links use safe target attributes;
- form endpoints and IDs are configured;
- form loading, success, error, disabled, and fallback states work;
- form success and error updates are announced to assistive technology;
- the same conversion action is not repeated excessively;
- metadata title and description match the current product;
- the deployed brand, main CTA, form action, and expected commit match the
  release being verified;
- copyright, license, and dates are accurate.

Never submit real user data during verification without explicit authorization.
Use local or test values only when submission has been authorized.

## 8. Final diff review

Review for:

- copied brand language or signature visual identity;
- unused components, content, CSS utilities, uniforms, or scripts;
- accidental dependency or lockfile changes;
- magic timing values with no scene rationale;
- hard-coded coordinates that break compact layouts;
- selectors coupled to brittle DOM order;
- missing cleanup;
- placeholder integration values;
- unrelated edits.

End with a factual summary of what was verified and what remains external,
physical-device-only, or untested.
