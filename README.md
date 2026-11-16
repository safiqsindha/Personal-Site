# safiqsindha.com: one HTML file, no build step

[Live site](https://www.safiqsindha.com) · [Writing](https://www.safiqsindha.com/blog/) · [Resume (PDF)](https://www.safiqsindha.com/safiq-sindha-resume.pdf) · [Build your own](BUILD-YOUR-OWN.md)

The personal site of a hardware program manager at Microsoft Azure who builds agent evals on the side. The homepage is a single hand-written `index.html`: markup, styles and scripts in one file, 97 KB on disk and about 25 KB over the wire. Every illustration, including the 17 flip-card postcards, is inline SVG, so the page makes no image requests. There is no framework, no bundler and no build command; deploying is copying files.

## Design decisions

**One file is the constraint that decides everything else.** "No build step" ruled out most libraries before they could be argued for. The trade-off is a long file; it stays navigable because every section is a commented block in page order.

**Headline numbers on the front, detail on the back.** Each postcard leads with its strongest fact (450 racks, 97%, $10M) so nothing important is hidden behind a click. The back holds the supporting detail.

**Motion that idles.** One `requestAnimationFrame` loop drives the ridgeline parallax and the badge pendulum, and stops when nothing moves. Off-screen card animations pause through `IntersectionObserver`, and `prefers-reduced-motion` turns all of it off.

**Readable without the tricks.** The page works with JavaScript off, text meets 4.5:1 contrast with nothing under 11px, the phone nav keeps all six links, and printing produces a plain-text resume built from the card backs.

**One fact, one source.** Every figure on the site matches the resume PDF in this repository; when they disagree, the resume wins.

Scope: Google Fonts is the only third-party dependency, and Cloudflare adds its analytics beacon at the edge. Card details sit behind a flip, which is a deliberate cost of the postcard design. There is a hidden game.

## Repository

```
index.html                 the homepage: markup, styles, scripts, inline SVG
404.html                   not-found page, served by the Worker's 404-page handling
blog/                      plain HTML posts sharing blog.css, plus the Atom feed
safiq-sindha-resume.pdf    the resume linked from the contact section
_headers                   security and cache headers, applied by Cloudflare
wrangler.jsonc             deploy config: serve the repo root as static assets
.assetsignore              repo-only files kept out of the upload
robots.txt, sitemap.xml    crawler directives
og-image.png, favicon*     share card and icons
BUILD-YOUR-OWN.md          the prompt behind the site, for reuse
```

## Running it locally

```
python3 -m http.server     # then open http://localhost:8000
```

`python3 -m http.server` does not serve `404.html` for missing paths; open it directly to preview it. `wrangler dev` reloads in a loop here because it writes to `.wrangler/` inside the folder it serves.

## Deploying

A Cloudflare Worker with static assets, deployed by Workers Builds on every push to `main`. Pull requests get a preview URL. There is no Worker script and no build command; `.assetsignore` keeps the README, build notes and `.git` out of the upload. The canonical host is `www.safiqsindha.com`.

## Writing a post

A post is a hand-written HTML file.

1. Copy `blog/one-html-file/` to `blog/<new-slug>/` and replace the title, description, dates, canonical URL, JSON-LD and the `.prose` body
2. Add the post to the top of the list in `blog/index.html`
3. Add it to the `#writing` section of `index.html` (keep the newest three)
4. Add an `<entry>` to `blog/feed.xml` and bump the feed's `<updated>`
5. Add a `<url>` to `sitemap.xml`

## Building something similar

The prompt is in [BUILD-YOUR-OWN.md](BUILD-YOUR-OWN.md): fill in the bracketed sections with your own details. It covers the constraints that mattered, the mistakes worth skipping, and deployment notes.

## License

No license file. The design and copy are personal; the approach in [BUILD-YOUR-OWN.md](BUILD-YOUR-OWN.md) is free to reuse.
