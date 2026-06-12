# Bi-temporal Image-driven Acute Stroke Evolution Analysis — Project Page

Private project page for the paper **"Bi-temporal Image-driven Acute Stroke Evolution Analysis"**
(Md Sazidur Rahman, Kjersti Engan, Kathinka Dæhli Kurz, Mahdieh Khanmohammadi),
under review at **IEEE BHI 2026**.

> ⚠️ **Private / unlisted.** This repository and page are kept private while the paper is
> under review. The page sets `robots: noindex, nofollow` and the code release is gated
> until publication.

## What's here

- `index.html` — the full single-page site (self-contained; styles are inlined).
- `static/images/paper/` — the four paper figures (Fig. 1–4), extracted from the submitted PDF
  and downsized for the web.
- `static/interactive/` — interactive **Plotly** t-SNE figures (ISLES'24), embedded as
  lazy-loaded iframes:
  - `mjnet_tsne_slice_isles.html`, `mjnet_tsne_patient_isles.html` — mJ-Net deep embeddings
  - `bl_tsne_slice_isles.html`, `bl_tsne_patient_isles.html` — baseline statistical features
- `static/pdfs/bi-temporal-ctp-dwi.pdf` — the submitted manuscript.
- `static/css/`, `static/js/` — Bulma + Font Awesome assets from the
  [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template).

## Page sections

1. Hero (title, authors, links)
2. Framework overview (Fig. 1)
3. Abstract
4. Highlights + headline numbers
5. The six bi-temporal ROI classes (color legend)
6. Results — the four region-pair tests and an interactive, color-coded **Table II**
7. Visual analysis — Fig. 2 (t-SNE FE1–FE4), Fig. 4 (mJ-Net t-SNE), Fig. 3 (bubble plots);
   click any figure to open it full-screen
8. Interactive t-SNE explorer (tabbed Plotly figures)
9. Ablation (Table III) and subgroup (Table IV) analyses
10. BibTeX

## Run locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

The interactive iframes are loaded only when their tab is first opened, so the initial page
stays light despite the ~20 MB of bundled Plotly figures.

## Going public later

When the paper is accepted:
- update `note = {Under review}` in the BibTeX and the venue badge in `index.html`,
- fill in the GitHub **Code** link (currently disabled) and the arXiv/DOI links,
- change `<meta name="robots" ...>` to `index, follow`,
- make the repository public and enable GitHub Pages.
