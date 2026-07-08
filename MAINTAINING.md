# Maintaining R7's Online Guide

This is your personal playbook for updating the guide and publishing it. It's
written to be followed even if you don't live in a terminal. Keep it in the
repo so it's always next to the file it describes.

The whole guide is one file: **`index.html`**. Everything else in the repo
(this file, the README, the changelog, the license) is supporting material.

---

## Part A — One-time setup (do this once)

You'll put the guide on **GitHub Pages**, GitHub's free static hosting. The
result is a stable public link that never changes, even as you update the
guide.

### 1. Create the repository

1. Sign in at <https://github.com> and click **New repository**.
2. Name it something clean, e.g. `r7-online-guide`.
3. Set it to **Public** (public is what makes the history transparent).
4. Don't add a README from GitHub — you already have one. Click
   **Create repository**.

### 2. Upload the files

Easiest path (no command line):

1. On the empty repo page, click **uploading an existing file**.
2. Drag in **all** of these:
   - `index.html`
   - `README.md`
   - `MAINTAINING.md`
   - `CHANGELOG.md`
   - `LICENSE`
3. In the commit box at the bottom type `Initial publish (v1.7)` and click
   **Commit changes**.

<details>
<summary>Prefer the command line? Click here.</summary>

```bash
# from the folder containing the files
git init
git add index.html README.md MAINTAINING.md CHANGELOG.md LICENSE
git commit -m "Initial publish (v1.7)"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/r7-online-guide.git
git push -u origin main
git tag v1.7 && git push --tags
```
</details>

### 3. Turn on hosting

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Set **Branch** to `main` and folder to `/ (root)`. Click **Save**.
4. Wait ~1 minute. GitHub shows your live URL, like
   `https://YOUR-USERNAME.github.io/r7-online-guide/`.

Because the file is named `index.html`, that URL shows the guide directly.

### 4. Point the README at your live URL

Open `README.md`, replace the placeholder URL near the top with your real
Pages URL, and commit. Done — you're live.

---

## Part B — Publishing an update (do this every time)

Think of a release as **five small steps**. They take a few minutes.

### Step 1 — Edit the content

Open `index.html` and make your change. Use the **content landmarks** in the
comment at the very top of the file to jump to the right spot (e.g.
`id="section2"`, `class="wn-body"`, `id="glossary"`).

House rules while editing:
- Every external link gets `target="_blank" rel="noopener"`.
- Prefer official first-party links.
- Write for a smart reader with **zero** technical background. If you must use
  a technical term, define it — or add it to the Glossary.

### Step 2 — Bump the version number in THREE places

Search `index.html` for the old version (e.g. `v1.7`) and update:

1. The `<title>` tag near the top.
2. The header link — search for `version-link` — change `vX.X · Month Year`.
3. The *What's New* label — search for `wn-current` — change `Latest: vX.X`.

**Version numbering, plain rules:**
- Small fixes (dead links, typos, wording): bump the **last** number —
  `v1.7 → v1.7.1`.
- New sections or meaningful new advice: bump the **middle** number —
  `v1.7 → v1.8`.

### Step 3 — Add a "What's New" entry

Search for `wn-body`. Copy the most recent `<div class="wn-release"> … </div>`
block, paste it **directly below `wn-body` (at the top of the list)**, and
rewrite it for your new version. **Never delete old entries** — the history is
the point. Template:

```html
<div class="wn-release">
  <h4><span class="wn-ver">v1.8</span> <span>Short release title</span> <span class="wn-date">Month 2026</span></h4>
  <ul>
    <li>Plain-English description of each change.</li>
  </ul>
</div>
```

### Step 4 — Flag genuinely new content

Add `<span class="new-badge">New v1.8</span>` next to new items, and remove
"New" badges that are more than two versions old so they don't pile up.

### Step 5 — Mirror the entry into `CHANGELOG.md`

Copy the same plain-English bullet points into `CHANGELOG.md` under a new
heading at the top. This keeps a clean history that readers (and search
engines) can follow without opening the HTML.

### Then publish

**No command line:** in the repo, click `index.html`, click the pencil
(**Edit**), paste your updated file, and commit with a message that matches the
changelog, e.g. `v1.8 — add hardware wallet section, fix 3 dead opt-out links`.
Do the same for `CHANGELOG.md`. Then go to **Releases → Draft a new release**,
create a tag like `v1.8`, and publish — that gives readers a downloadable
snapshot.

<details>
<summary>Command line version</summary>

```bash
git add index.html CHANGELOG.md
git commit -m "v1.8 — add hardware wallet section, fix 3 dead opt-out links"
git push
git tag v1.8 && git push --tags
```
</details>

---

## Part C — Routine housekeeping

Privacy links rot faster than almost anything. A light recurring pass keeps the
guide trustworthy:

- **Quarterly:** click through the **Section 3** opt-out links — they change
  often. Fix or mark any that break. This matches the quarterly opt-out cadence
  the guide itself recommends.
- **Twice a year:** re-check that recommended tools are still maintained,
  still free where you said they were, and still the best pick.
- **Any time a tool changes hands or gets acquired:** re-evaluate whether it
  still belongs in the guide.

When you retire a recommendation, say so in the *What's New* entry and briefly
explain why (as done for HTTPS Everywhere and BitChat in v1.7). Telling readers
*why* something was removed is part of the transparency promise.

---

## Quick reference

| I want to…                        | Where to look                                  |
| --------------------------------- | ---------------------------------------------- |
| Change the intro / contact        | `id="quickstart"` and the `<section class="hero">` |
| Edit a section's advice           | `id="section1"` … `id="section4"`              |
| Add/adjust a glossary term        | `id="glossary"`                                |
| Add a changelog entry             | `class="wn-body"`                              |
| Update the license/footer         | the `<footer>` block                           |
| Change the version number         | `<title>`, `version-link`, `wn-current`        |
