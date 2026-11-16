# Host Blood Gene Expression Signatures to Distinguish Active from Latent Tuberculosis

Computing Bioinformatics group project.

## Research Question

Can whole-blood gene expression tell active TB apart from latent TB infection in African adults, and does this still work in people living with HIV?

## Hypothesis

Active TB causes an interferon-driven change in blood gene expression that separates it from latent TB. HIV co-infection blurs that difference, so classifiers will perform worse in HIV+ patients.

## Objectives

1. Find genes that are expressed differently in active TB and latent TB, using FDR correction.
2. Run GO and pathway enrichment on those genes to check whether interferon and immune pathways come out on top.
3. Train a classifier for active vs. latent TB and compare it with two baselines: a majority-class model and the published 3-gene Sweeney score (GBP5, DUSP3, KLF2).
4. Compare how well the model performs in HIV− and HIV+ patients.

## Data

| Dataset | Description | Role |
|---|---|---|
| GEO GSE37250 (Kaforou et al., 2013) | Whole-blood microarrays from South Africa and Malawi: active TB, latent TB, other diseases, with HIV status | Main dataset |
| GEO GSE19491 (Berry et al., 2010) | Whole-blood TB signature study (UK and South Africa) | External validation |
| MSigDB Hallmark / GO, STRING | Gene sets and protein interaction networks | Biological interpretation |

All data is public and is downloaded directly in the notebook with GEOparse.

## Repository Structure

- `notebooks/TB_host_response.ipynb`: main analysis notebook (runs top to bottom in Google Colab)
- `data/`: downloaded data files (not committed if large)
- `README.md`: this file

## Analysis Stages

1. Question and objectives
2. Data acquisition
3. Preprocessing and quality control
4. Exploratory data analysis
5. Core analysis (differential expression with FDR)
6. Biological interpretation (GO/pathway enrichment, STRING)
7. Machine learning (classifier vs. baselines)
8. Conclusions and limitations

## How to Run

1. Open `notebooks/TB_host_response.ipynb` in Google Colab.
2. Run all cells from top to bottom (Runtime > Run all). The first cell installs the required packages.

## Group Members

| Student ID | Name |
|---|---|
| 148654 | Jeremy Chege |
| 142544 | Lorna Nyabuto |
| 147585 | Nicole Kirimi |
| 132989 | Wesley Mutisya |
| 168323 | Micheal Wambari |
| 163362 | Bill Ritchie |

## Key Results

- 1,577 of 10,065 genes differ between active and latent TB (FDR < 0.05, |log2FC| > 0.5): 800 higher and 777 lower in active TB.
- Genes higher in active TB are most enriched for Interferon Gamma and Interferon Alpha response pathways.
- A 100-gene logistic regression reached AUC 0.954 (cross-validated), compared with 0.500 for the majority-class baseline and 0.926 for the 3-gene Sweeney score.
- Performance is lower in HIV-positive patients (AUC 0.922) than in HIV-negative patients (0.984); the difference is 0.062 (95% CI 0.024 to 0.105).
- No external validation was done; all results are from cross-validation within GSE37250.

## References

- Kaforou M. et al. (2013). Detection of tuberculosis in HIV-infected and uninfected African adults using whole blood RNA expression signatures. PLoS Medicine.
- Berry M.P.R. et al. (2010). An interferon-inducible neutrophil-driven blood transcriptional signature in human tuberculosis. Nature.
- Sweeney T.E. et al. (2016). Genome-wide expression for diagnosis of pulmonary tuberculosis: a multicohort analysis. Lancet Respiratory Medicine.
