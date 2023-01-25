# Expected Loss Model

The model is used to estimate the expected losses to their stable value wrap model, and which is also run repeatedly to perform stress tests.

The log-normal equity returns generation was found to be correct, and is approved for use provided that the simulated equity returns are (at least approximately) log-normal and uncorrelated with the fixed income portion of the portfolio (|_| _ 0.2). Similarly, the equity returns sheet is approved for use (with externally generated returns) provided that the input returns are either properly correlated with the fixed income returns, or sufficiently uncorrelated as above. 

The spread adjustment to the crediting rate is made when MV/BV > 0.9 (and is generalized to a schedule, with increasing spreads at larger MV/BV ratios). Recall that the crediting rate C is determined by:

 

and the crediting rate is used to determine the (stable) growth of the book value:

 

where we have included a possible spread adjustment SA.

The only significant issue is that the State Bank deal has a spread adjustment (SA) that declines from 0.75% to 0.5% in steps of 0.05% over the first 5 years of the deal, whereas the model assumes that SA is fixed throughout the life of the deal. Setting SA=0.75% will result in a conservative exposure calculation, but not necessarily conservative VaR/stress-testing results.

We have added the amortizing spread adjustment to the model and fond that with the current deal parameters (ignoring tax) results in a VaR of _ 3bp, which is underestimates by _ 0.5bp if this adjustment amortization is ignored (as the IPS model does). As the book value of this deal is a relatively small fraction of the entire portfolio (_ 0.3%), this difference is insignificant.

The model treats an equity component of the underlying as a log-normal process, with quarterly equity percent-returns generated for quarter n by:

 

Here μ and _ are the input quarterly mean return and standard deviation respectively. (If not generated, these quarterly returns are input into the sheet manually.)

The market value of the underlying is then modeled as a two-component portfolio, with fixed equity fraction _. Recall that the value (MV) of a purely fixed-income portfolio changes from month to month.

 

where R is the simulated yield (see https://finpricing.com/lib/FxForwardCurve.html) for the quarter, generated from a mean-reverting process:

 

with a the reversion rate (per quarter), eb the long run yield, and _ the instantaneous (quarterly) volatility.

The effective return on the fixed-income part of the underlying is therefore:

 

and therefore the market value growth of a mixed underlying portfolio grows as:

 

All other calculations (crediting rate, book value growth, etc.) remain the same.

Clearly this approach is strictly correct only for a wrapped portfolio that is re-balanced to have a fixed equity fraction every quarter, and the two components are uncorrelated.

One of the general weaknesses in the IPS model is that all processes are uncorrelated. In this case, we can consider the effects of a correlation between the equity and yield process by generating correlated returns by using:

 

where _ represents the correlation between the fixed-income and ‘equity’ returns.



