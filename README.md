# County Median Income and Diabetes-Related Hospitalizations

This project examines the relationship between county-level median adjusted gross income and the Diabetes Composite observed hospitalization rate across California counties in 2022.

The analysis combines county-level data from the California Franchise Tax Board and the California Department of Health Care Access and Information (HCAI). A simple linear regression model is used to evaluate whether counties with higher median adjusted gross income tend to have lower diabetes-related preventable hospitalization rates.

## Research Question

Is median adjusted gross income associated with the Diabetes Composite observed hospitalization rate across California counties in 2022?

The project hypothesizes that counties with higher median adjusted gross income will have lower Diabetes Composite observed hospitalization rates.

## Data Sources

The analysis uses the following 2022 county-level data sources:

- **Diabetes-related hospitalization data:** California Department of Health Care Access and Information (HCAI), [Rates of Preventable Hospitalizations for Selected Medical Conditions by County](https://data.ca.gov/dataset/rates-of-preventable-hospitalizations-for-selected-medical-conditions-by-county-lghc-indicator)
- **Income data:** California Franchise Tax Board, [B-6 Comparison by County](https://data.ca.gov/dataset/b-6-comparison-by-county2)

The diabetes dataset provides the `Diabetes Composite` observed hospitalization rate per 100,000 population. The income dataset provides median adjusted gross income by county and taxable year.

## Repository Structure

```text
.
├── README.md
├── paper-1.qmd
├── paper-1.pdf
├── diabetes-scatter.png
├── diabetes-residual.png
└── diabetes-qqplot.png
```

Raw data files are not included in this repository.

## Data Preparation

The data preparation process consists of the following steps:

1. Filter the hospitalization data to the year 2022.
2. Retain only observations corresponding to `Diabetes Composite`.
3. Keep the county name and `ObsRate_ICD10` variables.
4. Filter the income data to taxable year 2022.
5. Keep the county name and `Median Income` variables.
6. Merge the two datasets using an inner join based on `County`.
7. Divide median income by 1,000 so that the predictor is measured in thousands of dollars.

No observations were manually deleted or imputed. The data were not otherwise modified beyond filtering, selecting variables, merging the datasets, and changing the income unit for interpretability.

## Statistical Analysis

The project fits the following simple linear regression model:

```text
Diabetes Composite observed rate
= β₀ + β₁(Median adjusted gross income in $1,000s) + ε
```

The slope parameter is tested using:

```text
H₀: β₁ = 0
Hₐ: β₁ ≠ 0
```

The analysis uses a two-sided t-test with a significance level of 0.05. Scatterplots, a residual plot, and a normal Q-Q plot are used to assess the regression assumptions.

## Main Findings

The fitted model shows a statistically significant negative association between median adjusted gross income and the Diabetes Composite observed hospitalization rate. In general, counties with higher median adjusted gross income tend to have lower diabetes-related hospitalization rates.

Because this is an observational, county-level analysis, the results demonstrate an association rather than a causal relationship. The findings should not be interpreted as evidence that increasing an individual's income would directly reduce their risk of diabetes-related hospitalization. Other factors, such as age distribution, healthcare access, insurance coverage, population size, and demographic characteristics, may also contribute to the observed relationship.

## Reproducing the Analysis

### Requirements

Install the following software and R packages:

- [R](https://cran.r-project.org/)
- [Quarto](https://quarto.org/)
- `readr`
- `dplyr`
- `ggplot2`
- `knitr`

The packages can be installed in R with:

```r
install.packages(c("readr", "dplyr", "ggplot2", "knitr"))
```

### Steps

1. Clone or download this repository.

2. Place the following CSV files in the same directory as `report.qmd`:

   - `ca-hcai-preventablehospitalizations-county_2005-2024.csv`
   - `2023-b-6-comparison-by-county.csv`

3. Open a terminal in the repository directory and render the Quarto report:

```bash
quarto render report.qmd
```

4. Quarto will generate the PDF report and execute the R code contained in the document.

## Software

The statistical analysis was conducted in R. The report was written and rendered using Quarto.

## Author

Elaine Li

## Acknowledgments
This project repository is based on the template provided by Rohan Alexander.


