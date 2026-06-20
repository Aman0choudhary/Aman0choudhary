# PLAN — anime-noir GitHub profile README

Goal: replicate the ink-splatter / bold-lockup poster aesthetic (ref: Toji fan art) for a GitHub profile README — without reproducing copyrighted character art. Anchor = typographic lockup instead of character illustration.

## 1. Design tokens

```
bg            #f4f2ec   off-white
ink           #0a0a0a / #070707→#1c1c1c gradient   panel + lockup-adjacent dark mass
accent        #2dd4bf   teal — tags, glow flecks, badge icons, stat-widget rings
text-muted    #3a3a3a   tag strip / ID stamp (on light bg)
text-soft     #b9b6ae   tagline (on dark bg)
type-display  Arial Black / system bold sans, heavy tracking — the lockup word
type-mono     Courier New — tags, stamps, stats labels
type-body     Georgia italic — one-line tagline
```

## 2. File structure

```
your-username/              ← repo must be named exactly your GitHub username
├── banner.svg
└── README.md
```

## 3. Build banner.svg

1. Canvas 1600×500, base fill = bg color.
2. Generate a single jagged "torn panel" path: irregular polygon, left edge pinned to x=0, right edge wanders ~500–650px with 2–3 sharp outward notches (the "spike" details). Force the edge ≥640px wide specifically across the y-band where the lockup text sits, so the panel never clips the letters.
3. Fill panel with dark radial gradient (#1c1c1c → #070707).
4. Clip a layer of low-opacity (~0.05–0.18) blobs inside the panel for ink-wash texture variation.
5. Outside the panel, scatter ~80 small irregular blobs (organic blob path: jittered points + quadratic joins, not circles) decreasing in size/opacity left→right, to read as debris bleeding into the white space. Do NOT clip these — they cross the panel boundary on purpose.
6. Inside the panel, add 5–7 small teal (#2dd4bf) blobs near the upper-left as glow flecks (echoes the reference's eye-glow without depicting eyes).
7. Lockup text: your name/handle, Arial Black, ~120–130px, heavy letter-spacing, fill = bg color (light-on-dark), positioned inside the guaranteed-wide panel band.
8. Below it: monospace tagline in accent color, then a smaller italic line in text-soft.
9. Right side (light field only): thin horizontal divider + monospace tag strip (4–5 short caps phrases separated by `|`) in text-muted, plus a small top-right "ID stamp" (e.g. `PROJECT//001`) for the poster-credit detail.
10. **Renderer trap to avoid:** skip `feTurbulence`/blur filters for any base layer. If the filter isn't supported by the viewer (GitHub's image proxy, some renderers), an unfiltered rect defaults to opaque black and blacks out the whole canvas. Texture via layered low-opacity blobs instead, not filters.

## 4. Build README.md

Sections, in order:

1. `<img src="./banner.svg" width="100%">` centered.
2. Optional: readme-typing-svg badge (animated one-liner, same accent color) right under the banner.
3. Dossier block — fenced code block, `key   value` aligned, 4–5 lines (role / based / building / stack / status).
4. Current project callout — blockquote, 3–4 sentences, what it does not just what it's built with.
5. Stack badges — shields.io `style=for-the-badge`, `color=0a0a0a`, `logoColor=2dd4bf` for every badge, so they sit on the same palette as the banner.
6. Metrics — github-readme-stats + top-langs + streak-stats widgets, all themed with `bg_color=0a0a0a`, accent params set to `2dd4bf`, text to `b9b6ae`/`f4f2ec`. **Every widget URL needs your real username swapped in or it 404s/renders empty.**
7. Reach — 2–3 social badges, same dark/teal badge style.
8. Footer — repeat the tag-strip device from the banner bottom (small caps, `|`-separated, centered) as a closing rhyme.

## 5. Ship it

1. Create repo named exactly your GitHub username (triggers the special profile-README feature).
2. Drop both files in root, commit, push.
3. Find/replace the username placeholder across every stats-widget URL.
4. Swap real social links.
5. Optional: change the single accent hex (`2dd4bf`) everywhere to retheme without touching layout.
