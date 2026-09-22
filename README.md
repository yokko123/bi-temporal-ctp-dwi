# Bi-temporal Image-driven Acute Stroke Evolution Analysis

Project page and code for the IEEE BHI 2026 submission

> **Bi-temporal Image-driven Acute Stroke Evolution Analysis**
> Md Sazidur Rahman, Kjersti Engan, Kathinka Dæhli Kurz, Mahdieh Khanmohammadi

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
tissue by its eventual fate, using statistical, radiomic and deep-learning
feature families.

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

## Repository layout

```
index.html          the project page (self-contained; styles inlined)
static/             paper figures + interactive Plotly t-SNE figures
code/               the implementation - see code/README.md
```

### Code

| Stage | Contents |
|---|---|
| [`code/01_preprocessing/`](code/01_preprocessing) | DICOM → NIfTI, CTP motion correction, CTP/DWI → NCCT registration, SynthStrip, and the six bi-temporal ROI classes |
| [`code/02_features/`](code/02_features) | FE1 baseline statistics, FE2 GLCM radiomics, FE3 mJ-Net embeddings, FE4 nnU-Net embeddings |
| [`code/03_analysis/`](code/03_analysis) | region-pair tests (Table III), ablation (Table IV), subgroups (Table V), figures |
| [`code/demo/`](code/demo) | synthetic cohort so the analysis runs without any data |

```bash
cd code
conda env create -f environment.yml && conda activate bitemporal
python demo/make_synthetic_cohort.py --out-dir demo/data
cd 03_analysis && python run_table3_region_pairs.py --config ../demo/data/config.yaml
```

### Page sections

One column, greyscale only, no scripts. Alternating full-width bands give the
page its rhythm: white behind the header, the teaser figure and the results,
a light grey (`#f7f7f7`) behind the abstract and the BibTeX.

- Title, authors, and the Paper / Code links
- Framework overview (Fig. 1)
- 01 - Abstract
- 02 - Results, the four region-pair comparisons plus Figs. 2-4
- 03 - BibTeX

Run it locally with:

```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

`index.html` is self-contained apart from the figures under
`static/images/paper/` and the Inter webfont. Figures were re-extracted from the
manuscript PDF composited onto white; the earlier copies had their alpha
flattened onto black, which hid the panel titles and legends.

`static/css/`, `static/js/` and `static/interactive/` are left over from the
previous Bulma-based page and are no longer referenced.

## Data

No patient data is in this repository.

* The **local cohort** (n = 109 analysed, of 149) is retrospective hospital data
  and cannot be shared.
* **ISLES'24** (n = 149) is public:
  [isles-24.grand-challenge.org](https://isles-24.grand-challenge.org/)

Stages 01 and 02 read data roots from environment variables; stage 03 reads
paths from a YAML config. Both default to `/path/to/...` placeholders, and
`code/README.md` lists them.

## Going public later

When the paper is accepted:

- update `note = {Under review}` in the BibTeX and the "Under review" line under
  the authors in `index.html`,
- replace the `Paper (on publication)` placeholder with the PDF / arXiv / DOI
  link (the **Code** link is already live),
- change `<meta name="robots" ...>` to `index, follow`,
- drop the footer line about the page being private,
- make the repository public and enable GitHub Pages.

## License

[MIT](LICENSE) for the code in this repository. Third-party components
(mJ-Net, nnU-Net, SynthStrip/SynthSeg, the Academic Project Page Template)
remain under their own licenses; see the LICENSE file.
