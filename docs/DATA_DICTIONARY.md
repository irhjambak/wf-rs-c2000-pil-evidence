# Data Dictionary

## Main Log Files

The files in `results/logs/` use two suffixes:

- `__python_reference.csv`: host-side Python reference simulation.
- `__pil_serial.csv`: simulation run whose controller step was executed on the C2000 target through the serial PIL bridge.

Important columns:

| Column | Meaning |
|---|---|
| `t` | Simulation time in seconds. |
| `X`, `Y` | Vehicle position in the inertial plane. |
| `psi` | Vehicle heading in radians. |
| `u`, `v`, `r` | Reduced-order body velocity states. |
| `E` | Energy state used by the controller. |
| `rudder`, `sail` | Command values in radians. |
| `rudder_deg`, `sail_deg` | Command values in degrees. |
| `is_control_update` | True when the row corresponds to a controller execution instant. |
| `control_index` | Integer index used to match Python-reference and C2000 serial controller updates. |
| `solver_status` | Controller status code returned by the controller. |
| `candidate_type_selected` | Encoded selected candidate type. |
| `candidate_set_size` | Number of candidates evaluated by the controller. |
| `intervention` | Indicates whether the safety/recovery supervisor changed the nominal command. |

Note: the raw CSV logs retain the internal `method` labels used by the original
PIL runner. These labels are metadata from the logging pipeline; the public
evidence claim is the matched command equivalence between the host-reference rows
and the C2000 serial rows for each `control_index`.

## Command-Error Files

The files in `results/command_error/*command_error.csv` are produced by merging Python-reference and C2000 serial logs on `control_index`.

Important columns:

| Column | Meaning |
|---|---|
| `control_index` | Matched controller update. |
| `t` | Time associated with the Python-reference matched row. |
| `rudder_deg_ref`, `sail_deg_ref` | Python-reference commands. |
| `rudder_deg_pil`, `sail_deg_pil` | C2000 serial PIL commands. |
| `rudder_error_deg` | `rudder_deg_pil - rudder_deg_ref`. |
| `sail_error_deg` | `sail_deg_pil - sail_deg_ref`. |
| `solver_status_pil` | C2000 solver status at the matched update. |
| `candidate_type_selected_pil` | C2000 selected candidate type. |
| `candidate_set_size_pil` | C2000 candidate-set size. |
| `intervention_pil` | C2000 intervention flag. |

## Six-Scenario Summary

`results/pil_serial_six_scenario_summary.csv` is the compact summary used for the manuscript table. It reports reference rows, C2000 serial rows, matched control updates, maximum absolute command errors, RMS command errors, and protocol failures.
