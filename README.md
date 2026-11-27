# Occlusion-Aware Plot Digitization & Spectral Surrogate Testing

**Live Rendered Report:** [View Quarto HTML Output](https://nnneeeaaalll.github.io/physiological-synchrony-digitization-quantification/)

## Overview
Standard automated plot-digitizing tools rely on linear or spline interpolation across missing segments. When two positively correlated physiological time series are plotted with opaque strokes, occlusion occurs preferentially at shared peaks and troughs—causing standard interpolation to attenuate cross-correlation and distort high-frequency power.

This repository provides a transparent, self-contained Python/Quarto pipeline that:
1. **Digitizes overlapping curves (`Code_Generated_Image.png`)** using RGB chromaticity/luminance thresholding and an explicit **foreground-occlusion prior** (`mal[t] = fem[t]` where the foreground gray stroke obscures the background orange trace), followed by 3-point binomial smoothing (`[0.25, 0.5, 0.25]`) and Z-score standardization.
2. **Evaluates cross-series synchrony** via linear detrending and $N = 1{,}000$ **FFT phase-randomized surrogates** (`phaseScrambleTS`), quantifying Arbitrary Significance (`AS = R / R_99.9%`) while preserving each signal's exact power spectrum and autocorrelation structure.

## Background & Data Provenance
This pipeline demonstrates the analysis workflow on a **figure-level replication** of physiological temperature traces from an unpublished study (`Code_Generated_Image.png`). Because the input here is a rasterized summary plot rather than raw sensor data, minor differences relative to the original raw-data metrics are expected due to pixel quantization and finite stroke thickness during overlapping intervals.

## Repository Contents
* `Temperature_Overview_Panel_A.png` — Panel A from the source figure, showing the windows marked B and C.
* `physiological_synchrony_end_to_end3.py` — Updated standalone Python script.
* `physiological_synchrony_end_to_end.qmd` — Primary Quarto source document combining narrative, extraction code, diagnostic plots, and surrogate testing.
* `physiological_synchrony_end_to_end.ipynb` — Executed Jupyter Notebook with saved inline outputs.
* `Code_Generated_Image.png` — Source figure image used for reproducible extraction.
* `index.html` — Self-contained rendered HTML report served via GitHub Pages.

## Reproduction
```bash
pip install -r requirements.txt
quarto render physiological_synchrony_end_to_end.qmd
