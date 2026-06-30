# Inspecting and Verifying the PIL Evidence

This public repository is evidence-only. It contains the logs, summaries,
figures, source notes, and hashes needed to inspect the embedded
processor-in-the-loop (PIL) validation result.

The full host runner and firmware source are intentionally not part of the
default public upload unless a separate code release is requested.

## What Can Be Checked From This Repository

1. Read the six-scenario summary:

   ```text
   docs/RESULTS_SUMMARY.md
   results/pil_serial_six_scenario_summary.csv
   ```

2. Inspect paired logs:

   ```text
   results/logs/*__python_reference.csv
   results/logs/*__pil_serial.csv
   ```

3. Inspect command-error files:

   ```text
   results/command_error/*command_error.csv
   results/command_error/pil_serial_six_scenario_summary.csv
   ```

4. Inspect generated figures:

   ```text
   results/figures/pil_serial_six_scenario_command_error.png
   results/figures/*__pil_serial_command_error.png
   ```

5. Check the hardware/setup notes:

   ```text
   docs/source_notes/
   ```

## Integrity Check

After downloading or copying this repository, compare files with
`MANIFEST_SHA256.txt`.

PowerShell example:

```powershell
Get-Content .\MANIFEST_SHA256.txt | Select-Object -First 10
Get-FileHash .\README.md -Algorithm SHA256
```

For a strict check, recompute hashes for the listed files with
`Get-FileHash -Algorithm SHA256` and compare the relative paths and hash strings
against `MANIFEST_SHA256.txt`.

## Hardware Context

The recorded PIL run used:

```text
Target board: TI LAUNCHXL-F28379D / TMS320F28379D C2000
Serial port: COM6
Baud rate: 115200
Startup message: READY,C2000_PIL
```

At each controller update, the host sent one `REQ` line to the target and
received one `CMD` line from the target. The included CSV logs and command-error
files document the matched update records.

## Optional Full Re-Run

A full re-run requires the host runner and firmware source package, the C2000
target, a flashed firmware image, and the original serial setup. Those files are
not included in the evidence-only public repository by default.

The evidence here supports the paper's embedded execution and command-equivalence
claim; it is not a full simulation-code release and not an on-water field trial.
