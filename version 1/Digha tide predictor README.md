# Digha Tide Calculator — improved model

This version is deliberately built around the only Digha data available in the conversation: the Tidechart screenshot containing high/low extrema from 19–28 August 2026.

## Data used

38 reported extrema:
- 19–28 August 2026
- time + height
- high/low classification

These are **not continuous observations**. They are reported tide-table extrema, so the model must be treated as an empirical extrapolation.

## Model

eta(t) = Z0 + sum[a_i cos(w_i t) + b_i sin(w_i t)]

The frequencies are fixed constituent frequencies. The local coefficients are estimated from the supplied extrema with least squares.

The program tests five candidate models and chooses the one with the lowest leave-one-day-out cross-validation RMSE.

The selected model will normally be:

M2 + S2 + N2 + K1 + O1 + M4

## Numerical improvements

- Householder QR least squares instead of explicitly forming (X'X)^-1.
- No artificial +50-minute/day rule.
- No manually entered Digha amplitudes/phases.
- High/low times are found from dh/dt = 0 and refined by bisection.
- Leave-one-day-out cross-validation chooses the model complexity.
- Harmonic amplitudes and phases are displayed from the actual fitted coefficients.
- Sunrise/sunset and Moon phase are kept as contextual astronomy; they are not falsely used as direct inputs to the fitted tide curve.
- No extrapolated linear sea-level trend is used, because a 10-day extrema record cannot justify a 54-day secular trend.

## Scientific limitation

This is not equivalent to a professional harmonic prediction based on continuous tide-gauge observations and full astronomical arguments/nodal corrections. The model is best described as a **frequency-constrained empirical harmonic extrapolation**.

For the October 12 result, use the model as a close mathematical estimate and compare it with a published tide table when one is available.
