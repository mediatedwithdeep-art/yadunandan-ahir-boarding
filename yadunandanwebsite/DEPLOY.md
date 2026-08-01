# Deploying — GitHub + Vercel

**There is no build step.** No npm, no framework, no package.json. Vercel just serves the files.

## The files

```
index.html
vercel.json
.nojekyll
assets/
  brand/   emblem.png  logo.png  logo-cream.png
  images/  building-dusk.jpg  corridor.jpg  dining.jpg  ground-aerial.jpg
           ground-cricket.jpg  library.jpg  room.jpg  study-hall.jpg  thali.jpg
```

**All fifteen files go at the ROOT of the repository.** Not inside a folder.

If `index.html` ends up inside a folder, the site 404s — that is what happened last time.

## Upload to GitHub

Easiest and safest is git:

```bash
git add .
git commit -m "Update website"
git push
```

If you use the GitHub website instead: dragging a *folder* onto the upload page sometimes drops
or flattens nested files. Drag the **contents** — `index.html`, `vercel.json`, and the `assets`
folder — rather than a wrapper folder around them.

## Vercel

Push to GitHub, then in Vercel hit **Redeploy**. That is all — it will not build anything.

If you are connecting the project for the first time:

- **Framework Preset:** `Other`
- **Root Directory:** `./`
- **Build Command:** leave empty
- **Output Directory:** leave empty
- **Install Command:** leave empty

Vercel detects a static site automatically because there is no `package.json`.

### What `vercel.json` does

Nothing that can break a deploy — it declares no build. It only:

- caches `assets/*` for a year (photos never change once uploaded, so repeat visits are instant)
- sets two standard security headers
- turns on clean URLs

Deleting it would still deploy fine; you would just lose the caching.

## Check it worked

1. The page loads (not 404) → `index.html` is at the root.
2. The building photo shows behind the hero → `assets/` uploaded with its structure.
3. The Krishna emblem shows top-left → `assets/brand/emblem.png` is there.
4. The photo grid shows nine photographs, none of them a dashed "photo needed" box.

If the page loads but photos are missing, the `assets/` folder did not upload correctly.
Filenames are **case-sensitive**: `Room.JPG` will not match `room.jpg`.

## `.nojekyll`

Only matters if you also serve this from GitHub Pages — it stops Jekyll from processing the
site and failing the build. Harmless on Vercel.
