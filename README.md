# EquiGQNet - Project Page

Project page for **EquiGQNet: Fast Grasp Quality Evaluation via Shared Equivariant Point Cloud Encoding**.

Live at <https://equigqnet.github.io/>.

## Status

| Item | State |
| --- | --- |
| Paper (arXiv) | Not submitted yet - page shows a disabled "Soon" button |
| Code | Not released yet - page shows a disabled "Soon" button |
| Real-world videos | Included (6 runs, 6x playback speed) |

## Structure

```
index.html                            # the whole page
static/css/bulma.min.css              # Bulma, from the Academic Project Page Template
static/css/index.css                  # template styles
static/css/equigqnet.css              # project-specific styles (template CSS untouched)
static/js/fontawesome.all.min.js      # renders the 4 button/UI icons as inline SVG
static/js/index.js                    # BibTeX copy + scroll-to-top
static/images/figures/                # the 3 figures used on the page
static/videos/house_hold{1,2,3}.mp4   # household decluttering runs, 6x speed
static/videos/dexnet_adv{1,2,3}.mp4   # Dex-Net adversarial runs, 6x speed
paper/                                # LaTeX source the page content was written from
```

`static/` holds only what the page references. The template's carousel and slider
libraries, its sample PDF and placeholder media, the Font Awesome *stylesheet* (dead
without the `webfonts/` folder, which the template never shipped) and jQuery are all
gone. No favicon is declared, so browsers show their own default page icon.

Page sections, in order: hero, teaser pair, Abstract, Introduction, Real-World
Experiments (setup figure, results table, decluttering runs), BibTeX.

The only page-specific JavaScript is a short IntersectionObserver at the end of
`index.html` that autoplays the run videos on scroll; everything else is static
HTML/CSS, so GitHub Pages serves it as-is. `.nojekyll` is present, so no Jekyll build runs.

### Figure pattern

Figures follow one pattern throughout - a paragraph, then an uncaptioned figure linked
to the full-size file:

```html
<div class="has-text-centered project-figure">
  <a href="static/images/figures/NAME" target="_blank" rel="noopener">
    <img src="static/images/figures/NAME" alt="..." loading="lazy">
  </a>
</div>
```

Add `class="fig-half"` on the `<img>` to render it at half the column width. Every
figure stays inside the 960px text column, so nothing is wider than the prose.

## Things left to fill in

Search `index.html` for `TODO` - each one marks a spot to update:

1. **After arXiv submission** - set the `href` on the Paper and arXiv buttons, then remove
   the `is-soon` class, the `aria-disabled` attribute and the `<span class="soon-tag">`
   from those two `<a>` elements. Also uncomment the `citation_arxiv_id` /
   `citation_pdf_url` meta tags (Google Scholar reads them) and replace the `note` field
   in the BibTeX block with the real `eprint` / `archivePrefix` / `primaryClass`.
2. **On code release** - same treatment for the Code button, pointing at the repository.
3. **Jaeseog Won's link** - the only author without a personal page; wrap the name in an
   `<a href="...">` like the others once one exists.
4. **Social preview** (optional) - the `og:image` / `twitter:image` tags currently point at
   `fig1_overview.png`. A purpose-made 1200x630 image at
   `static/images/social_preview.png` renders better in link previews.

## Videos

The six clips total roughly 76 MB, which is comfortably inside GitHub Pages' limits
(1 GB per repository, 100 GB/month bandwidth).

- **Teaser** (top of page): `house_hold1.mp4` and `dexnet_adv1.mp4` side by side, muted
  autoplay on loop.
- **Decluttering Runs**: all six clips in a 3-wide grid, household on the top row and
  Dex-Net adversarial on the bottom row.

The grid clips carry `data-autoplay` and start playing when they scroll into view, via an
IntersectionObserver in the script at the end of `index.html`; they pause again on the way
out. They deliberately do *not* use the `autoplay` attribute - that would pull all six
files (~76 MB) on every page load. Until a clip is reached it stays at
`preload="metadata"` with a `#t=0.1` media fragment on its `<source>`, which makes the
browser fetch only the header and seek to the first frame, so it still shows a real
thumbnail. Keep the `#t=0.1` suffix when swapping a clip, or the thumbnail goes black.
With JavaScript disabled the clips remain thumbnails with working controls.

To shrink the files, re-encode in place and keep the filenames:

```bash
ffmpeg -i in.mp4 -vcodec libx264 -crf 28 -preset slow -movflags +faststart -an out.mp4
```

`-movflags +faststart` matters for web playback and for the thumbnail trick above;
`-an` drops the (silent) audio track.

## Acknowledgments

Built on the [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template),
adopted from the [Nerfies](https://nerfies.github.io/) project page.

## Website License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
