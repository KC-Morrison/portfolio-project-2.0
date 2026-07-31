# kmorrison.dev

Katie Morrison's portfolio site. One HTML file, three images, no build step.

## What's here

- `index.html` - the whole site (HTML, CSS, everything)
- `katie.webp` / `katie.jpg` - hero photo (square, 800x800)
- `og-image.jpg` - social sharing image (1200x630)
- `ROADMAP.md` - iteration roadmap, outstanding work and known traps; read this before making changes
- `PROJECT-INSTRUCTIONS.md` - the instructions text for the Claude project, and what to attach to it

Not in the repo: the original high-resolution photo and the QR codes. The QR codes can be regenerated from the URL at any time. Consider copying the original photo into `assets/source/` so future recrops are possible without hunting for it.

## How deploys work

Netlify is linked to this repository. Push to `main` and the site deploys automatically in about a minute. Every deploy is kept: to roll back, open Netlify, Deploys, pick an older one, "Publish deploy".

## Making a change

Using GitHub Desktop:

1. **Pull** before you start, so you have the latest
2. Edit `index.html` (yourself, or ask Claude)
3. Open `index.html` in a browser to check it, including at phone width
4. **Commit** with a one-line summary of what changed, then **Push**

## Rules for any change (see ROADMAP.md for the full list)

- Never name the employer anywhere, including metadata, alt text and commit messages
- Australian English, no em dashes
- Keep it a single dependency-free HTML file
- Test at phone width before pushing
- Confirm the file still ends with `</html>` and the contact section and footer are intact
