# C2000 PIL Source Notes

These notes summarize the processor-in-the-loop path used to generate the
included WF-RS C2000 evidence.

The public repository is evidence-only. It includes logs, summaries, figures,
metadata, and setup notes. It does not include the full host runner or firmware
source unless a separate code release is approved.

## PIL Concept

```text
Host sailing simulation
        -> one controller-step request line
TI LAUNCHXL-F28379D C2000 firmware
        -> one rudder/sail command response line
Host simulation continues and writes paired logs
```

The host keeps the plant, wind, obstacle, and mission simulation. The C2000
target executes the controller step and returns command outputs.

## Recorded Hardware Path

- Target board: TI LAUNCHXL-F28379D / TMS320F28379D C2000.
- Serial link: SCI/UART over USB.
- Recorded serial port: `COM6`.
- Baud rate: `115200`.
- Target startup line: `READY,C2000_PIL`.
- Host request prefix: `REQ`.
- Target command prefix: `CMD`.

## Evidence Included In This Repository

- Paired host-reference and C2000 serial logs in `results/logs/`.
- Command-error comparisons in `results/command_error/`.
- Six-scenario summary in `results/pil_serial_six_scenario_summary.csv`.
- Figures in `results/figures/`.
- Integrity hashes in `MANIFEST_SHA256.txt`.

## Scope Reminder

This evidence supports embedded controller-step execution and command
equivalence. It is not field sailing, perception validation, hydrodynamic
identification, actuator validation, or a full hardware-in-the-loop test.
