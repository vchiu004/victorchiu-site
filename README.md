# victorchiu.com

Static site. No build step, no dependencies, no framework. Open any `.html`
file in a browser and it works.

## Files

| File | What it is |
|---|---|
| `index.html` | Home — springing name, sound-on-hover project index, paintings, writing |
| `capsule.html` | Capsule — complete with photographs |
| `tap-room.html` | Tap Room / Motion Detect Synth — complete with photos and patches |
| `two-instruments.html` | BOO + Living Wavetable — needs its images |
| `sound-works.html` | Five pieces with Bandcamp players |
| `paintings.html` | Gallery — six labelled slots waiting for the paintings |
| `sdp-statement.html` | Unstable Systems (SDP statement) |
| `writing.html` | Writing index |
| `about.html` | Bio, contact, CV — needs its two photos |
| `essay.html` | Template — duplicate per new piece of writing |
| `project.html` | Template — duplicate for a future project |
| `style.css` | All styling. Colours and type at the top |
| `images/` | 18 processed photographs and patch screenshots |
| `audio/` | 15 loudness-matched, seamless-loop excerpts |
| `favicon.png`, `apple-touch-icon.png` | The tab icon — a crop of *Untitled*, 2026 |
| `404.html` | Shown for missing pages (Cloudflare Pages picks it up automatically) |
| `sitemap.xml`, `robots.txt` | Search engines |

## Before you publish

Search every file for square brackets (`[ ]`) — those are placeholders.
Also replace:

- `you@victorchiu.com` with your real address
- the `#` in the Instagram / LinkedIn footer links
- the `<meta name="description">` on each page (this is what Google shows)

## Adding a project

1. Duplicate `project.html`, rename it something like `thesis.html`
2. Edit the title, fact table, and text
3. Open `index.html`, copy one `<a class="index-row">` block, paste it, and
   point its `href` at your new file

Adding an essay works the same way with `essay.html` and `writing.html`.

## Adding images

Make a folder called `images`, drop your files in, then replace:

```html
<div class="figure-placeholder">Lead image</div>
```

with:

```html
<img src="images/your-file.jpg" alt="Describe what the image shows">
```

Resize photos to about 2000px wide before uploading — a 12MB camera file will
make the page slow to load. The `alt` text matters for screen readers and for
search.

## Changing the look

Everything visual is controlled by the block at the top of `style.css`:

```css
--paper:  #EDEDE8;   /* background */
--ink:    #111110;   /* text and rules */
--accent: #0026FF;   /* links and eyebrows */
```

Change those three values and the whole site changes.

The name on the home page is deliberately set wider than the screen and
clipped at the right edge. If you'd rather it fit, find `.lockup h1` and lower
`21vw` to about `13vw`.

## Audio

Excerpts live in `audio/`. The home page picks one at random per project on
hover. To add or replace one, drop the file in and edit the `EXCERPTS` list at
the top of the `<script>` block in `index.html`.

All excerpts were loudness-matched to -18 LUFS and rendered as seamless loops
(a 2-second crossfade joins the tail back to the head), so hovering between
rows doesn't jump in volume and a looping excerpt has no audible seam. If you
add new files, run them through the same treatment or they'll stand out.

Keep excerpts around 30 seconds. The player loops them for a randomised 32-58
seconds before fading out on its own.

## Publishing

### 1. Put the files on GitHub

- Make a free account at github.com
- Create a new repository (public is fine)
- Upload all the files — GitHub's web uploader works, no command line needed

### 2. Connect Cloudflare Pages

- Sign up at pages.cloudflare.com (free)
- Create a project → connect your GitHub repo
- Leave the build settings blank; there's no build step
- Deploy. You'll get a temporary address like `victorchiu.pages.dev`

Check that address works before touching your domain.

### 3. Point victorchiu.com at it

Your domain stays registered with WordPress.com. You're only changing where
it points.

- In Cloudflare Pages: your project → Custom domains → add `www.victorchiu.com`
  and `victorchiu.com`. Cloudflare will show you the DNS values it wants.
- In WordPress.com: Domains → select victorchiu.com → **Change Your Name
  Servers & DNS Records** → turn off "Use WordPress.com Name Servers" → enter
  Cloudflare's nameservers → Save.

Give it a few hours. Up to 48 in the worst case.

**Before you switch:** if you have email at victorchiu.com, write down your MX
records first and re-add them at Cloudflare, or your email will stop arriving.

From then on, every time you push a change to GitHub, the live site updates
automatically.
