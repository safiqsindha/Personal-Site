# safiqsindha.com

My personal site — a single self-contained HTML file, no build step and no dependencies beyond Google Fonts.

Hardware program management at Microsoft Azure, the agent tooling I build outside of it, and a paper-cut forest that I probably spent longer on than I should have.

**Live:** https://safiqsindha.com

## Structure

Everything is in `index.html` — markup, styles, and scripts. The illustrations are hand-written inline SVG, so the whole site is about 90KB and renders without a single image request.

| File | Purpose |
|---|---|
| `index.html` | The entire site |
| `og-image.png` | Social share card (1200×630) |
| `favicon.svg` / `favicon-*.png` | Icons for browsers, iOS, Android |
| `safiq-sindha-resume.pdf` | Linked from the contact section |

## Notes

- Postcards flip on click or keyboard; card fronts carry the headline facts so nothing is hidden behind an interaction
- Ridgeline parallax and the badge pendulum are driven by scroll position, in one `requestAnimationFrame` loop that idles when nothing is moving
- Off-screen card animations pause via `IntersectionObserver`
- `prefers-reduced-motion` disables all of it
- Printing the page produces a plain-text resume — the card backs become the body copy
- There is a hidden game

## Deploying

Static files, so anything works. Currently on Cloudflare Pages with no build command and the repo root as the output directory.

## Want to build something similar?

The prompt I used is in [BUILD-YOUR-OWN.md](BUILD-YOUR-OWN.md) — fill in the bracketed sections with your own details and go. It includes the constraints that mattered, the mistakes worth skipping, and deployment notes.
