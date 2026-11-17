# Open-Ended Evolution of Public Interest

Code and analysis for *Open-Ended Evolution of Public Interest: A Longitudinal Computational Analysis Using Google Trends Data, 2004–2025* — an MSc dissertation (Aston University, 2026) testing whether public search interest in technology topics behaves as an open-ended evolutionary system, following the criteria of Packard et al. (2019).

**Paper draft:** [link to arXiv preprint — add once posted]
**Dissertation:** Kolakaluri, S. (2026). *Open-Ended Evolution of Public Interest.* MSc dissertation, Aston University. Supervised by Dr James M. Borg.

## Summary

Using 22 years of worldwide Google Trends data (January 2004 – December 2025) for ten technology topics, this analysis applies:

- **Shannon Entropy** as a measure of diversity of public attention across topics each year
- A **novelty-detection algorithm**, flagging a topic as novel when its interest crosses a threshold having been near-zero in every prior year

**Headline results** (full ten-topic set):

| Metric | Result |
|---|---|
| Shannon Entropy, 2004 → 2023 peak | 1.03 → 2.21 (+115%), 96% of theoretical maximum ln(10) ≈ 2.30 |
| Novelty events detected | Four first-emergence events from near-zero prior interest — 2008 (Cloud Computing), 2017 (Blockchain, Cryptocurrency), 2021 (NFT, Metaverse), 2023 (ChatGPT) — plus three repeated crossings the following year as each emergence continued to build (2018, 2022, 2024) |
| Saturation | None detected through 2025 |

These results are provisionally consistent with two of the three OEE criteria proposed by Packard et al. (2019) - ongoing novelty generation and increasing diversity over time - while the third, no fixed upper bound on diversity, is explicitly reported as not established: a finite observation window, and a fixed ten-topic measurement instrument, cannot demonstrate the absence of a ceiling. See the paper's Table 3 and Limitations section for the full evaluation, including why these findings should be read as exploratory rather than statistically validated (no null-model comparison has yet been performed) and why the ten topics' individually-normalised Google Trends scores are not strictly comparable to one another.

## Repository structure

```
.
├── Google_Trends_OEE_Analysis.ipynb   Main analysis notebook (run top to bottom)
├── data/                               Google Trends CSV exports (see data/README.md)
├── outputs/                            Generated charts (created when the notebook runs)
├── requirements.txt                    Python dependencies
├── LICENSE                             MIT License
└── README.md                           This file
```

## Reproducing the analysis

1. Clone the repository and install dependencies:
   ```bash
   git clone https://github.com/sivaiah-kolakaluri/oee-public-interest-google-trends.git
   cd oee-public-interest-google-trends
   pip install -r requirements.txt
   ```
2. Place the Google Trends CSV exports in `data/` (see `data/README.md` for exact export settings — worldwide scope, monthly resolution, 2004–2025, one file per topic).
3. Run `Google_Trends_OEE_Analysis.ipynb` top to bottom in Jupyter.

The notebook has two parts: a preliminary 5-topic validation pass (Part A), and the full 10-topic analysis reported in the paper (Part B).

## Method notes

- Google Trends scores are **relative** (0–100 within the selected time range and region), not absolute search volumes.
- The main analysis uses `fillna(0)` rather than `dropna()` when merging topics that emerged partway through the window: a term that had not yet been coined (e.g. "ChatGPT" before November 2022) genuinely has zero search interest, not missing data. An earlier version of this pipeline used `dropna()`, which discarded every month where any later-emerging topic lacked a value, artificially flattening the early entropy curve — see the dissertation's methodology section for the full discussion.
- Novelty thresholds (current-year average > 10, all prior years < 2) were agreed with the dissertation supervisor as a conservative, asymmetric rule that avoids flagging topics that merely fluctuate at moderate levels.
- The notebook trims every loaded series to the documented analysis window (1 Jan 2004 – 31 Dec 2025) before computing entropy or running novelty detection. This is explicit in the code rather than left to the Google Trends export settings alone, so the reported period holds even if a CSV is (re)downloaded later with a wider default range. It also creates `outputs/` on first run if the folder isn't already there, so the notebook runs top to bottom on a fresh clone with no manual setup.

## Reproducibility notes (author-verified)

The full pipeline was re-run end to end against the original ten Google Trends CSVs, starting from a fresh clone of this repository: `pip install -r requirements.txt`, the ten files placed under `data/` with the exact filenames in `data/README.md`, then `Google_Trends_OEE_Analysis.ipynb` executed top to bottom with no manual intervention. It reproduced the entropy values and all ten novelty-flagged topic-year combinations reported in the paper's Table 2 (2008, 2017 x2, 2018, 2021 x2, 2022 x2, 2023, 2024 - seven flagged years, six distinct topics, four first-emergence episodes), confirming the published notebook is self-contained and runs as described.

This check was performed by the authors, not by an independent third party: because Google's terms discourage redistributing raw Trends exports, the CSVs themselves are not included in this repository, so an outside reviewer currently has to re-download them (per `data/README.md`) before they can verify the pipeline end to end for themselves.

A separate epsilon-sensitivity check confirmed that the small constant added before normalising each year's values (`epsilon = 1e-4`, used to avoid `log(0)`) changes the reported entropy by at most 0.0003 in any single year across epsilon values spanning six orders of magnitude (1e-4 to 1e-10) - including years where up to six of the ten topics had zero recorded interest - well below the two-decimal precision reported in the paper.

## Citation

If you use this code or build on this analysis, please cite:

```bibtex
@mastersthesis{kolakaluri2026oee,
  author = {Kolakaluri, Sivaiah},
  title  = {Open-Ended Evolution of Public Interest: A Longitudinal Computational
            Analysis Using Google Trends Data, 2004--2025},
  school = {Aston University},
  year   = {2026}
}
```

## License

MIT — see [LICENSE](LICENSE).

## Contact

Sivaiah Kolakaluri — ksivaiahk@gmail.com
MSc Artificial Intelligence, Aston University
