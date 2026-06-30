# Embedded PIL Results Summary

## Summary Table

| Scenario | Reference rows | C2000 serial rows | Matched control updates | Max rudder error [deg] | Max sail error [deg] | RMS rudder error [deg] | RMS sail error [deg] | Protocol failures |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| S0: Crosswind sanity | 316 | 316 | 64 | 2.664535e-15 | 1.421085e-14 | 3.966717e-16 | 3.552714e-15 | 0 |
| S1: Upwind tacking | 653 | 653 | 131 | 3.552714e-15 | 1.421085e-14 | 4.956263e-16 | 4.123794e-15 | 0 |
| S2: Obstacle, favorable wind | 415 | 415 | 83 | 3.419487e-14 | 2.486900e-14 | 4.015430e-15 | 6.028651e-15 | 0 |
| S3: Low-energy transit | 354 | 354 | 71 | 1.776357e-15 | 4.263256e-14 | 2.981371e-16 | 8.681884e-15 | 0 |
| S4: Obstacle escape near no-go zone | 1274 | 1274 | 255 | 1.776357e-15 | 1.421085e-14 | 1.722605e-16 | 2.246933e-15 | 0 |
| S5: Coupled wind, obstacle, and energy | 550 | 550 | 110 | 6.861178e-14 | 1.421085e-14 | 7.715030e-15 | 3.604815e-15 | 0 |

Total plant rows: 3562.

Total matched control updates: 714.

Total protocol failures: 0.

## Meaning of Matched Control Updates

The plant is integrated at 0.2 s, but the controller is called at 1.0 s. Therefore, not every CSV row is a controller execution. A matched control update is one Python-reference controller update and one C2000 serial response with the same `control_index`.

## Figures

- `results/figures/pil_serial_six_scenario_command_error.png` shows the six-scenario absolute command-error suite.
- Individual figures in `results/figures/*__pil_serial_command_error.png` include signed error, absolute error, and command overlays for each scenario.

The manuscript uses the compact six-scenario absolute-error plot because it shows the error magnitude on a log scale and fits all scenarios in one figure. The individual plots are retained for auditability.

