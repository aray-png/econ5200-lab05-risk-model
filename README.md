# Abigail Ray || Diagnosing a Flawed Risk Model — VaR, Expected Shortfall & Monte Carlo

## Objective
I diagnosed a flawed Value at Risk model, compared it against better alternatives, and built a reusable risk calculation module.

## Methodology
- Found that a junior analyst's VaR model, which assumed returns followed a normal distribution, understated the true 99% Value at Risk by 12.7% ($40,393 on a $10M portfolio)
- Computed VaR and Expected Shortfall three different ways on the same portfolio returns: assuming a normal distribution, fitting a Student-t distribution (fitted degrees of freedom = 4.58), and using the historical (empirical) distribution directly
- Priced a European call option with Monte Carlo simulation and reduced the standard error by 1.26x using antithetic variates, a technique that pairs each random draw with its mirror image to cancel out some of the random noise
- Built a reusable Python module, risk_metrics.py, with functions for VaR, Expected Shortfall, and Monte Carlo-based risk estimation, and ran its built-in self-tests to confirm it worked correctly
- Had an AI write a backtesting function to check how often each VaR estimate was actually breached, revised my initial prompt once to fix an ambiguity in sign convention, and checked the AI's output against a count I calculated by hand

## Key Findings
- The normal-distribution VaR model understated the true 99% risk by 12.7%, a $40,393 gap on a $10M portfolio, because it failed to account for the fat tails present in the actual return data
- The normal 99% VaR was breached on 1.71% of days, well above the 1% a properly calibrated 99% VaR should allow, confirming the model gave a false sense of safety
- Antithetic variates reduced the Monte Carlo standard error by 1.26x without requiring any additional simulations
- The Student-t distribution (fitted with 4.58 degrees of freedom) better captured the fat-tailed nature of the data than the normal distribution did, since a lower degrees-of-freedom value indicates fatter tails
