# Build your own version of this site

This is the prompt I used to build [safiqsindha.com](https://safiqsindha.com). Paste it into Claude (or any capable model), fill in the bracketed sections with your own details, and you'll get something in the same family.

A few notes before you start:

- **Fill in the content section properly.** The output is only as good as what you put in. Vague inputs produce a vague site.
- **Approve the plan before letting it write code.** The last paragraph of the prompt forces this. Don't skip it — it's much cheaper to redirect a bad direction at the plan stage than after 2,000 lines of HTML exist.
- **Iterate on one card at a time.** Regenerating the whole file to fix a single illustration wastes the parts that already worked.
- **Change the art direction if forest paper-cut isn't you.** The structure below works with any consistent visual world — swap the aesthetic paragraph and keep everything else. Blueprint linework, risograph print, topographic maps, and midcentury travel posters would all work with the same bones.

---

## The prompt

Build me a single-file personal website — one self-contained `.html`, no build step, no dependencies except Google Fonts. It will be linked from my resume, so the audience is hiring managers and recruiters. It has to read as credible and high-signal first, and charming second — never the reverse.

### Visual direction

The aesthetic is **layered paper-cut illustration**, like a Vox explainer video or a screen-printed national park poster. One deep background color used consistently across the entire page. Every section sits above two layered ridgeline silhouettes (a lighter distant canopy, a near-black foreground ridge) built with CSS `clip-path`, plus a subtle SVG turbulence grain overlay at very low opacity.

**Critical constraint:** paper-cut must not become childish. Do not use rounded, friendly display fonts (Baloo, Quicksand, Fredoka, Comic Neue). Use a characterful serif for display, a clean grotesque for body, and a monospace for data labels and eyebrows — the monospace is what keeps it feeling like a spec sheet rather than a storybook. Muted, printed-stock colors, not saturated cartoon colors.

### Structure

1. **Hero** — a short handwritten-cursive SVG flourish that draws itself on load, then my name in very large display serif, a two-sentence positioning paragraph, and a strip of hard proof numbers with monospace labels beneath them.

2. **[Section one name]** — four postcards.

3. **[Section two name]** — four to six postcards.

4. **History** — a dense, scannable ledger. Left column is a monospace date range, right column is role, organization, and two or three sentences of substance. No flipping, no interaction — this is the part a recruiter actually reads.

5. **Badge band** — a lanyard-hung ID card, centered in its own section between History and Contact. Cream card stock, circular monogram, punched slot at top, and a dashed-rule list of key/value rows summarizing me.

6. **Contact** — a headline, a primary CTA, a resume download, and a monospace footer.

### Postcard mechanics

Each postcard is a 3D flip card (`transform-style: preserve-3d`, `rotateY(-180deg)` on toggle, ~1s custom cubic-bezier so it feels like a page turning rather than a UI toggle).

- **Front:** a full-bleed illustrated SVG scene, a gradient scrim for text legibility, a folded top-right corner (CSS `clip-path` triangle with a drop shadow), a monospace category tag, a short display-serif word, a title, a one-line note, and a small "Flip for detail" cue.
- **Back:** a muted darker shade of the front's color, a circular dashed postmark stamp rotated slightly, a heading, and three bullet points of real substance with the key figure bolded.
- **The front must carry the point, the back carries the proof.** Assume most visitors never flip a single card. Put the *concept* on the front and the *numbers* on the back — a front reading "89.8%" means nothing to someone who doesn't know what it measures.

Cards are `<button>` elements, keyboard-accessible, with `aria-pressed` reflecting flip state.

**Important:** use no hash links (`href="#section"`) anywhere. Nav items should be buttons that scroll via JS, offset for the fixed header. Hash navigation causes problems in sandboxed preview environments and buys nothing.

### The card illustrations — this is where the work goes

Every card front gets its own **hand-composed SVG landscape scene**, not an icon on a colored rectangle. Each scene should have: a tinted sky with a vertical gradient, a celestial body or atmospheric element, two or three layered hill silhouettes in progressively darker shades, and one foreground motif that literally depicts the card's subject.

Each scene needs its own **subtle looping animation** — different per card, always ambient rather than attention-grabbing. Lights blinking out of phase, figures moving along a path, rings expanding outward, a dashed line flowing, a dial sweeping, windows lighting in sequence.

Invent a scene that *depicts* the topic rather than symbolizing it generically. For example — replace these with your own:

- Infrastructure work → a skyline made of server racks at dusk with LEDs blinking
- Leadership → small figures climbing a switchback trail toward a ridge
- Security → a gatehouse with a searchlight sweeping across it
- Trade-offs → a balance scale tipping slowly
- Building tooling → planks laying themselves across a gap between two cliffs
- Teaching → a campfire with seated figures and rising embers
- A university → its landmark building, rendered in the same paper-cut language

### Motion

Beyond the card scenes, add three page-level effects:

- **Ridge parallax** driven by scroll position, with far and near ridges moving at different rates and in opposite horizontal directions.
- **The lanyard badge as a damped pendulum** — scroll delta becomes an angular impulse, so flicking the page makes it swing and settle. This is the single most delightful element; give it a faint idle motion so it never sits perfectly dead.
- A gentle pointer-driven drift on the ridgelines.

**Performance requirements, non-negotiable:** cache all geometry on load and resize — never call `getBoundingClientRect()` inside the animation loop. Run one `requestAnimationFrame` loop that stops when nothing is moving rather than looping forever. Pause off-screen card animations with `IntersectionObserver`. Avoid `mix-blend-mode` on full-screen layers and `backdrop-filter` on anything fixed.

### Content

Write the copy from these details, in first person, specific and unpretentious. No corporate filler, no "passionate about," no "results-driven."

- **Name / title / organization:** [...]
- **One-line positioning:** [...]
- **Hero proof numbers:** [3–5 hard facts]
- **Section one, four cards:** [name each and give 3 real bullets with numbers]
- **Section two, four to six cards:** [same]
- **History entries:** [role, org, dates, what you actually did]
- **Badge summary rows:** [6–8 key/value pairs]
- **Contact:** [LinkedIn URL, email]

### Quality floor

Responsive to mobile (cards reflow to one column, nav hides). On mobile WebKit, `backface-visibility` alone is unreliable — also toggle `visibility` at the flip midpoint or the back will bleed through the front. Visible keyboard focus rings and a skip link. `prefers-reduced-motion` fully respected. Scroll-triggered reveals via `IntersectionObserver` with a small stagger — but add a `no-js` class on `<html>` removed by an inline script, so the page is never blank if JS fails. Semantic HTML, decorative SVGs marked `aria-hidden`. Open Graph and Twitter card metadata, JSON-LD `Person` structured data, and a print stylesheet that collapses the page into a clean paper resume (hide the art and card fronts; print the card backs as body copy).

Before you write any code, tell me your palette as named hex values, your three typefaces and what each is doing, and a one-line description of each card scene. I want to approve the plan before you build.

---

## After the first draft

Things I'd expect to iterate on, based on how mine went:

- **Typography is the whole ballgame.** If the first result feels like a children's book, that's the fonts, not the illustrations.
- **Card titles drift toward being too specific.** "89.8% accuracy" on a card front is meaningless out of context; "Bitemporal memory layer" tells you what it is. Numbers go on the back.
- **Ask for stronger parallax than feels right.** Subtle motion often ends up invisible while still costing performance — the worst of both worlds.
- **Add an easter egg.** Mine hides a game of Snake behind a small element in the nav. Costs an hour, and it's the thing people mention.

## Deploying

Static files, so any host works. GitHub repo → Cloudflare Pages (no build command, root as output directory) → point your domain's nameservers at Cloudflare. Rename the file to `index.html`, keep every asset at the repo root since the paths are root-relative, and test your share card at [opengraph.dev](https://opengraph.dev) before pasting the link anywhere — LinkedIn caches previews aggressively.
