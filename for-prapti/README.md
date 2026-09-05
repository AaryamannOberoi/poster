# for prapti 🤍

A scrolling love-note site with a 3D particle background, a tilting photo, and a line-by-line reveal.

## Files
- `index.html` — the whole site (includes the 3D box + cat companion and the confession scroll, all inline)
- `prapti.jpg` — the photo (keep it in the same folder as `index.html`, same name)
- `hello-kitty-final.png` — the little reveal image in the "welcome back" banner (keep it next to `index.html`)

## Deploy on GitHub Pages
1. Create a new repo (or reuse one), and add `index.html`, `prapti.jpg`, and `hello-kitty-final.png` to the root.
2. Push:
   ```
   git init
   git add .
   git commit -m "for prapti"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Source → Deploy from branch → main / (root)** → Save.
4. Your site goes live at `https://<your-username>.github.io/<repo-name>/` in a minute or two.

## Tweaking it
- The note text lives in `index.html` under `<section class="note">` — each line is its own `<p class="note-line">`.
- Colors are CSS variables at the top of the `<style>` block (`--accent-rose`, `--accent-gold`, etc.) if you want to shift the palette.
