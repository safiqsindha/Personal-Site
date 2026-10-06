<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
    <img src="assets/banner-light.svg" alt="Personal Site" width="100%">
  </picture>
</p>

# safiqsindha.com

**One self-contained HTML file. No build step, no framework, no image requests.**

My personal site: hardware program management at Microsoft Azure, the agent tooling I build outside of it, and a paper-cut forest that I probably spent longer on than I should have.

- **~90 KB, zero images** — every illustration is hand-written inline SVG, so the page renders without a single additional request
- **No build step at all** — markup, styles, and scripts live in one `index.html`; deploying is copying files
- **Motion that behaves** — one `requestAnimationFrame` loop that idles when nothing moves, off-screen animation paused via `IntersectionObserver`, and everything disabled under `prefers-reduced-motion`
- **Degrades to a resume** — printing the page produces plain-text body copy from the card backs

![Live](https://img.shields.io/badge/live-safiqsindha.com-22c55e?style=flat-square)
![Build](https://img.shields.io/badge/build%20step-none-22c55e?style=flat-square)
![Size](https://img.shields.io/badge/size-~90KB-22c55e?style=flat-square)
![Dependencies](https://img.shields.io/badge/dependencies-Google%20Fonts%20only-0891b2?style=flat-square)

**[Live site](https://safiqsindha.com)** · **[Build your own](BUILD-YOUR-OWN.md)**

## Structure

The homepage is entirely `index.html` — markup, styles, and scripts. The blog is plain HTML pages that share one stylesheet.

| File | Purpose |
|---|---|
| `index.html` | The homepage |
| `blog/index.html` | Post listing |
| `blog/<slug>/index.html` | One folder per post, for clean URLs |
| `blog/blog.css` | Shared blog styles, same tokens as the homepage |
| `blog/feed.xml` | Atom feed |
| `_headers` | Cloudflare Pages security and cache headers |
| `og-image.png` | Social share card (1200×630) |
| `favicon.svg` / `favicon-*.png` | Icons for browsers, iOS, Android |
| `robots.txt` / `sitemap.xml` | Crawler directives |
| `assets/` | README banner artwork |

> **Known gap:** `index.html` links to `safiq-sindha-resume.pdf`, which is not tracked in this repository. Either commit the PDF or update the link in the contact section.

## Notes

- Postcards flip on click or keyboard; card fronts carry the headline facts, so nothing important is hidden behind an interaction
- Ridgeline parallax and the badge pendulum are driven by scroll position, in a single `requestAnimationFrame` loop that idles when nothing is moving
- Off-screen card animations pause via `IntersectionObserver`
- `prefers-reduced-motion` disables all of it
- Printing the page produces a plain-text resume — the card backs become the body copy
- There is a hidden game

## Writing a post

Still no build step — a post is a hand-written HTML file.

1. Copy `blog/one-html-file/` to `blog/<new-slug>/` and replace the title, description, dates, canonical URL, JSON-LD, and the `.prose` body
2. Add the post to the top of the list in `blog/index.html`
3. Add it to the `#writing` section of `index.html` (keep the newest three)
4. Add an `<entry>` to `blog/feed.xml` and bump the feed's `<updated>`
5. Add a `<url>` to `sitemap.xml`

## Deploying

Static files, so anything works. Currently on Cloudflare Pages with no build command and the repository root as the output directory.

## Want to build something similar?

The prompt I used is in **[BUILD-YOUR-OWN.md](BUILD-YOUR-OWN.md)** — fill in the bracketed sections with your own details and go. It covers the constraints that mattered, the mistakes worth skipping, and deployment notes.

## License

No license file is present in this repository. The design and copy are personal; the approach in [BUILD-YOUR-OWN.md](BUILD-YOUR-OWN.md) is free to reuse.
