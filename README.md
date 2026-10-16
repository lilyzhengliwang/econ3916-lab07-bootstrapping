# econ3916-lab07-bootstrapping

# Estimation & Bootstrapping: Quantifying Uncertainty Without a Formula

## Objective
I used the UCI Adult Census Income data to compare formula-based confidence intervals with bootstrap intervals, and to find where each one works and where it breaks.

## Methodology
- Loaded the UCI Adult Census Income data (32,561 respondents).
- Separated the standard deviation of the data from the standard error of an estimate, and checked the s/sqrt(n) relationship across four sample sizes.
- Built parametric confidence intervals from the CLT and compared how quickly they converge for age and for capital gains.
- Ran the bootstrap by hand with a resampling loop, then again with `scipy.stats.bootstrap`.
- Bootstrapped the median of whole-number ages and examined the result.
- Compared percentile and BCa intervals on a heavily skewed variable.
- Bootstrapped a two-sample difference in mean weekly hours.
- Asked an AI to write a bootstrap-interval function, revised my prompt once, and checked the function against my own intervals.
- Ran a coverage simulation on lognormal data at n=50, for both the mean and the median.

## Key Findings
- The CLT interval converges quickly for age and slowly for capital gains, because capital gains are heavily skewed.
- The bootstrap SE of the median of 32,561 whole-number ages is exactly 0.0000. Every resample returns the same median, because with that many ties the median is pinned. The bootstrap is reporting a real property of the data, not failing.
- For the mean at n=50, the nominal 95% parametric interval covered [YOUR VALUE]% and the percentile bootstrap covered [YOUR VALUE]%. That gap is inside the Monte Carlo standard error of about 1.3 points, so the two methods are indistinguishable here and both under-cover slightly. The bootstrap does not fix a statistic that already has a formula.
- For the median, the mean-centred parametric interval covered only about [YOUR VALUE]%, while the bootstrap held near its nominal level. The bootstrap earns its place on statistics with no formula.
- The AI's first function used NumPy's global random state and had no `seed` argument. It ran without error but could not be reproduced. After I asked for a local generator and a `seed` argument, the seeded call matched my scipy interval exactly.
