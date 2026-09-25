# Bi-temporal Image-driven Acute Stroke Evolution Analysis — project page

Project page for the IEEE BHI 2026 submission

> **Bi-temporal Image-driven Acute Stroke Evolution Analysis**
> Md Sazidur Rahman, Kjersti Engan, Kathinka Dæhli Kurz, Mahdieh Khanmohammadi
> University of Stavanger · Stavanger University Hospital

**Code:** https://github.com/yokko123/bi-temporal-ctp-dwi-code

> ⚠️ **Private / unlisted.** The paper is under review, so this repository and
> the page are kept private. The page sets `robots: noindex, nofollow`.
> See [Going public later](#going-public-later).

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
static/images/paper/          the four paper figures
static/images/favicon.ico
```

One column, greyscale only, no scripts and no external CSS or JS beyond the
Inter webfont. Alternating full-width bands give the page its rhythm: white
behind the header, the teaser figure and the results, a light grey (`#f7f7f7`)
behind the abstract and the BibTeX.

Sections:

- Title, authors, and the Paper / Code links
- Framework overview (Fig. 1)
- 01 — Abstract
- 02 — Results, the four region-pair comparisons plus Figs. 2–4
- 03 — BibTeX

Run it locally with:

```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

### Figures

Re-extracted from the manuscript PDF and composited onto white. The originals
had their alpha channel flattened onto black, which left the panel titles and
legends black-on-black and unreadable.

The `<img>` URLs carry a `?v=` version. Bump it whenever you replace a figure
in place, otherwise browsers keep serving the copy they already cached.

## Going public later

When the paper is accepted:

- update `note = {Under review}` in the BibTeX and the "Under review" line under
  the authors in `index.html`,
- replace the `Paper (on publication)` placeholder with the PDF / arXiv / DOI
  link (the **Code** link is already live),
- change `<meta name="robots" ...>` to `index, follow`,
- drop the footer line about the page being private,
- make both repositories public and enable GitHub Pages.

## License

[MIT](LICENSE) for the page itself. The figures are from the manuscript; see the
LICENSE file.
