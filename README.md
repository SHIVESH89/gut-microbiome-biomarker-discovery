# 🧬 Project 2: Gut Microbiome Analysis & Disease Biomarker Discovery

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Status](https://img.shields.io/badge/Status-Complete%20Analysis-success.svg)]()
[![Data-Source](https://img.shields.io/badge/Dataset-curatedMetagenomicData%20%7C%20Nature%20Medicine-informational.svg)](https://github.com/borenstein-lab/microbiome-metabolome-curated-data)

---

## 📌 Executive Summary

Colorectal cancer (CRC) is one of the leading causes of cancer mortality globally. Emerging biomedical research (*Nature Medicine, Cell, Gastroenterology*) establishes that intestinal microbiome dysbiosis plays a critical role in colorectal carcinogenesis along the **adenoma-carcinoma sequence**. Perturbations in mucosal homeostasis, depletion of short-chain fatty acid (SCFA) synthesizers, and opportunistic colonization by pro-inflammatory oncomicrobes drive epithelial barrier breakdown, genotoxic stress, and tumor progression.

This repository contains an end-to-end computational biology and statistical genomics pipeline analyzing shotgun metagenomic sequencing and clinical metadata from **347 human participants** (*Yachida et al., Nature Medicine 2019* / *curatedMetagenomicData*). We perform rigorous **Exploratory Data Analysis (EDA)**, **Inferential Hypothesis Testing ($t$-tests, ANOVA, Tukey's HSD)**, and **Principal Component Analysis (PCA)** to uncover microbial biomarkers and ecological diversity patterns driving colorectal disease stages.

---

## 🎯 The Need for the Dataset

### Why curatedMetagenomicData & Nature Medicine (Yachida et al.)?
* **High-Resolution Metagenomics:** Shotgun metagenomics provides species and genus-level taxonomic resolution far exceeding 16S rRNA amplicon sequencing.
* **Granular Colorectal Progression Spectrum:** The cohort uniquely covers the full continuum of colorectal carcinogenesis across **6 clinical stages**:
  * Healthy Controls ($N = 127$)
  * Stage 0 Carcinoma in situ ($N = 27$)
  * Stage I/II Carcinoma ($N = 69$)
  * Stage III/IV Carcinoma ($N = 54$)
  * Multiple Polypoid Adenomas (MP) ($N = 40$)
  * High-grade Dysplasia (HS) ($N = 30$)
* **Clinical Metadata Integration:** Merges patient stool metagenomes with Age, Gender, BMI, Smoking Brinkman Index, Alcohol consumption, and Tumor anatomical localization.

---

## 🔬 What Has Been Done

### 1. Data Cleaning & Integration
* Merged patient clinical records with high-dimensional genus relative abundance matrices across all 347 participants with 100% completeness (0% missingness).
* Extracted GTDB bacterial phyla (*Bacteroidota*, *Firmicutes*, *Proteobacteria*, *Actinobacteriota*, etc.) and calculated ecological metrics (Shannon entropy, Richness, and Bacteroidota-to-Firmicutes $B/F$ ratio).

### 2. Exploratory Data Analysis (EDA) & Visualizations (`01_EDA_Visualization.ipynb`)
* **Univariate Distributions:** Demographics (Age, Gender, BMI), WHO weight classification, clinical stage breakdown, lifestyle exposure (smoking Brinkman index, alcohol score), and tumor anatomical site breakdown.
* **Taxonomic Composition:** Phylum-level stacked relative abundance bars, $B/F$ ratio distributions, and Top 15 dominant gut genera.
* **Bivariate Associations:** Stratified cross-stage analyses of BMI, Age, and key biomarker genera (*Fusobacterium*, *Faecalibacterium*).
* **Correlation & Multivariate Analysis:** Spearman correlation matrix heatmap, bivariate linear regressions, and multi-feature pairplots.

### 3. Inferential Hypothesis Testing & PCA (`02_Statistical_Analysis.ipynb`)
* **Descriptive Suite:** Comprehensive calculation of central tendencies (Mean, Median, Mode), dispersion (Std, Variance, IQR, Range), skewness ($g_1$), kurtosis ($g_2$), and frequency cross-tabulations.
* **Two-Sample Independent $t$-Tests:** Evaluated physiological variations (BMI across biological sex; Healthy vs CRC cohorts) accompanied by effect size estimation (**Cohen's $d$**).
* **One-Way ANOVA & Effect Sizes:** Evaluated variance across the 6 clinical stages against metabolic and microbial indicators, measuring explained variance via **Eta-squared ($\eta^2$)**.
* **Post-Hoc Pairwise Comparisons:** Applied **Tukey's Honestly Significant Difference (HSD)** test with family-wise error rate control.
* **Unsupervised Learning (PCA):** Standardized Z-score normalization, Scree plot with Kaiser criterion, 2D PCA Biplot with feature loading vectors, component loadings heatmap, and 3D PCA dimensional projection.

---

## 📂 Repository Structure

```text
Project2_Microbiome_Analysis/
├── dataset/                                   # Curated clinical & metagenomic data (compressed <25 MB for GitHub)
│   ├── curated_sample_metadata.csv            # 347 patients with clinical phenotype metadata (81.8 KB)
│   ├── curated_genus_relative_abundance.csv.gz # Genus abundance profiles (4.77 MB, decompresses to 33.5 MB)
│   └── curated_species_relative_abundance.csv.gz # Species abundance profiles (14.85 MB, decompresses to 134.2 MB)
│
├── plots/                                     # Generated EDA figures (15 high-res PNGs)
│   ├── 01_missing_values.png
│   ├── 02_age_sex_distribution.png
│   ├── 03_bmi_distribution.png
│   ├── 04_stage_distribution.png
│   ├── 05_phylum_composition.png
│   ├── 06_bf_ratio_analysis.png
│   ├── 07_tumor_localization.png
│   ├── 08_lifestyle_factors.png
│   ├── 09_dominant_genera.png
│   ├── 10_bmi_by_stage.png
│   ├── 11_age_by_stage.png
│   ├── 12_biomarkers_by_stage.png
│   ├── 13_correlation_heatmap.png
│   ├── 14_scatter_relationships.png
│   └── 15_pair_plot.png
│
├── visualizations/                            # High-resolution PNG figures (categorized by notebook)
│   ├── 01_EDA_Visualizations/                 # 15 Clean EDA Plots (matching plots/)
│   └── 02_Statistical_Analysis/               # 12 Statistical & PCA Plots (t-tests, ANOVA, Scree, Biplots, 3D PCA)
│
├── stats_output/                              # Exported statistical summary tables & CSV reports
│   ├── descriptive_summary.csv
│   ├── frequency_tables.csv
│   ├── ttest_results.csv
│   ├── ttest_battery_results.csv
│   ├── anova_results.csv
│   ├── anova_battery_results.csv
│   ├── pca_loadings.csv
│   └── pca_loadings_matrix.csv
│
├── 01_EDA_Visualization.ipynb                 # Exploratory Data Analysis & visual discovery notebook
├── 02_Statistical_Analysis.ipynb              # Descriptive, inferential stats ($t$-test/ANOVA) & PCA notebook
├── README.md                                  # Project documentation, insights & setup guide
└── requirements.txt                           # Python dependencies for reproduction
```

---

## 📊 Key Findings & Insights

1. **Adenoma-to-Carcinoma Microbial Succession:** Microbiome dysbiosis is initiated in benign adenoma stages (`MP` - Multiple Polypoid Adenomas, `HS` - High-grade Dysplasia) before invasive adenocarcinoma onset.
2. **Oncogenic Pathobiont Enrichment:** Statistically significant enrichment of pro-inflammatory, mucosal-adherent pathobionts (notably *Fusobacterium*, *Porphyromonas*, *Peptostreptococcus*) in advanced carcinoma stages.
3. **Depletion of Beneficial Commensals:** Concomitant reduction in butyrate-producing short-chain fatty acid (SCFA) synthesizers (*Faecalibacterium*, *Roseburia*, *Bifidobacterium*).
4. **Statistical Significance & Effect Sizes:** Two-sample $t$-tests and ANOVA confirm significant divergence in taxonomic ratios and metabolic profiles across disease cohorts ($p < 0.05$).
5. **Dimensionality Reduction (PCA):** The leading principal components capture the dominant biological axes driven by phylum balance (*Bacteroidota* vs *Firmicutes*) and ecological richness.

---

## 🚀 Getting Started

### Prerequisites
* Python 3.9+
* Jupyter Notebook / JupyterLab

### Installation

1. **Navigate to the Repository Directory:**
   ```bash
   cd Project2_Microbiome_Analysis
   ```

2. **Activate your Virtual Environment:**
   ```bash
   # Windows (PowerShell):
   venv\Scripts\Activate.ps1

   # macOS / Linux:
   source venv/bin/activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Launch the Notebooks:**
   ```bash
   jupyter notebook
   ```
   * Open `01_EDA_Visualization.ipynb` to explore the exploratory data analysis pipeline.
   * Open `02_Statistical_Analysis.ipynb` to view the descriptive statistics, inferential testing, and PCA suite.

---

## 📚 References & Acknowledgments

* **Primary Dataset:** Yachida, S., Mizutani, S., Shiroma, H., et al. *"Metagenomic and metabolomic analyses reveal distinct stage-specific phenotypes of the gut microbiota in colorectal cancer."* *Nature Medicine* 25, 968–978 (2019).
* **curatedMetagenomicData:** Pasolli, E., Schiffer, L., Manghi, P., et al. *"Accessible, curated metagenomic data through ExperimentHub."* *Nature Methods* 14, 1023–1024 (2017).
* **Colorectal Cancer Microbiome Literature:**
  * Kostic, A. D., et al. *"Fusobacterium nucleatum potentiates intestinal tumorigenesis and modulates the tumor-immune microenvironment."* *Cell Host & Microbe* (2013).
  * Wong, S. H., & Yu, J. *"Gut microbiota in colorectal cancer: mechanisms of action and clinical applications."* *Nature Reviews Gastroenterology & Hepatology* (2019).

---

## 👤 Author
**Shivesh** ([@SHIVESH89](https://github.com/SHIVESH89))  
*Computational biology and metagenomics analysis for colorectal cancer biomarker discovery.*
