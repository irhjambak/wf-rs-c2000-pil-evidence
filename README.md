# WF-RS C2000 Processor-in-the-Loop Evidence

This repository contains processor-in-the-loop (PIL) evidence for the
Wind-Feasible Recovery Supervisor (WF-RS) used in an autonomous sailing
sea-drone no-go-zone recovery study.

The purpose of this repository is to document embedded execution evidence. The
sailing plant and environment remain simulated on the host computer, while the
WF-RS controller step executes on a TI LAUNCHXL-F28379D C2000 target and returns
rudder and sail commands over a serial request-response interface.

This is not an on-water experiment and not a full simulation-code release.

## What Is Included

- PIL result summaries.
- Python-reference and C2000 serial command logs.
- Command-error CSV files.
- Generated PIL figures.
- Documentation of the serial protocol and validation setup.
- File hashes for integrity checking.

## Main Result

Across six representative scenarios, the C2000 target responses matched the
host-reference controller outputs at 714 controller update instants with zero
protocol failures. Rudder and sail command differences are at numerical
roundoff level.

## Folder Structure

- `docs/`: implementation report, result summary, reproduction notes, and data dictionary.
- `metadata/`: package metadata.
- `results/logs/`: paired host-reference and C2000 serial logs.
- `results/command_error/`: command-error summaries.
- `results/figures/`: generated command-error and hardware figures.
- `MANIFEST_SHA256.txt`: file hashes for integrity checking.

## Scope

The PIL evidence verifies embedded controller-step execution and serial
communication behavior. It does not validate the full sailing platform in field
conditions.
