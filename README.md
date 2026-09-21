# Gaia DR3 Stellar Cluster Membership Analysis

Analysis of stellar parameter distributions for members and candidates
of Galactic stellar clusters using Gaia Data Release 3.

## Contents
- `notebooks/gaia_cluster_analysis.ipynb` — main analysis
- `data/gaiadr3_cluster_stars.fits` — input catalog (or download instructions)
- `requirements.txt` — Python dependencies

## Summary of findings
- High-probability members cluster tightly in 5-D astrometric parameter space;
  low-probability candidates are more scattered.
- BP-RP color shows statistically significant differences between RA-split
  subsamples in several clusters; parallax and proper motion do not.


## How to run
```bash
pip install -r requirements.txt
jupyter notebook notebooks/gaia_cluster_analysis.ipynb
```

## Data

The analysis expects `gaiadr3_cluster_stars.fits` in this directory.

This file is not committed to the repository because of its size
(~840 MB). 
