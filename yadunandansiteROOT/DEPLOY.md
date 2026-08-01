# Deploying to GitHub Pages

## The file layout matters

GitHub Pages serves `index.html` from **the root of the branch** (or from `/docs`). It does not
look inside other folders.

So the files must sit like this in the repository — **not** nested inside an `ahir-boarding/`
folder:

```
<repo root>/
├── index.html          ← must be at the top level
├── .nojekyll           ← must be at the top level
└── assets/
    ├── brand/
    │   ├── logo.png
    │   ├── logo-cream.png
    │   └── emblem.png
    └── images/
        ├── building-dusk.jpg
        ├── corridor.jpg
        ├── ground-aerial.jpg
        ├── ground-cricket.jpg
        └── study-hall.jpg
```

**If `index.html` ends up inside a folder, the site URL returns 404.** That is the most common
cause of "it doesn't work after uploading".

Use `yadunandan-site-ROOT.zip` — its contents are already arranged this way. Unzip it and upload
what is *inside* it, not the folder itself.

## What `.nojekyll` does

GitHub Pages runs every site through Jekyll by default. Jekyll can fail the build on a plain
static site and will email you "Page build failed". The empty `.nojekyll` file switches Jekyll
off entirely and serves the files as they are. It must be at the repository root.

## Uploading through the GitHub website

Dragging a *folder* into GitHub's upload page sometimes flattens or drops nested files. Safer:

1. Upload `index.html` and `.nojekyll` first (root level).
2. Then **Add file → Create new file**, type `assets/brand/x` in the name box — GitHub creates the
   folders as you type the `/`. Cancel, then use **Upload files** and drag the images in while
   inside that folder.

Or just use `git`:

```bash
git add .
git commit -m "Add website"
git push
```

## Turning Pages on

Repository → **Settings** → **Pages** → Source: *Deploy from a branch* → pick the branch and
`/ (root)` → **Save**. Give it a minute, then reload.

## Check it worked

Open the site and confirm:

- The page loads at all (not 404) → `index.html` is at the root.
- The building photo shows behind the hero → the `assets/` folder uploaded with its structure.
- The Krishna emblem shows in the top-left → `assets/brand/emblem.png` is there.

If photos are missing but the page loads, the `assets/` folder did not upload correctly. Paths are
**case-sensitive** on GitHub Pages: `Building-Dusk.JPG` will not match `building-dusk.jpg`.
