# OLS Diagnostics: When the Standard Error Is Lying

## Objective
I tested when the classical OLS standard error can be trusted and built a regression that passes every diagnostic in this lab and is still wrong.

## Methodology
- Simulated 2,000 points with errors whose spread grows with x and fitted the same regression with classical and with robust (HC3) standard errors
- Ran 400 simulated samples and counted how often each 95% interval contained the true slope
- Read four residual plots beside Breusch-Pagan and Jarque-Bera tests
- Measured leverage and standardised residuals and Cook's distance and deleted the most influential row out of 600
- Fitted a California Housing regression of median house value on four district features with classical and HC3 standard errors
- Wrote a function hc3_se() that gives back the HC3 standard error of one coefficient and ran it with and without the 965 districts at the 5.0 ceiling
- Simulated data where a confounder drives both x and y and regressed y on x alone

## Key Findings
- Both fits gave the same slope of 2.0147 with a classical standard error of 0.0264 and a robust one of 0.0290, so heteroskedasticity changed the standard error and not the estimate.
- The classical 95% interval covered the true slope in 91.8% of the 400 samples (Monte Carlo SE 1.4%) and the robust one in 93.5% (Monte Carlo SE 1.2%), so only the classical shortfall was clearly more than chance.
- Deleting one row out of 600 moved the slope 0.58 of its own standard error and the standard error fell 33%, so the row hurt the standard error far more than the slope.
- In California Housing the HC3 standard error on AveRooms was 5.02 times the classical one.
- My hc3_se() function gave an HC3 standard error on AveRooms of 0.0121 with all districts and 0.0082 without the 965 at the 5.0 ceiling. I kept all districts because a smaller standard error is not a reason to drop rows.
- My confounded regression passed Breusch-Pagan (p = 0.8058) and Jarque-Bera (p = 0.6628) and its largest Cook's distance was 0.0202, but the coefficient on x was 2.6975 against a truth of 1.5. Diagnostics check the standard error and not whether a confounder is missing.
