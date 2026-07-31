# Verification

## Contents

1. Required automated checks
2. Viewport matrix
3. Story checkpoints
4. Accessibility
5. Performance and resilience
6. Content and conversion
7. Final diff review

## 1. Required automated checks

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

## 2. Viewport matrix

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

## 3. Story checkpoints

Do not verify only the hero and footer. Inspect screenshots or live state at:

1. hero after entrance settles;
2. first continuous-scroll scene at mid-progress;
3. tension or evidence scene with partial disclosure;
4. the frame immediately before the decisive threshold;
5. the decisive effect after it settles;
6. the opaque world transition at full cover;
7. the first frame after the transition;
8. a proof artifact in its fully readable state;
9. the final CTA and all form states.

Scroll forward and backward across discrete thresholds. Confirm the root theme,
overlays, and shared state do not become stranded.

## 4. Accessibility

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
- reduced-motion mode contains the complete story;
- no focusable control is hidden behind fixed chrome.

Keyboard-test all interactive controls. Do not infer accessibility from markup
alone.

## 5. Performance and resilience

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

Inspect the production bundle when adding a large motion or graphics
dependency. A visually impressive hero does not justify loading unused
libraries on every route.

## 6. Content and conversion

Confirm:

- claims match repository or product evidence;
- example output is real or clearly labeled as illustrative;
- CTAs point to real destinations;
- external links use safe target attributes;
- form endpoints and IDs are configured;
- form loading, success, error, disabled, and fallback states work;
- the same conversion action is not repeated excessively;
- metadata title and description match the current product;
- copyright, license, and dates are accurate.

Never submit real user data during verification without explicit authorization.
Use local or test values only when submission has been authorized.

## 7. Final diff review

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
