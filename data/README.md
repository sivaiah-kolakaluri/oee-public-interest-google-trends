# Data

This folder holds the Google Trends CSV exports used by `Google_Trends_OEE_Analysis.ipynb`.
They are not included in the repository (Google Trends' terms discourage mass redistribution of raw exports); reproduce them directly from Google Trends:

1. Go to https://trends.google.com/trends/explore
2. Search for each topic below, one at a time
3. Set the date range to **1/1/2004 – 12/31/2025**
4. Set region to **Worldwide**
5. Download the CSV ("Interest over time" panel, download icon)
6. Save it under the exact filename below (the notebook reads these names directly)

| Topic | Expected filename |
|---|---|
| Artificial Intelligence | `multiTimeline(AI).csv` |
| Blockchain | `multiTimeline(BC).csv` |
| Machine Learning | `multiTimeline(ML).csv` |
| Virtual Reality | `multiTimeline(VR).csv` |
| Cryptocurrency | `multiTimeline(CC).csv` |
| Cybersecurity | `multiTimeline(CS).csv` |
| NFT | `multiTimeline(NFT).csv` |
| Metaverse | `multiTimeline(MV).csv` |
| ChatGPT | `multiTimeline(CG).csv` |
| Cloud Computing | `multiTimeline(CCM).csv` |

Each CSV has one header row (skipped by the notebook via `skiprows=1`) followed by `Month, <search interest 0-100>` rows.

Note: the notebook itself trims every series to 1 Jan 2004 – 31 Dec 2025 before analysis (see the main `README.md`'s Method notes), so a CSV exported with a wider date range than requested above is not a problem — any months outside the documented window are dropped automatically rather than silently included.
