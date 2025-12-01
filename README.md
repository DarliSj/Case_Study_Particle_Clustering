# Modeling Particle Cluster Distributions using Voronoi Tessellation and General Additive Models

### Project Overview
This project studies how turbulence parameters affect the distribution of particle cluster volumes in simulated fluid flows. Using data provided by the Duke Civil and Environmental Engineering Department, I analyzed simulation results run under varying conditions determined by three physical parameters: Reynolds number ($Re$), Froude number ($Fr$), and Stokes number ($St$).

The primary goals were to build predictive models for the mean, standard deviation, skewness, and kurtosis of particle distributions and to interpret how these parameters affect key distribution metrics, analyzing for potential non-linear and interaction effects.

### Methodology
To align with the project goals, I transformed raw moments into central moment response variables and log-transformed them to protect against the distorting effect of outlier observations.

**1. Inference: General Additive Models (GAM)**
* Developed GAMs to interpret relationships, fitting smooth terms to capture the nonlinear relationship between particle inertia ($St$) and each response.
* Utilized **Restricted Maximum Likelihood (REML)** to automatically choose the optimal smoothness penalty, effectively "tuning" the model to prevent fitting overly complex curves to noise.
* Confirmed model reliability using `gam.check()` diagnostics and ensured basis dimensions were sufficiently large.

**2. Prediction: Random Forest (RF)**
* Selected a Random Forest model for its flexibility to predict distribution parameters from unobserved $Re$ and $Fr$ parameters.
* Engineered a rich, 10-variable feature set including log-transformed predictors and pre-calculated, explicit interactions to allow the algorithm to find the most predictive relationships.
* Tuned hyperparameters (600 trees, `mtry` of 3, `min.node.size` of 4) to stabilize results and decorrelate trees.

**Bias Correction**
* Applied a **Duan smearing factor** to correct for re-transformation bias when converting log-transformed predictions back to the original scale.


### Key Findings
* **Mean Cluster Volumes:** Driven mostly by turbulence ($Re$). The analysis shows that increasing turbulence has a powerful negative relationship with mean particle concentration, nearly eliminating clustering at higher $Re$ values.
* **Variance, Skewness, & Kurtosis:** Driven by a complex interplay of all three parameters. A substantial interaction effect was found between $Re$ and $Fr$, indicating that the impact of gravity on clustering depends on the turbulence level.
* **Stokes Number:** Key distribution parameters depends on $St$ through a positive, non-linear relationship.
* **Model Accuracy:** The Random Forest model proved "exceptionally predictive," achieving high OOB $R^2$ values ($>0.94$) across all moments, confirming the model captured complex physical relationships without significant overfitting.


## Files 

* .qmd file has all the code and written insights after codechunks.
* .csv files are named accordingly
