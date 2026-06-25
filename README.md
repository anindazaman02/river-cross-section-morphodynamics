# River Cross-Section Profile Analysis and Bathymetric Volumetric Modeling

[![Language](https://img.shields.io/badge/Language-R%20%2F%20RStudio-blue?logo=r&logoColor=white)](https://www.r-project.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Project Overview
This repository hosts a specialized hydrological engineering processing pipeline written in R to analyze river channel cross-sections and track long-term morphological adjustments. The script ingests multi-year field survey datasets (Distance and Reduced Level measurements) to map cross-sectional profile lines, extract critical depth baselines, and compute the net cross-sectional geometry using numerical integration methods. 

This framework is highly critical for tracking structural riverbed degradation (scouring), aggradation (siltation), and assessing flood carrying capacities over time.

---

## 📊 Methodological Framework & Engineering Calculations

The R pipeline parses complex geometric profiles through four distinct operations:

### 1. Data Cleaning and Temporal Parsing
* Ingests survey profiles out of localized Excel files (`Cross_SectionRMBR26.xlsx`) using the `readxl` package.
* Drops incomplete records (`NA`) across coordinates to preserve the mathematical continuity of the profile boundary.
* Extracts the chronological `Year` string from localized field collection timestamps using the `dplyr` mutation functions.

### 2. Numerical Integration for Area Calculations
* To calculate the net cross-sectional area under the irregular channel boundary curves, the script implements the **Trapezoidal Rule** via the `pracma::trapz()` integration framework:
  $$\text{Area} = \int_{a}^{b} f(x) \,dx \approx \sum_{i=1}^{n-1} \frac{f(x_i) + f(x_{i+1})}{2} (x_{i+1} - x_i)$$
* Maps the geometric integrals across independent cross-sectional distance parameters vs. vertical bed height offsets (Reduced Level, `RL(m)`).

### 3. Bed Elevation Profiles
* Groups data tables cleanly by historical collection years to compute critical morphodynamic indicators:
  * **Mean RL ($\text{m}$):** Identifies the overall volumetric shift or vertical tilting trend of the channel frame.
  * **Minimum RL ($\text{m}$):** pinpoints the maximum thalweg depth line (the absolute lowest point in the riverbed channel), providing clear empirical proof of active bed-scouring or sediment accumulation.

### 4. Interactive Data Rendering
* Generates a structural multi-line scatter chart via `ggplot2` mapping the cross-sectional geometries. Individual temporal baselines are color-coded dynamically by `Year` to provide instant, publication-ready visual proof of how the river boundaries shifted sideways or down over time.

---

## 💻 Repository Structure & Usage

### File Directory
* `river_cross_section_modeling.R` — Main processing script containing the structural computational code.

### Prerequisites & Dependencies
To run this analysis locally, ensure you have R or RStudio installed along with the following CRAN libraries:
```r
install.packages(c("readxl", "dplyr", "ggplot2", "pracma"))
