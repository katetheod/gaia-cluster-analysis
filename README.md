# Gaia DR3 Stellar Cluster Analysis

An exploratory analysis of the physical and astrometric properties of
stars in Galactic open clusters, using data from the Gaia mission's third
data release (Gaia DR3).

## Contents
- [Background](#background)
- [Data](#data)
- [Analysis](#analysis)
- [Key findings](#key-findings)
- [How to run](#how-to-run)
- [Caveats](#caveats)

---

## Background

**Gaia** is an ESA mission that has been mapping the positions, distances,
and motions of stars in the Milky Way since 2014. Its third data release
(Gaia DR3, 2022) contains positions, parallaxes, and proper motions for
more than 1.8 billion sources, freely available through the
[Gaia Archive](https://www.cosmos.esa.int/web/gaia-users/archive).

**Stellar clusters** are groups of stars that formed together and remain
gravitationally bound. Because they share an origin, their members have
similar distances, velocities, and colours — which is exactly what Gaia
measures. Clusters are natural laboratories for testing our understanding
of star formation and stellar evolution.

The catch: when we look at a cluster, we also see foreground and background
stars that happen to line up along the same line of sight. Modern cluster
catalogues solve this by assigning each star a **membership probability**
between 0 and 1. Stars with probability > 0.8 are very likely true members;
lower-probability stars are probably contaminants. This analysis uses that
probability to separate the two populations and to study the structure of
the clusters themselves.

### Parameters used

| Symbol | Meaning | Units |
|--------|---------|-------|
| `RAdeg` | Right ascension (position on sky, like longitude) | deg |
| `DEdeg` | Declination (position on sky, like latitude) | deg |
| `Plx` | Parallax (larger = closer) | mas |
| `pmRA`, `pmDE` | Proper motion (apparent motion across sky) | mas/yr |
| `Gmag` | Gaia G-band brightness | mag |
| `BP-RP` | Colour index (blue minus red) | mag |
| `Prob` | Membership probability | 0–1 |

---

## Data

The analysis uses `gaiadr3_cluster_stars.fits` — a FITS binary table of
~1.29 million Gaia DR3 sources with pre-computed cluster membership
probabilities across 56 columns.

### Download

The file is not committed to this repository because of its size (~840 MB).
It can be downloaded from
[Google Drive](https://drive.google.com/file/d/1YXb91oXz8KUJpgZilIxznwHMRBtfZj4y/view?usp=sharing).

After downloading, place it at:

    data/gaiadr3_cluster_stars.fits

> Google Drive may show a virus-scan warning for files this large.
> Click **Download anyway** to proceed.

---

## Analysis

The notebook is organised into four sections, each addressing a different
question about the structure of stellar clusters.

1. **Do high- and low-probability members trace the same region of
   parameter space?** For four large clusters, members are split by
   membership probability (> 0.8 vs. ≤ 0.8) and their joint distributions
   in 5-D astrometric space are compared using a scatter matrix.

2. **Do physical parameters vary systematically within high-confidence
   members?** For clusters with > 200 high-probability members, stars are
   split by whether they lie above or below the mean RA (and separately,
   mean Dec). Distributions are compared with histograms and two-sample
   t-tests.

3. **How do global cluster properties correlate with each other?** For
   each cluster, mean and standard deviation of parallax and proper
   motion, and spatial size, are computed. A scatter matrix reveals
   pairwise relationships.

4. **Which correlation coefficient is appropriate?** Pearson's `r`
   (linear) and Spearman's `rho` (monotonic) are computed on raw and
   log-transformed data to test how sensitive the conclusions are to
   the choice of method.

---

## Key findings

- **Membership probability is meaningful.** High-probability members
  concentrate near cluster centres in astrometric space; low-probability
  candidates are more scattered.

- **Parallax is homogeneous within clusters, but colour and proper motion
  are not.** Several clusters show significant differences in `BP-RP` and
  proper motion between spatial subsamples — consistent with differential
  reddening or internal dynamics.

- **Cluster-level scaling relations exist, but are partly observational.**
  Nearby clusters appear larger on the sky and more dispersed in parallax
  — a mix of geometric and physical effects.

- **Spearman's rho is the better choice** for these parameters, since
  parallax and proper motion are skewed and bounded.

---

## How to run

```bash
git clone https://github.com/<your-username>/gaia-cluster-analysis.git
cd gaia-cluster-analysis
pip install -r requirements.txt
```

## Data

The analysis expects `gaiadr3_cluster_stars.fits` in this directory.

This file is not committed to the repository because of its size
(~840 MB). The data can be downloaded from
[Google Drive](https://drive.google.com/file/d/1YXb91oXz8KUJpgZilIxznwHMRBtfZj4y/view?usp=sharing).
