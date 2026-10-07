# Bi-temporal Image-driven Acute Stroke Evolution Analysis — project page

Project page for

> **Bi-temporal Image-driven Acute Stroke Evolution Analysis**
> Md Sazidur Rahman, Kjersti Engan, Kathinka Dæhli Kurz, Mahdieh Khanmohammadi
> University of Stavanger · Stavanger University Hospital

**Live page:** https://yokko123.github.io/bi-temporal-ctp-dwi/
**Code:** https://github.com/yokko123/bi-temporal-ctp-dwi-code
**Code DOI:** [10.5281/zenodo.23209370](https://doi.org/10.5281/zenodo.23209370)

**Accepted at IEEE BHI 2026.** The paper is not yet on IEEE Xplore, so the
Paper button is still a placeholder; see [Remaining steps](#remaining-steps).

## What the paper does

Admission CT perfusion (CTP) estimates the ischemic core and penumbra, and
follow-up DWI defines the final infarct. Existing work treats these as
segmentation or prediction targets and so says little about *how* penumbral
tissue with similar admission appearance goes on to recover or infarct.

This work registers the two time points and intersects their labels into six
outcome-aware ROI classes, then asks whether admission CTP already separates
tissue by its eventual fate.

| Class | Paper | Admission (T₁) | Outcome (T₂) |
|---|---|---|---|
| `core_fi` | ROI<sup>fi</sup><sub>c</sub> | core | infarcted |
| `core_brain` | ROI<sup>b</sup><sub>c</sub> | core | salvaged |
| `pen_fi` | ROI<sup>fi</sup><sub>p</sub> | penumbra | infarcted |
| `pen_brain` | ROI<sup>b</sup><sub>p</sub> | penumbra | salvaged |
| `clb_brain` | ROI<sup>b</sup><sub>CLB</sub> | contralateral healthy | healthy |
| `nhb_fi` | ROI<sup>fi</sup><sub>NHB</sub> | non-hypoperfused | infarcted |

Headline results: salvaged and infarcted penumbra separate consistently
(∆̃<sub>cos</sub> = 0.146, p < 0.05), core tissue barely separates by subsequent
fate, and the largest separation is between initially non-hypoperfused tissue
that later infarcted and healthy contralateral brain (∆̃<sub>cos</sub> = 0.460).
The same pattern holds on ISLES'24.

## This repository

Page only. The preprocessing, feature-extraction and analysis code lives in
[bi-temporal-ctp-dwi-code](https://github.com/yokko123/bi-temporal-ctp-dwi-code).

```
index.html                    the whole page; styles are inlined
static/images/paper/          the framework and bubble-plot figures
static/interactive/           the two t-SNE figures, as Plotly pages
static/images/favicon.svg     tab mark: the T1 n T2 intersection
static/images/favicon.ico     fallback for browsers without SVG icons
static/images/apple-touch-icon.png
```

One column. Inter for text, Source Serif 4 for the display title, and a single
teal accent (`#0d7684`) on section numbers, links, buttons and the table rules;
everything else is greyscale. Full-width bands alternate white and `#f6f8f8`
end to end, and a dark variant follows `prefers-color-scheme`. The only script
on the page is Plotly, loaded from a CDN inside the two t-SNE iframes.

The figures are drawn on white and contain medical imagery that must not be
inverted, so in dark mode they stay white plates. They sit on a tinted band with
an explicit rim (`--plate-edge`) and a soft halo, so the white reads as a
deliberate plate rather than merging with the page in light mode or glaring off
it in dark mode.

Sections:

- Title, authors, and the Paper / Code / DOI buttons
- Framework figure as the hero
- 01 — Abstract
- 02 — Method, the six ROI classes
- 03 — Results, all three result tables, the two interactive t-SNE figures and
  the bubble plot
- 04 — BibTeX

The six ROI classes are listed with a small square marker rather than a colour
key: hollow means the tissue survived, filled means it went on to infarct.

Run it locally with:

```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

### Figures

The framework and bubble-plot figures were re-extracted from the manuscript PDF
and composited onto white; the originals had their alpha channel flattened onto
black, which left the panel titles and legends unreadable.

Fig. 2 is coloured by tissue fate with marker shape per class; Fig. 4 uses the
six-class palette from the Fig. 1 legend, matching the paper.

The two t-SNE figures are interactive Plotly pages rather than the paper's PNGs,
regenerated from the cohort feature tables with the same projection recipe as
`bitemporal.figures.tsne_embedding` in the code repository. They carry **no
patient identifiers**: hover text shows only the ROI class, since this page is
public. Coordinates are stored as base64 typed arrays, so both files together
are under 0.5 MB.

Regenerate them with the script kept alongside the analysis code; they are not
rebuilt by anything on this page.

The `<img>` URLs carry a `?v=` version. Bump it whenever you replace a figure
in place, otherwise browsers keep serving the copy they already cached.

## Remaining steps

Done on acceptance: `robots` is now `index, follow`, the under-review notices
and the private-preview footer are gone, and the BibTeX carries the camera-ready
venue.

Done since: the code repository is public and archived on Zenodo
([10.5281/zenodo.23209370](https://doi.org/10.5281/zenodo.23209370), v1.0), and
the page carries a DOI button.

Still open:

- **This repository is still private**, although its Pages site is public. Make
  it public too if you want the page source visible.
- **When the paper appears on IEEE Xplore**, replace the
  `Paper (IEEE Xplore, soon)` placeholder in `index.html` with a live link, and
  add the `doi` plus page numbers to the BibTeX and to `CITATION.cff`, dropping
  `note = {In press}` / `notes: In press`.
- **Check the venue string** against the camera-ready instructions. The BibTeX
  uses `2026 IEEE-EMBS International Conference on Biomedical and Health
  Informatics (BHI)`.
- **Check the figures** still match the camera-ready. They were extracted from
  the submitted PDF; if any changed during revision, re-extract and bump the
  `?v=` on the `<img>` URLs.

## License

[MIT](LICENSE) for the page itself. The figures are from the manuscript; see the
LICENSE file.
