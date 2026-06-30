# LAUNCHXL-F28379D Flashing And SCI Bring-Up Notes

Date: 2026-06-27  
Board: TI LAUNCHXL-F28379D  
Recorded serial port: `COM6`  
Recorded baud rate: `115200`

## Result

The board flashing/debug path worked for the recorded PIL evidence run.

Confirmed working:

- Windows detected the XDS100 debug/serial interface.
- Code Composer Studio could load/debug the C28x CPU1 target.
- A RAM build could run on the board.
- LaunchPad LEDs blinked from firmware.
- A serial terminal received readable SCI/UART output from the board.
- The serial PIL request/response firmware was built, flashed, and validated
  over `COM6` at `115200` baud.

Serial terminal settings used:

```text
Serial line: COM6
Baud: 115200
Data bits: 8
Stop bits: 1
Parity: None
Flow control: None
```

## Bring-Up Issue Summary

The first imported TI SCI echo example required board-specific cleanup before
the PIL protocol was tested. The important issues were:

- the imported example expected a different CCS product registration;
- LaunchPad SCI pins differ from generic/controlCARD pin mappings;
- the LaunchPad clock setup needed to match the board crystal;
- the original example could halt on receive errors;
- the original example printed only once and then waited for input, which made
  serial bring-up harder to inspect.

The final test firmware used a line-oriented SCI bridge:

```text
Startup output: READY,C2000_PIL
Input: one ASCII REQ,... line
Processing: parse request and execute the controller step
Output: one ASCII CMD,... line
```

## PIL Firmware Evidence Result

The recorded serial test passed for the single-scenario bring-up and was then
extended to the six-scenario package included in this repository.

Single-scenario bring-up result:

```text
scenario: s2_obstacle_easy_wind
transport: serial
reference rows: 415
pil rows: 415
control updates compared: 83
max abs rudder error: 3.41949e-14 deg
max abs sail error: 2.4869e-14 deg
```

Six-scenario evidence summary:

```text
total plant rows: 3562
matched controller updates: 714
protocol failures: 0
maximum command error: below 7e-14 deg
```

## Why This Matters For PIL

This bring-up validated the communication path needed for processor-in-the-loop:

```text
Host simulator -> serial request -> C2000 firmware -> serial response -> host log
```

The included logs and command-error files document the final matched
host-reference and C2000 serial outputs.

## Public-Repository Boundary

Absolute local workspace paths, IDE project paths, and source-code build details
are intentionally omitted from this public note. They are not needed to inspect
the evidence package and should not be treated as part of the paper's public
artifact unless a separate source-code release is approved.
