# Marketing Campaign A/B Test Analysis

A statistical analysis of a real marketing experiment, testing whether advertising measurably increased purchase conversion compared with a public service announcement (PSA) control, and by how much.

## Overview

Companies run A/B tests to separate the effect of a campaign from background noise. In this experiment, most users were shown an advertisement (the treatment group) while a smaller group saw a neutral PSA in the same placement (the control group). This project answers two questions:

1. Did the ads increase conversion?
2. Is the observed difference statistically significant, and how large is it likely to be in reality?

![Conversion rate by test group](./conversion_rate_by_group.png)

## Key Findings

| Group | Users | Conversions | Conversion rate |
|---|---|---|---|
| Ad (treatment) | 564,577 | 14,423 | 2.55% |
| PSA (control) | 23,524 | 420 | 1.79% |

- **Absolute difference:** +0.77 percentage points
- **Relative lift:** 43.1%
- **Significance test:** chi-square test of independence, χ²(1) = 54.01, p < 0.001
- **95% confidence interval for the difference:** approximately 0.60 to 0.94 percentage points

The difference is statistically significant, and even the conservative end of the confidence interval indicates a real uplift from the ads.

## Dataset

- **Source:** [Marketing A/B Testing on Kaggle](https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing)
- **Size:** 588,101 users
- **Columns:** `user id`, `test group` (ad or psa), `converted` (True/False), `total ads`, `most ads day`, `most ads hour`

The raw data file is not included in this repository. To reproduce the analysis, download `marketing_AB.csv` from the link above (a free Kaggle account is required) and place it in the same folder as the notebook.

## Methodology

1. **Data inspection:** loaded the data with pandas and checked structure, column names and group sizes.
2. **Conversion rates:** calculated conversion rate, user count and conversions for each test group.
3. **Hypothesis test:** built a 2×2 contingency table (test group × converted) and ran a chi-square test of independence with `scipy.stats.chi2_contingency` (SciPy's default continuity correction for 2×2 tables). The null hypothesis was that conversion is independent of test group, tested at α = 0.05.
4. **Effect size:** calculated the absolute difference, relative lift, and a 95% confidence interval for the difference in proportions (normal approximation).
5. **Visualisation:** plotted conversion rate by group.

## Recommendation

The ads produce a real, measurable increase in conversions, so the campaign is worth continuing, subject to a cost check. This dataset contains no ad cost or revenue-per-sale data, so whether a lift of roughly 0.6 to 0.9 percentage points is *profitable* depends on those figures, which should be compared before scaling spend.

## Limitations

- **Unbalanced groups:** about 96% of users were in the ad group and about 4% in the PSA group, so the PSA conversion rate is estimated less precisely than the ad rate. The chi-square test accommodates unequal group sizes, but the uncertainty is not symmetrical.
- **Random assignment is assumed:** as stated in the dataset's documentation. If assignment was not random, the results could reflect differences between the groups rather than the effect of the ads.
- **Significance is not profitability:** a statistically significant uplift does not by itself show the campaign pays for itself.

## Reproducing the Analysis

1. Clone or download this repository.
2. Download `marketing_AB.csv` from Kaggle and place it in the project folder.
3. Install dependencies: `pip install -r requirements.txt`
4. Launch Jupyter with `jupyter notebook` and open `ab_test_analysis.ipynb`.
5. Run all cells from top to bottom.

## Tools Used

- **Python**
- **pandas** for data handling
- **SciPy** for the statistical test
- **Matplotlib** for visualisation
- **Jupyter Notebook**

## Repository Contents

```
├── ab_test_analysis.ipynb          # Full analysis with outputs and written recommendation
├── conversion_rate_by_group.png    # Chart of conversion rate by test group
├── requirements.txt                # Python dependencies
└── README.md
```

## Author

**Ali Abdo**
[aliabdo.dev](https://aliabdo.dev) · [LinkedIn](https://www.linkedin.com/in/ali-abdo-164744298/) · [GitHub](https://github.com/Ali-Abdo03)

