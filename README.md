# Marky's Landscaping — Website

A single-page site for Marky's Landscaping (Chaguanas, Trinidad & Tobago) featuring a
scroll-scrubbed video hero, a real "Our Work" video, real before/after photography, and
full service/contact info.

## What's inside

```
index.html              — the entire site (HTML/CSS/JS in one file)
assets/
  logo.png               — Marky's Landscaping logo (transparent background)
  video/
    hero.mp4              — background montage, scroll-scrubbed in the pinned hero section
    our-work.mp4           — real crew footage, click-to-play in the "Our Work" section
  images/
    ...                    — real before/after and crew photos, cropped from marketing
                             flyers and customer photos
```

No build step, no dependencies, no framework — it's a static site, so it deploys as-is.

## Deploy to GitHub

1. Create a new repository on GitHub (e.g. `markys-landscaping`).
2. Upload every file in this folder, **keeping the folder structure intact**
   (the `images/` folder must stay a folder, not be flattened).
3. Commit to the `main` branch.

Via git CLI, from inside this folder:
```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/markys-landscaping.git
git push -u origin main
```

## Deploy to Vercel

1. Go to [vercel.com/new](https://vercel.com/new) and import the GitHub repo you just created.
2. Framework preset: choose **"Other"** (this is a plain static site — no build command needed).
3. Leave build/output settings blank and click **Deploy**.
4. Vercel will give you a live `.vercel.app` URL immediately. You can attach a custom domain
   afterward under Project Settings → Domains.

That's it — every push to `main` will auto-redeploy.

## Performance notes

- `hero.mp4` uses all-intra frame encoding (every frame is a full keyframe) — this is
  required for the scroll-scrub to stay smooth, and is why it doesn't compress down further
  without introducing jank into the scroll animation.
- `our-work.mp4` (the "Our Work" section video) is fully lazy — no network request happens
  for it at all until the visitor scrolls near that section.
- The logo loads as WebP (with a PNG fallback for older browsers) — about 75% smaller than
  the PNG at identical visual quality, which matters since it appears four times on the page.
- Fonts load via a preconnected `<link>` instead of a render-blocking `@import`.
- Vercel serves everything over HTTP compression and a CDN automatically — no extra config
  needed for that part.

## Notes

- The site opens with a brief "Enter Site" screen — this is intentional. Browsers require
  a real user click before they'll allow JavaScript to scrub a video frame-by-frame on scroll,
  so this button satisfies that requirement.
- Phone numbers used: **(868) 314-6575** (general contact) and **(868) 314-6576** (free quotes) —
  double check both are correct before going live.
- To swap the background video or any photo later, just replace the file with the same name
  inside `assets/` and redeploy — no code changes needed.
