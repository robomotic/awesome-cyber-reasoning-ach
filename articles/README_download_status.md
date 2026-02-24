# Download status for Bayesian forensics references

This folder contains automated downloads for the references listed in the main document.

## What is included

- Downloaded PDF files where direct access was available.
- Downloaded HTML landing pages where PDF access is restricted.
- Two CSV manifests:
  - `download_manifest.csv` (first pass)
  - `download_manifest_retry.csv` (retry pass)

## Status summary

### Successfully downloaded as PDF

- A1_Kwan_2008_Reasoning_About_Evidence_Using_BN.pdf
- B1_Liu_PNFM_NIST_PDF.pdf
- B2_PNFM_CSRC_PDF.pdf
- B3_PNFM_GMU_PDF.pdf
- C1_Pappaterra_2018_retry_https.pdf
- C2_Murray_2016_Memory_Forensics_Triage.pdf

### Downloaded as HTML (landing/open pages)

- A2_Schneps_2018_Ranking_Impact_Tests_BN.html
- A3_Casey_Pollitt_2021_Quantitative_Evaluation_DFI.html
- A5_Fenton_Neil_Berger_2016_Legal_BN.html
- B4_Nisioti_2022_2023_ScienceDirect_retry.html
- B5_Nisioti_Open_PDF_retry.html
- C3_DigitalForensics_PNFM_Blog_retry_root.html
- C4_BayesForensics_GitHub.html
- C6_ACM_DOI_retry_via_doi_org.html
- C7_ScienceDirect_retry_pdfft.html

### Blocked/empty via automated download

- A4_JDFSL_Admissibility_BN_Digital_Evidence.html (2 bytes)
- A4_JDFSL_Admissibility_BN_Digital_Evidence_retry.html (0 bytes)
- C5_Korb_Nicholson_Bayesian_AI_SemanticScholar.html (2 bytes)
- C5_Korb_Nicholson_Bayesian_AI_SemanticScholar_retry.html (0 bytes)

## Why some items are not full papers

Some domains (notably ScienceDirect/ACM and a few portals) enforce anti-bot checks, cookie/session requirements, or institutional paywall controls. The script can save landing pages, but direct PDF retrieval may require a browser session.

## Manual completion suggestion

Open blocked/HTML items in a browser and use "Download PDF" where available. Keep the same filename stem so your local set remains consistent.

## Suggested manual downloads (priority)

These are the highest-priority items to download manually because automated retrieval did not produce usable PDFs:

1. **C6 ACM paper**
  - URL: https://dl.acm.org/doi/10.1145/3769126.3769231
  - Save as: `C6_ACM_DOI_10_1145_3769126_3769231.pdf`


## Optional note on C5 (book reference)

- **C5** is a reference page (Semantic Scholar), not necessarily a direct downloadable full-text source.
- If you want the actual book/chapter PDF, search by title and edition and save bibliographic metadata instead if full text is unavailable.
