# WF-RS C2000 Processor-in-the-Loop Evidence

This repository contains processor-in-the-loop (PIL) evidence for the
Wind-Feasible Recovery Supervisor (WF-RS) used in an autonomous sailing
sea-drone no-go-zone recovery study.

The repository is intentionally evidence-focused. It documents embedded
controller-step execution on a TI LAUNCHXL-F28379D C2000 target and the
resulting command-equivalence checks against a host-reference run. It is not a
full simulation-code release and it is not an on-water field experiment.

## What This Repository Shows

- The C2000 target was flashed with a PIL firmware wrapper for the WF-RS
  controller step.
- The target sent the startup message `READY,C2000_PIL`.
- The host sent one `REQ` record at each controller update and received one
  `CMD` response from the target.
- Six representative scenarios were run over the serial PIL link.
- Host-reference and C2000 serial logs matched at 714 controller update instants
  with zero protocol failures.
- Rudder and sail command differences were at numerical roundoff level.

## Main Result

| Scenario | Matched control updates | Max rudder error [deg] | Max sail error [deg] | Protocol failures |
|---|---:|---:|---:|---:|
| S0: Crosswind sanity | 64 | 2.664535e-15 | 1.421085e-14 | 0 |
| S1: Upwind tacking | 131 | 3.552714e-15 | 1.421085e-14 | 0 |
| S2: Obstacle, favorable wind | 83 | 3.419487e-14 | 2.486900e-14 | 0 |
| S3: Low-energy transit | 71 | 1.776357e-15 | 4.263256e-14 | 0 |
| S4: Obstacle escape near no-go zone | 255 | 1.776357e-15 | 1.421085e-14 | 0 |
| S5: Coupled wind, obstacle, and energy | 110 | 6.861178e-14 | 1.421085e-14 | 0 |

`Matched control updates` means host-to-target `REQ` and target-to-host `CMD`
records with the same `control_index`. It is the number of controller execution
instants compared, not the number of plant integration rows.

## Included Evidence

- `docs/IMPLEMENTATION_REPORT.md`: reviewer-facing implementation and scope
  report.
- `docs/RESULTS_SUMMARY.md`: six-scenario PIL result summary.
- `docs/REPRODUCE.md`: how to inspect and verify the included evidence files.
- `docs/DATA_DICTIONARY.md`: explanation of the main CSV columns.
- `docs/GITHUB_PUBLICATION.md`: upload notes for this evidence-only repository.
- `docs/source_notes/`: original flashing and C2000 PIL notes.
- `metadata/`: source/package metadata retained from the handoff.
- `results/logs/`: host-reference and C2000 serial CSV logs.
- `results/command_error/`: merged command-error CSVs and summary tables.
- `results/figures/`: generated command-error figures and hardware setup image.
- `MANIFEST_SHA256.txt`: SHA-256 hashes for the public evidence files.

## Scope

The PIL validation checks embedded execution, serial communication, and command
equivalence for the controller step. The sailing plant, wind field, obstacle
geometry, and mission progression remain simulated on the host computer.

This evidence does not validate field sailing performance, perception, state
estimation, hydrodynamic identification, sensors, actuators, or full
hardware-in-the-loop behavior.

## Serial Configuration

The recorded run used `COM6` at `115200` baud.
