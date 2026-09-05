# Prompt for Claude Code

Copy everything in the fenced block below and paste it into Claude Code, run from inside the `for-prapti/` project folder (see folder layout at the bottom of this file first).

```
I have an existing single-page site in this folder: index.html + prapti.jpg.
It's a scrolling "welcome back" page for my partner: a hero photo, a scrolling
handwritten note (the .note-line elements), and a "welcome back" banner at the
end. DO NOT change the existing copy, the photo, or the note text — you're
adding a new feature alongside what's there.

GOAL
Add a persistent 3D companion that lives on the page for the whole scroll: a
stylized kawaii cat mascot sitting inside a small 3D gift box, in the same
render style as reference/wireframe-1.png and reference/wireframe-2.png
(pure black background, the model drawn as bright white wireframe/line-art,
or a halftone dot-matrix build-up along the silhouette — blend the two if
that looks best). Do not copy the nav links or the time/weather HUD text from
those screenshots, just the rendering style: black background, white
wireframe/dotted geometry, that glowing low-poly look.

IMPORTANT — don't use an actual licensed Hello Kitty model or texture.
Design an original low-poly cat head with the same recognizable silhouette as
reference/hello-kitty-final.png (round head, big rounded ears, a bow, no
mouth, a couple of whisker lines) — an homage built from scratch, not a
ripped official asset.

BEHAVIOR
- On page load (or the first time the canvas scrolls into view), a 3D box
  sitting closed opens: the lid rotates up on a hinge and the cat's face is
  revealed underneath, with a smooth easing animation (roughly 1s).
- Once open, the cat's two pupils continuously track the cursor position,
  clamped so they never leave the eye socket — this is the main "game" feel,
  it should feel alive and a little funny/cute.
- The whole box+cat scene is `position: fixed`, sitting behind the note text
  in z-index, taking up roughly the right 40–45% of the viewport at full
  height, and it stays in place for the entire page scroll — it's the
  page's ambient background/companion, the same way the wireframe head is
  the persistent hero visual in the reference screenshots.
- The .note lines should read as if they're unrolling / dropping down from
  the top of the viewport in front of this background: raise their z-index
  above the canvas and keep them roughly within the left 55–60% of the
  viewport so they don't fully cover the box (a little overlap near the top
  is fine and matches the look).
- On narrow screens (below ~900px), shrink the box+cat canvas down into a
  small fixed widget (roughly 140x140px, pinned to a corner) instead of half
  the viewport, so the note text stays readable.
- At the very end of the page, in the "welcome back" banner section, add
  reference/hello-kitty-final.png as a small image next to or below the
  "welcome back" text — this is the final happy payoff, she loves Hello
  Kitty so this should land as a little reveal/reward at the end.

ALSO ADD — a clickable "confession scroll" + an honesty question
- Somewhere between the existing scrolling note and the final "welcome back"
  banner, add a rolled-up scroll/parchment graphic that sits closed and
  waiting. Unlike the .note-line lines above it (which reveal automatically
  as you scroll), this one does NOT auto-open — it only unrolls when she
  clicks/taps it. Give it a small idle animation (a gentle sway, or a soft
  pulse) so it visibly reads as something to click.
- On click, animate it unrolling and reveal two lines in the same
  handwriting style as the rest of the note:
  "ur the only cutie i miss"
  "and i loved this territorial side... its v hot 👀"
- About half a second after that reveal, show a playful question underneath:
  "thodi si chidhi thi ya nahi?" with two buttons, "yes" and "no".
- The "no" button is a joke and should dodge the cursor: on mouseenter (and
  on touchstart, for mobile, since hover doesn't exist there), reposition it
  to a new random spot within a bounded area near the question — not
  off-screen, not on top of "yes" — with a quick playful hop/transition
  rather than a hard teleport, so no matter how she chases it, it never
  lands under the cursor. "yes" behaves like a completely normal button.
- Clicking "yes" reveals one last short line underneath, something warm like
  "thought so 🫶", and that's the end of this interaction.

TECHNICAL
- Use Three.js (whatever version/CDN is already referenced in index.html, or
  a newer one if it's cleaner — this is a static file with no build step and
  no CSP restrictions, it just gets pushed to a GitHub repo and served via
  GitHub Pages, so any CDN script tag is fine).
- Build the box from a BoxGeometry with a separate lid mesh hinged on an
  Object3D pivot at the back edge; animate the open rotation with
  requestAnimationFrame easing, triggered by an IntersectionObserver (or a
  short delay on load).
- Build the cat head from primitives or a simple custom BufferGeometry —
  faceted/low-poly is exactly the right look, it doesn't need to be
  anatomically refined. Two small dark spheres for pupils, each translated
  within a small clamped radius based on normalized mouse position (simplest
  approach: offset by normalized mouse x/y with a clamp; upgrade to a
  raycast-onto-a-plane approach only if that looks meaningfully better).
- Respect prefers-reduced-motion the same way the rest of the site already
  does: skip the animated box-opening (just render it already open) and
  freeze or heavily dampen the eye-tracking.
- Keep it in index.html inline unless the new code gets long enough that
  splitting it into a kitty.js file is clearly cleaner — either is fine, just
  keep it a static, buildless site.

Work in small steps: get the box + hinge + open animation working and
visually right first, then add the cat head and get the render style
matching the references, then wire up eye tracking last. Show me progress
along the way rather than doing it all in one shot.
```

## Folder layout to hand to Claude Code

```
for-prapti/
├── index.html                     (already have this)
├── prapti.jpg                     (already have this)
└── reference/
    ├── wireframe-1.png            (style reference — dot/halftone reveal)
    ├── wireframe-2.png            (style reference — clean wireframe mesh)
    └── hello-kitty-final.png      (the payoff image for the ending)
```

All three reference images are already in the `reference/` folder alongside this prompt — just keep the whole `for-prapti/` folder together and open Claude Code inside it. The images matter here, not just the words: Claude Code can actually look at them, and dot density, line weight, and exactly how "kawaii" the final cat should read are things that are much easier to nail by pointing at a picture than describing in text.

One nudge if the first pass doesn't look right: ask it to iterate specifically on the wireframe/dot shader against the two reference screenshots side by side — that's the part most likely to need a couple of tries to get the density and glow right.
