# econ3916-lab07-bootstrapping

# Estimation & Bootstrapping: Quantifying Uncertainty Without a Formula

## Objective
I compared formula-based and bootstrap confidence intervals to see when each one can be trusted to quantify uncertainty.

## Methodology
- Loaded the UCI Adult Census Income data (32,561 respondents).
- Separated the standard deviation of the data from the standard error of an estimate, and checked the s/√n relationship across four sample sizes.
- Built parametric confidence intervals from the CLT and compared how quickly it converges for age versus capital gains.
- Ran the bootstrap by hand, then again with `scipy.stats.bootstrap`.
- Computed the bootstrap SE of the median of age, which turned out to be a degenerate case (see Key Findings).
- Compared percentile and BCa intervals on a heavily skewed variable.
- Bootstrapped a two-sample difference in mean weekly hours.
- Asked an AI to write a bootstrap-interval function, revised my prompt once, and checked the function's output against my own intervals.
- Ran a coverage simulation on lognormal data at n=50, covering both the mean and the median.

## Key Findings
- The CLT converges quickly for age and slowly for capital gains, so a formula-based interval is reliable for one and shaky for the other.
- The bootstrap SE of the median of the 32,561 whole-number ages is exactly 0.0000. With that many ties, every resample returns the same median. The bootstrap is reporting a real property of the data, not failing.
- On a heavily skewed variable, I compared percentile and BCa intervals side by side.
- For the mean in the coverage simulation, the nominal 95% parametric interval covered 92.5% and the percentile bootstrap covered 91.5%. The gap falls inside the Monte Carlo standard error of about 1.3 points, so the two methods are indistinguishable here, and both under-cover slightly.
- For the median, the mean-centred parametric interval covered only 66.8%, while the bootstrap held near its nominal level. The bootstrap is the better choice when no simple standard-error formula fits the statistic.
