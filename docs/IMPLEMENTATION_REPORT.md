# Embedded PIL Implementation Report

## Validation Scope

The embedded processor-in-the-loop (PIL) validation checks whether the WF-RS
controller step can run on a TI LAUNCHXL-F28379D C2000 target and return the
same rudder and sail commands as the host-reference implementation. The plant
dynamics, wind field, obstacle geometry, and mission progression remain in the
host simulator.

This validation supports claims about embedded execution, serial communication,
and command equivalence. It does not replace on-water field tests, hydrodynamic
identification, perception validation, actuator validation, or full
hardware-in-the-loop testing with sensors and actuators.

## Hardware and Communication

- Target board: TI LAUNCHXL-F28379D / TMS320F28379D C2000.
- Serial port used in the recorded run: `COM6`.
- Baud rate: `115200`.
- Serial format: ASCII line-oriented request-response messages over SCI/UART.
- Startup record from firmware: `READY,C2000_PIL`.
- Host request prefix: `REQ`.
- Target response prefix: `CMD`.

## Architecture Under Test

The PIL setup has three conceptual layers.

1. Host simulation and runner

   The host advances the sailing plant and mission environment. At each
   controller update, it sends the current controller-step inputs to the C2000
   target and logs the target response alongside a host-reference result.

2. Serial request-response bridge

   The bridge builds `REQ` records, parses `CMD` records, checks sequence
   numbers, and writes paired CSV logs. A matched control update is accepted
   only when the target response has the expected `control_index`.

3. Embedded controller step

   The flashed target executes the controller-step logic and returns rudder and
   sail commands plus diagnostic fields. The target response is compared against
   the host-reference command for the same control update.

## Request-Response Transaction

At each controller update:

1. The host increments `control_index`.
2. The host sends one `REQ` record to the C2000 target.
3. The firmware parses the request into the controller input structure.
4. The firmware calls the controller-step function.
5. The firmware formats a `CMD` response.
6. The host accepts the response only if the returned sequence number matches
   the expected request.
7. The host stores the C2000 serial row and the host-reference row for the same
   `control_index`.

The request contains the vehicle state, wind state, mission geometry, no-go
parameters, energy parameters, obstacle list, nominal rudder and sail commands,
assurance margins, and timing values. The response contains the target rudder and
sail commands plus solver/status diagnostics, predicted margins, slack terms,
candidate-set metadata, intervention flag, and correction information.

## Evidence Files

The public evidence is stored in:

- `results/logs/*__python_reference.csv`: host-reference logs.
- `results/logs/*__pil_serial.csv`: C2000 serial PIL logs.
- `results/command_error/*command_error.csv`: merged control-update comparison
  files.
- `results/pil_serial_six_scenario_summary.csv`: compact six-scenario summary.
- `results/figures/pil_serial_six_scenario_command_error.png`: compact suite
  plot.
- `results/figures/*__pil_serial_command_error.png`: individual scenario plots.
- `results/figures/launchpad_hardware_setup.jpeg`: hardware setup image.
- `docs/source_notes/`: original flashing and serial test notes.
- `MANIFEST_SHA256.txt`: integrity hashes for the public evidence files.

## Interpretation

Across the six serial PIL scenarios, the host-reference logs and C2000 serial
logs contain 3562 plant rows and 714 matched controller updates. No row-count
mismatch, missing control update, or protocol failure was observed. The maximum
command differences were below `7e-14 deg`, which is numerical roundoff for this
comparison. This supports the statement that the embedded C2000 implementation
produced command-equivalent outputs for the tested scenarios.

## Public-Repository Boundary

This repository is scoped as an evidence release. It contains the logs,
summaries, figures, metadata, and source notes needed to inspect the PIL claim.
The broader simulation and source-code release is intentionally separate unless
the authors choose to publish it later.
