# Gaia DR3 Stellar Cluster Analysis

An exploratory **data analysis and statistical modelling project** using Gaia DR3 to investigate the astrometric, spatial, and statistical properties of Galactic stellar clusters.

The project combines **large-catalogue data exploration, data cleaning and filtering, statistical hypothesis testing, correlation analysis, uncertainty estimation, model fitting, Bayesian inference, and scientific visualization**. Although the application is astrophysical, the workflow demonstrates transferable data-analysis skills for working with large, structured datasets.

## Contents

- [Project overview](#project-overview)
- [Data](#data)
- [Data analysis focus](#data-analysis-focus)
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

This repository contains **three complementary analyses**:

1. **Statistical Analysis of Stellar Populations in Gaia DR3 Clusters** — membership, distributions, subgroup comparisons, correlations, and statistical testing.
2. **Stellar Density Profiles and King Model Fitting** — radial aggregation, model fitting, goodness-of-fit, and uncertainty estimation.
3. **Bayesian Distance Inference and MCMC Modeling** — prior sensitivity, posterior inference, and MCMC estimation of cluster-model parameters.

Together, the notebooks form an end-to-end portfolio project covering **data exploration, preprocessing, statistical inference, model fitting, uncertainty estimation, Bayesian methods, and visualization**.

---

## Data

The main dataset is:

`gaiadr3_cluster_stars.fits`

It is a FITS binary table containing approximately **1.29 million Gaia DR3 sources** with cluster membership information and 56 catalogue columns.

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


### Data preparation

- Loaded and explored a large FITS catalogue using **Astropy**
- Selected relevant catalogue columns for downstream analysis
- Filtered sources using cluster membership probability
- Created high- and low-confidence samples for comparison
- Constructed spatial subsets using right ascension and declination
- Calculated derived quantities such as radial distance from the cluster centre

### Exploratory data analysis

- Examined distributions of parallax, proper motion, magnitude, and colour
- Compared stellar populations across spatial and membership-probability groups
- Investigated relationships between cluster-level summary statistics
- Used transformations and alternative statistical measures to test the robustness of observed relationships

### Statistical analysis

- Applied two-sample statistical tests to compare subsamples
- Calculated **Pearson and Spearman correlations**
- Compared raw and logarithmically transformed variables
- Used chi-square statistics for model fitting and goodness-of-fit assessment
- Applied **bootstrap resampling** to estimate parameter uncertainties

### Statistical modelling

- Fitted radial stellar-density profiles with a **King model**
- Estimated model parameters and associated uncertainties
- Compared radial profiles of different stellar subpopulations
- Extended the analysis to **Bayesian distance inference**
- Used different prior assumptions and sample sizes to investigate posterior sensitivity
- Used **MCMC** to estimate posterior distributions for King-model parameters

### Visualization and interpretation

The notebooks use visualizations to support the analysis, including distributions, astrometric comparisons, spatial maps, radial density profiles, correlation plots, model fits, residuals, MCMC diagnostics, and posterior distributions.


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

**Data-analysis skills:** exploratory data analysis, filtering, feature selection, statistical testing, correlation analysis, subgroup comparison, and visualization.

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

**Data-analysis skills:** feature engineering, aggregation/binning, nonlinear model fitting, goodness-of-fit analysis, bootstrap uncertainty estimation, and model evaluation.

---

### 3. Bayesian Distance Inference and MCMC Modeling

[`notebooks/gaia_cluster_bayesian_inference_mcmc.ipynb`](notebooks/gaia_cluster_bayesian_inference_mcmc.ipynb)

This notebook extends the project from classical statistical analysis to Bayesian inference.

The analysis includes:

- Bayesian distance inference from Gaia parallaxes;
- comparison of a uniform prior with an exponentially decreasing distance prior;
- investigation of prior sensitivity using both the full sample and a smaller 10-star sample;
- estimation of posterior modes and credible intervals;
- King-profile modelling using a chi-square likelihood;
- MCMC parameter estimation using `emcee`;
- posterior and trace analysis;
- power-spectrum diagnostics;
- visualization of posterior distributions using `corner`.

Representative results include:

- full-sample posterior mode of approximately **1.558 kpc** under the uniform-prior analysis;
- 10-star sample posterior mode of approximately **1.498 kpc** under the exponentially decreasing prior;
- King-model minimum chi-square of approximately **15.22 for 23 degrees of freedom**, corresponding to a goodness-of-fit of approximately **0.887**;
- noticeable parameter correlations in the MCMC posterior, including a relationship between tidal radius and cluster mass.

**Data-analysis skills:** probabilistic modelling, prior sensitivity analysis, posterior inference, MCMC, uncertainty quantification, diagnostic analysis, and interpretation of parameter correlations.

---

## Key findings

- **Membership probability separates distinct astrometric populations.** High-probability members are generally more concentrated in astrometric parameter space than lower-probability candidates.
- **Parallax is comparatively homogeneous within the analysed clusters**, while several spatial subsamples show differences in proper motion and colour.
- **Cluster-level properties show measurable relationships**, including a relationship between mean parallax and angular size.
- **Correlation results depend on the statistical treatment.** Pearson vs. Spearman coefficients and raw vs. logarithmically transformed quantities can give different perspectives.
- **The King model provides a good description of the analysed radial density profile**, with the reported fit giving a reduced chi-square below unity and a high goodness-of-fit probability.
- **Bootstrap and chi-square analyses provide complementary uncertainty estimates** for the fitted King-model parameters.
- **Bayesian distance estimates are sensitive to prior assumptions and sample size**, illustrating an important consideration when drawing inferences from noisy astrometric measurements.
- **The MCMC analysis reveals posterior parameter correlations** and provides a probabilistic description of uncertainty in the fitted cluster model.
- **Subpopulation comparisons provide evidence that some stellar properties vary across the cluster field**, particularly proper motion and colour in selected samples. These results are exploratory.

---

## Technologies

### Python ecosystem

- **Python**
- **NumPy**
- **Pandas**
- **SciPy**
- **Astropy**
- **Matplotlib**
- **lmfit**
- **emcee**
- **corner**
- **Jupyter Notebook**

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
---

