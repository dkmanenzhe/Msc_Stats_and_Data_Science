# Writer identification and matching

STA5073Z (Data Science for Industry), Assignment 2.
Dakalo Manenzhe (MNNDAK002) and Troy Bisnath (BSNTRO001).

A CNN that identifies which of 20 writers wrote a digit, and a Siamese network that
decides whether two digits were written by the same person, trained on 25,000 simulated
28 x 28 images of the digits 0–4.

- **Website:** https://dkmanenzhe.github.io/Msc_Stats_and_Data_Science/
- **PDF report:** https://dkmanenzhe.github.io/Msc_Stats_and_Data_Science/STA5073Z_Assignment2.pdf

## Repository contents

| Path | Contents |
|---|---|
| `STA5073Z_Assignment2.qmd` | The report: a reproducible Quarto document with all text and code. |
| `_quarto.yml` | Website settings. The site is rendered into `docs/`. |
| `titlepage.tex`, `UCT_Logo.jpg` | Cover page of the PDF version. |
| `title-block.html`, `cover.css` | Cover page of the website version. |
| `data/handwriting.rds` | The assignment data. |
| `results/` | Saved model results, written by the report's code. |
| `images/` | Image grids, written by the report's code. |
| `docs/` | The rendered website served by GitHub Pages (`index.html` is the home page). Do not edit by hand. |
| `GIT_WORKFLOW.md` | How we work with branches, pull requests and GitHub Pages. |

## Reproducing the report

Requirements: R (4.3 or later) with the packages `keras3`, `dplyr`, `knitr` and `rmarkdown`;
a working keras3/TensorFlow installation (`keras3::install_keras()`); Quarto; and a LaTeX
installation for the PDF (for example `quarto install tinytex`).

From a terminal in the repository folder:

```bash
# Rebuild the website and PDF from the saved results (about a minute)
quarto render

# Retrain every model from scratch, then rebuild (about 25 minutes on a laptop CPU)
quarto render -P retrain:true
```

With the default `retrain: false`, models are trained only if the files in `results/` are
missing. Every number, table, figure and result-dependent sentence in the report is computed
from the results, so the text follows the results after a retrain. Retraining on a different
computer can change the numbers slightly.
