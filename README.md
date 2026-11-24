# Search-Interest Emergence and Diversity in Ten Technology Topics, 2004–2025

Code and analysis for *Search-Interest Emergence and Diversity in Ten Technology Topics, 2004–2025: A Descriptive Analysis Motivated by Open-Ended Evolution Theory*, developed from an MSc dissertation (Aston University, 2026). Open-ended evolution (Packard et al., 2019) is used as a motivating lens; this is a descriptive, exploratory analysis and does **not** claim to demonstrate open-endedness.

**Paper draft:** [link to arXiv preprint — add once posted]
**Dissertation:** Kolakaluri, S. (2026). *Open-Ended Evolution of Public Interest.* MSc dissertation, Aston University. Supervised by Dr James M. Borg.

## Summary

Using 22 years of worldwide Google Trends data (January 2004 – December 2025) for ten technology topics, this analysis applies:

- A **Shannon entropy index** of how evenly the ten topics are simultaneously prominent relative to their own historical peaks (not a measure of shares of public attention, since each series is scaled separately by Google Trends)
- An **emergence rule**, flagging a topic when its interest crosses a threshold having been near-zero in every prior year

**Headline results** (full ten-topic set):

| Metric | Result |
|---|---|
| Shannon Entropy, 2004 → 2023 peak | 1.03 → 2.21 (+115%), 96% of theoretical maximum ln(10) ≈ 2.30 |
| Emergence events detected | Four first-emergence events from near-zero prior interest — 2008 (Cloud Computing), 2017 (Blockchain, Cryptocurrency), 2021 (NFT, Metaverse), 2023 (ChatGPT) — plus three repeated crossings the following year as each emergence continued to build (2018, 2022, 2024) |
| Plateau | Entropy eased from 2.21 (2023) to 2.08 (2025); cannot be interpreted as saturation or its absence |

These results are descriptively consistent with two of the three OEE criteria proposed by Packard et al. (2019) - ongoing emergence and increasing diversity over time - while the third, no fixed upper bound on diversity, cannot be assessed: a finite observation window, and a fixed ten-topic measurement instrument, cannot demonstrate the absence of a ceiling. See the paper's Table 3 and Limitations section for the full evaluation, including why these findings should be read as exploratory rather than statistically validated (no null-model comparison has yet been performed) and why the ten topics' individually-normalised Google Trends scores are not comparable in level across topics. That is the main limitation: a calibrated multi-term re-collection (overlapping queries with a common bridge term), a threshold-sensitivity analysis and a null model are the planned follow-up, not results already obtained.

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
- Emergence thresholds (current-year average > 10, all prior years < 2) were agreed with the dissertation supervisor as a conservative, asymmetric rule that avoids flagging topics that merely fluctuate at moderate levels.
- The notebook trims every loaded series to the documented analysis window (1 Jan 2004 – 31 Dec 2025) before computing entropy or running emergence detection. This is explicit in the code rather than left to the Google Trends export settings alone, so the reported period holds even if a CSV is (re)downloaded later with a wider default range. It also creates `outputs/` on first run if the folder isn't already there, so the notebook runs top to bottom on a fresh clone with no manual setup.

## Reproducibility notes (author-verified)

The full pipeline was re-run end to end against the original ten Google Trends CSVs, starting from a fresh clone of this repository: `pip install -r requirements.txt`, the ten files placed under `data/` with the exact filenames in `data/README.md`, then `Google_Trends_OEE_Analysis.ipynb` executed top to bottom with no manual intervention. It reproduced the entropy values and all ten emergence-flagged topic-year combinations reported in the paper's Table 2 (2008, 2017 x2, 2018, 2021 x2, 2022 x2, 2023, 2024 - seven flagged years, six distinct topics, four first-emergence episodes), confirming the published notebook is self-contained and runs as described.

This check was performed by the authors, not by an independent third party: because Google's terms discourage redistributing raw Trends exports, the CSVs themselves are not included in this repository, so an outside reviewer currently has to re-download them (per `data/README.md`) before they can verify the pipeline end to end for themselves.

A separate epsilon-sensitivity check confirmed that the small constant added before normalising each year's values (`epsilon = 1e-4`, used to avoid `log(0)`) changes the reported entropy by at most 0.0003 in any single year across epsilon values spanning six orders of magnitude (1e-4 to 1e-10) - including years where up to six of the ten topics had zero recorded interest - well below the two-decimal precision reported in the paper.

## Citation

If you use this code or build on this analysis, please cite:

```bibtex
@mastersthesis{kolakaluri2026oee,
  author = {Kolakaluri, Sivaiah},
  title  = {Search-Interest Emergence and Diversity in Ten Technology Topics,
            2004--2025: A Descriptive Analysis Motivated by Open-Ended Evolution Theory},
  school = {Aston University},
  year   = {2026}
}
```

## License

MIT — see [LICENSE](LICENSE).

## Contact

Sivaiah Kolakaluri — ksivaiahk@gmail.com
MSc Artificial Intelligence, Aston University
