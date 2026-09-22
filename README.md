# Gaia DR3 Stellar Cluster Analysis

An exploratory analysis of the **astrometric, spatial, and statistical properties of Galactic stellar clusters** using data from the **Gaia Data Release 3 (Gaia DR3)**.

The project combines catalogue-level exploratory data analysis with statistical modelling to investigate cluster membership, spatial structure, stellar-population differences, and correlations between global cluster properties.

## Contents

- [Project overview](#project-overview)
- [Data](#data)
- [Notebooks](#notebooks)
- [Analysis](#analysis)
- [Key findings](#key-findings)
- [Technologies](#technologies)
- [Repository structure](#repository-structure)
- [How to run](#how-to-run)
- [Caveats and limitations](#caveats-and-limitations)

---

## Project overview

**Gaia** is an ESA mission that has been mapping the positions, distances, and motions of stars in the Milky Way since 2014. Gaia DR3 provides measurements for more than a billion astronomical sources, including positions, parallaxes, and proper motions.

**Stellar clusters** are groups of stars that formed from a common environment and therefore provide useful laboratories for studying stellar populations and Galactic structure. Gaia's astrometric measurements make it possible to identify cluster members and investigate their spatial and kinematic properties.

A central challenge is distinguishing genuine cluster members from foreground and background stars along the same line of sight. The catalogue used in this project includes a **membership probability (`Prob`)** for each source, which is used to separate higher- and lower-confidence members.

This repository contains two complementary analyses:

1. **Statistical Analysis of Stellar Populations in Gaia DR3 Clusters**  
   Investigates membership probabilities, spatial variations in stellar properties, cluster-level correlations, and the sensitivity of correlations to statistical methodology.

2. **Stellar Density Profiles and King Model Fitting**  
   Constructs a radial stellar-density profile for a cluster, fits a King model, estimates parameter uncertainties, and compares the radial structure of different stellar subpopulations.

Together, the notebooks form a small end-to-end astronomical data-analysis portfolio project, covering data exploration, statistical inference, model fitting, uncertainty estimation, and scientific visualization.

---

## Data

The main dataset is:

`gaiadr3_cluster_stars.fits`

It is a FITS binary table containing approximately **1.29 million Gaia DR3 sources** with cluster membership information and 56 catalogue columns.

The dataset is **not included in this repository because of its size (~840 MB)**.


The file is not committed to this repository because of its size (~840 MB). It can be downloaded from [Google Drive](https://drive.google.com/file/d/1YXb91oXz8KUJpgZilIxznwHMRBtfZj4y/view?usp=sharing).

### Main parameters

| Parameter | Description | Units |
|---|---|---|
| `RAdeg` | Right ascension | deg |
| `DEdeg` | Declination | deg |
| `Plx` | Parallax | mas |
| `pmRA` | Proper motion in right ascension | mas/yr |
| `pmDE` | Proper motion in declination | mas/yr |
| `Gmag` | Gaia G-band magnitude | mag |
| `BP-RP` | Gaia colour index | mag |
| `Prob` | Cluster membership probability | 0–1 |

---

## Notebooks

### 1. Statistical Analysis of Stellar Populations in Gaia DR3 Clusters

[`notebooks/gaia_cluster_analysis.ipynb`](notebooks/gaia_cluster_analysis.ipynb)

This notebook explores how stellar properties vary within and between Gaia DR3 stellar clusters.

The analysis includes:

- comparison of high- and low-probability members in astrometric parameter space;
- spatial subdivision of high-confidence cluster members using RA and Dec;
- comparison of parallax, proper motion, magnitude, and colour distributions;
- two-sample statistical tests between spatial subsamples;
- calculation of cluster-level summary statistics;
- exploration of correlations between global cluster properties;
- comparison of Pearson and Spearman correlation coefficients;
- investigation of the effect of logarithmic transformations.

---

### 2. Stellar Density Profiles and King Model Fitting

[`notebooks/stellar_cluster_density_king_model_project.ipynb`](notebooks/stellar_cluster_density_king_model_project.ipynb)

This notebook focuses on the radial structure of a stellar cluster.

The analysis includes:

- estimation of the cluster centre from stellar coordinates;
- calculation of stellar radial distances;
- construction of a radial surface-density profile;
- fitting of a King density model;
- estimation of central density, core radius, and tidal radius;
- chi-square-based parameter uncertainty analysis;
- bootstrap resampling for additional uncertainty estimates;
- comparison of density profiles for different stellar subpopulations.

The notebook uses a King-profile model to describe the projected radial density distribution and evaluates the quality and robustness of the resulting fit.


## Key findings

- **Membership probability separates distinct astrometric populations.** High-probability members are generally more concentrated in astrometric parameter space than lower-probability candidates.

- **Parallax is comparatively homogeneous within the analysed clusters**, while several spatial subsamples show differences in proper motion and colour. These differences may reflect a combination of intrinsic cluster structure, stellar populations, observational effects, or reddening.

- **Cluster-level properties show measurable relationships.** In particular, mean parallax and angular size exhibit a relationship consistent with the geometric effect that nearby clusters can appear larger on the sky.

- **Correlation results depend on the statistical treatment.** Comparing Pearson and Spearman coefficients, as well as raw and logarithmically transformed quantities, demonstrates the importance of checking the robustness of correlations rather than relying on a single statistic.

- **The King model provides a good description of the analysed radial density profile**, with the reported fit giving a reduced chi-square below unity and a high goodness-of-fit probability.

- **Bootstrap and chi-square analyses provide complementary uncertainty estimates** for the fitted King-model parameters.

- **Subpopulation comparisons provide evidence that some stellar properties vary across the cluster field**, particularly proper motion and colour in selected samples. These results are exploratory and require further investigation to establish their physical origin.

---

## Technologies

- **Python**
- **NumPy**
- **Pandas**
- **SciPy**
- **Astropy**
- **Matplotlib**
- **lmfit**
- **Jupyter Notebook**
- **FITS astronomical data**

### Methods

- Exploratory data analysis
- Data filtering and preprocessing
- Statistical hypothesis testing
- Pearson and Spearman correlation analysis
- Radial binning
- Least-squares / chi-square model fitting
- Bootstrap resampling
- Uncertainty estimation
- Scientific visualization

---

## How to run

Clone the repository:

```bash
git clone https://github.com/<your-username>/gaia-cluster-analysis.git
cd gaia-cluster-analysis
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

Place the downloaded Gaia DR3 FITS dataset in the location expected by the notebooks.

Launch Jupyter:

```bash
jupyter notebook
```

---

## Caveats and limitations

Several aspects of the analysis are exploratory.

- Membership probability is used as supplied by the cluster catalogue and is not independently recalculated.
- The spatial subsamples are defined relative to the mean RA and Dec, which is a simple division and does not necessarily correspond to physically distinct regions.
- The t-tests rely on assumptions that may not be fully satisfied by all Gaia observables.
- Multiple statistical comparisons are performed without a multiple-testing correction.
- The number of clusters used in the cluster-level correlation analysis is limited, so correlation coefficients may be sensitive to individual objects.
- Pearson and Spearman correlations describe statistical association and do not establish causation.
- The King model is an empirical description of the projected density profile and does not by itself establish the physical origin of the measured structure.
- The uncertainty estimates depend on the assumptions of the fitting and bootstrap procedures.

The results should therefore be interpreted as an exploratory investigation and a foundation for more detailed cluster-structure analysis.
---
