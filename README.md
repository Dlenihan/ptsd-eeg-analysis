# EEG Spectral Analysis of PTSD vs Healthy Controls

_Reanalysis of open-access EEG data from Rahmani et al. (2018, PLoS ONE)_

## Overview
This project investigates resting-state EEG differences between individuals with
**Post-Traumatic Stress Disorder (PTSD)** and **healthy controls (HC)** using
**alpha (8–12 Hz)** and **beta (13–30 Hz)** spectral power.  
It complements the original study, which analysed the same dataset using
**Hurst exponent analysis** to characterise temporal dynamics.

**Reference dataset:**  
Rahmani M., Gao C., Robert J., Miller E. L., & Najafizadeh L. (2018).  
_Dynamical Hurst analysis identifies EEG channel differences between PTSD and healthy controls._  
**PLoS ONE 13 (7): e0199144.**  
[https://doi.org/10.1371/journal.pone.0199144](https://doi.org/10.1371/journal.pone.0199144)

---

## Dataset
| Feature | Description |
|----------|--------------|
| **Participants** | 6 PTSD, 6 Healthy Controls |
| **EEG Channels** | 31 scalp electrodes + 1 ECG |
| **Sampling Rate** | 250 Hz |
| **Recording Length** | 130 000 samples (~8.7 min) |
| **Paradigm** | Resting-state EEG (eyes open/closed unspecified) |

Raw EEG text files are not stored in this repository; they can be accessed from
the supplementary materials of the cited publication.

---

## Analysis Workflow
1. **Load and clean EEG data**
   - Read 31 EEG channels from text files; drop ECG.
   - Interpolate or fill small gaps.
2. **Pre-processing**
   - Band-pass filter 1–40 Hz.
   - Set standard 10–20 electrode montage.
3. **Feature extraction**
   - Compute Power Spectral Density (PSD) using MNE-Python.
   - Integrate PSD in alpha (8–12 Hz) and beta (13–30 Hz) bands.
   - Derive both:
     - Per-channel power → for scalp topographies  
     - Global mean power → for group statistics
4. **Statistical comparison**
   - Independent-samples t-tests between groups.
   - Plot bar charts and scalp topomaps.

---

## Results
| Band | *t* | *p* | Interpretation |
|------|----:|----:|----------------|
| **Alpha (8–12 Hz)** | −2.19 | 0.069 | Lower alpha in PTSD (trend) |
| **Beta (13–30 Hz)** | −1.94 | 0.088 | Lower beta in PTSD (trend) |

**Findings**
- PTSD participants show **reduced alpha and beta power**, consistent with
  increased cortical arousal and reduced inhibitory control.
- Spatially, reductions are most evident over **frontal–parietal regions**, in
  line with the original study’s left-frontal Hurst-exponent difference at F3.

---

## Technologies
- Python 3.11  
- [MNE-Python 1.10+](https://mne.tools/stable/index.html)  
- NumPy · pandas · SciPy · Matplotlib · JupyterLab  

---

## Repository Structure
ptsd-eeg-analysis/
├── data/
│   ├── raw/           # raw EEG text files (not tracked)
│   └── processed/
├── notebooks/
│   ├── 01_load_and_clean.ipynb
│   ├── 02_psd_analysis.ipynb
│   └── 03_group_stats_and_topomaps.ipynb
├── outputs/
│   ├── figures/
│   └── results/
├── src/               # helper scripts (loader, plotting)
├── environment.yml
├── README.md
└── .gitignore

---

## Reproducibility
To recreate the environment:

```bash
conda env create -f environment.yml
conda activate eeg_project
jupyter lab

---

Citation

If you use this code or dataset, please cite:

Rahmani M., Gao C., Robert J., Miller E. L., & Najafizadeh L. (2018).
Dynamical Hurst analysis identifies EEG channel differences between PTSD and healthy controls.
PLoS ONE 13 (7): e0199144.
https://doi.org/10.1371/journal.pone.0199144￼

---

Author: Diarmuid Lenihan
Institution: University of Liverpool
Year: 2025
