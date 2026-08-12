# Deploy checklist

Delete this file once you're live — it's notes to self, not part of the site.

---

## 1. GitHub

1. Create a new **public** repo. Name it `safiqsindha.com` or `personal-site`.
2. Click **uploading an existing file**, drag in everything from this folder, commit.
3. Confirm all files sit at the **root** — no subfolders. The HTML references `/favicon.svg` and `/og-image.png` as root paths, so nesting breaks them.

## 2. Cloudflare Pages

1. Sign up / log in → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
2. Authorize GitHub, pick the repo.
3. Build settings:
   - Framework preset: **None**
   - Build command: **leave empty**
   - Build output directory: **leave empty** (or `/`)
4. Deploy. You get a `*.pages.dev` URL in about a minute — open it and confirm the site works.

## 3. Custom domain

1. In the Pages project → **Custom domains** → add `safiqsindha.com`, then add `www.safiqsindha.com`.
2. Cloudflare will prompt you to add the domain as a **site** first. Do that — it gives you two nameservers.
3. **Squarespace Domains** → your domain → **Nameservers** → switch from Squarespace defaults to the two Cloudflare gave you.
4. Wait for propagation. Usually under an hour, occasionally longer. HTTPS is issued automatically.

## 4. Verify

- [ ] `https://safiqsindha.com` loads
- [ ] `https://www.safiqsindha.com` redirects to it
- [ ] Padlock shows (valid HTTPS)
- [ ] Favicon appears in the tab
- [ ] Nav buttons scroll to the right sections
- [ ] Cards flip on click and on tap
- [ ] Badge swings when you scroll past it
- [ ] The hidden game opens (click the ochre period after the name)
- [ ] Cmd/Ctrl-P produces a clean printable resume
- [ ] Check on an actual phone, not just a narrow browser window
- [ ] Paste the URL into https://opengraph.dev and confirm the share card renders

## 5. Before sharing the link anywhere

- [ ] Add `safiq-sindha-resume.pdf` to the repo — **exact filename**, or the download button 404s
- [ ] Read the whole page once more with NDA eyes: SKU and revision counts, cluster figures, the four-week security timeline
- [ ] Update the LinkedIn URL if `linkedin.com/in/safiqsindha` isn't exactly right

LinkedIn caches link previews hard. Test the share card **before** you paste it into any post or message.

## 6. Optional, later

- Cloudflare Web Analytics — free, no cookie banner needed, one toggle in the dashboard
- Transfer the domain registration from Squarespace to Cloudflare once it's 60+ days old, so everything lives in one account
- Update `sitemap.xml` if you ever add pages

---

## Updating the site later

Edit `index.html` in GitHub (pencil icon works fine for small text changes), commit, and Cloudflare redeploys automatically in under a minute. No manual upload step ever again.
