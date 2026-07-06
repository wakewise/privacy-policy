# WakeWise privacy policy site

Static GitHub Pages site that hosts the WakeWise Alarm privacy policy at a public URL
(needed for the Google Play Store listing).

- `index.html` — the policy page. Self-contained: inline CSS, system fonts, **no external
  scripts, fonts, or trackers**, so viewing the page does not leak the visitor's data to a
  third party. Supports light/dark mode automatically.
- `.nojekyll` — tells GitHub Pages to serve the files as-is instead of running the Jekyll
  build.

## Enable GitHub Pages

This project must live in a GitHub repository first. Then:

1. Push the repo to GitHub.
2. Repo **Settings → Pages**.
3. **Source:** "Deploy from a branch".
4. **Branch:** `main` (or your default), **Folder:** `/docs`. Save.
5. Wait ~1 minute. The URL appears at the top of the Pages settings, e.g.
   `https://<your-username>.github.io/<repo-name>/`.
6. Paste that URL into the Play Console listing's "Privacy Policy" field.

### If the repo is private
GitHub Pages on a private repo requires a paid plan. If yours is private and you don't want to
make the whole Android source public, create a **separate public repo** (e.g. `wakewise-privacy`),
copy `index.html` and `.nojekyll` into its root, and enable Pages there with folder `/ (root)`.

## Keeping it in sync

The source of truth is [`../storepagestuff/PRIVACY_POLICY.md`](../storepagestuff/PRIVACY_POLICY.md).
`index.html` is a hand-maintained copy of that content. When you edit the policy, update both
files (or ask Claude to regenerate `index.html` from the markdown).
