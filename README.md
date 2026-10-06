# econ3916-lab04-anomaly-detection

# Robust Statistics -- Automated Anomaly Detection

## Objective
I tested how much a few extreme values distort common summary statistics on California Housing data, and compared two ways of flagging outliers.

## Methodology
- Loaded the California Housing dataset (20,640 block groups) from scikit-learn.
- Computed the mean, median, trimmed mean, standard deviation, IQR, and MAD for median house value, and compared how each one responds to the long right tail.
- Built Tukey Fences by hand (Q1 − 1.5×IQR and Q3 + 1.5×IQR) to flag price outliers, and plotted the fences on a histogram and boxplot.
- Ran scikit-learn's Isolation Forest on the housing features to flag rows with unusual combinations of values, not just unusual prices.
- Compared the rows flagged by each method to see where they agreed and disagreed.
- Ran a contamination experiment: I replaced 5% of the house values with extreme numbers and measured how much each statistic moved.

## Key Findings
- The mean and standard deviation get pulled up by expensive block groups, while the median, IQR, and MAD stay close to where most of the data sits.
- Tukey Fences and Isolation Forest mostly flagged different observations. Tukey only looks at price, so it flags the expensive areas. Isolation Forest flags rows with odd combinations, like very crowded or densely populated blocks.
- Many of the Tukey outliers sit exactly at the dataset's $500,001 cap. These are censored values, not true extremes, so deleting them would be a mistake.
- After 5% contamination, the mean shifted by 67.1% and the median shifted by only 3.6%.
- A flagged outlier isn't automatically an error. I'd check whether it's a data mistake, a measurement artifact, or a real extreme value before deciding what to do with it.
