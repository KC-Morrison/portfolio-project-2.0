# kmorrison.dev

Katie Morrison's portfolio site. One HTML file, three images, no build step.

## What's here

- `index.html` - the whole site (HTML, CSS, everything)
- `katie.webp` / `katie.jpg` - hero photo (square, 800x800)
- `og-image.jpg` - social sharing image (1200x630)
- `ROADMAP.md` - iteration roadmap and hard rules; read this before making changes
- `assets/` - QR codes (PNG and SVG, two colourways) and the original photo for future recrops. Not deployed.

## How deploys work

Netlify is linked to this repository. Push to `main` and the site deploys automatically in about a minute. Every deploy is kept: to roll back, open Netlify, Deploys, pick an older one, "Publish deploy".

Netlify only needs `index.html` and the three images at the repo root; `assets/`, `ROADMAP.md` and this README deploy too but are harmless. To exclude them later, set Netlify's publish directory to a subfolder and move the four site files into it.

## Making a change

1. Pull first: `git pull`
2. Edit `index.html` (or ask Claude Code to)
3. Check it locally: open `index.html` in a browser
4. `git add -A && git commit -m "what changed" && git push`

## Rules for any change (see ROADMAP.md for the full list)

- Never name the employer anywhere, including metadata and alt text
- Australian English, no em dashes
- Keep it a single dependency-free HTML file
- Test at phone width before pushing
