# osdagbridge-testing  # OsdagBridge Functional Testing & Structural Verification

FOSSEE Winter Internship 2026 · Osdag project · Screening task

**Author:** M. Sai Rishith Varma · B.Tech Civil Engineering (2nd year), IIT Hyderabad
**Contact:** rishithvarmamudunuri5@gmail.com · [GitHub](https://github.com/rishi-maker737)

## Overview

Functional testing of the **short-span steel girder bridge module** of OsdagBridge (IRC). The work checks input validation, project-location loads, deck concrete grade, multi-run state persistence (run, unlock, change, re-run) and the consistency of outputs, 3D CAD and design report with the inputs.

## Results at a glance

| Item | Result |
|---|---|
| Test cases | 8 (TC01–TC08) |
| Design runs | 24 (3 consecutive runs per test case) |
| Pass | 22 |
| Partial | 1 (TC08-R2) |
| Fail | 1 (TC08-R3) |

Key findings:
- Invalid inputs (span 19 m, 46 m, missing, negative, 99999 m) were rejected with no CAD output; boundary spans 20 m and 45 m were accepted.
- Unlocking, changing a parameter and re-running did not cause crashes or stale CAD/report data in the cases tested.
- Two related defects were found in TC08 where the **final design status disagrees with the individual check results**:
  - D1: no final design is given although all checks pass (TC08-R2)
  - D2: a final design is given although some checks fail (TC08-R3)

## Test cases

| ID | Purpose | Varied across R1 / R2 / R3 |
|---|---|---|
| TC01 | Baseline, default materials, girder section | baseline / one size smaller / one size larger |
| TC02 | Span lower-bound validation | 20 m / 19 m / 21 m |
| TC03 | Span upper-bound validation | 45 m / 46 m / 44 m |
| TC04 | Carriageway width | 7.5 m / 10.5 m / 5.5 m |
| TC05 | Location and climatic loads | Mumbai / Varanasi / Gulmarg (J&K) |
| TC06 | Deck concrete grade | M40 / M50 / M60 |
| TC07 | Invalid and edge inputs | span not given / −30 / 99999 |
| TC08 | Combined multi-run | span 30 / 30 + 5 girders / 40 + 5 girders |

Default inputs unless varied: span 30 m, carriageway 7.5 m, skew 0°, girder / cross bracing / end diaphragm E 350A, deck M40.

## Repository structure

```
osdagbridge-testing/
├── README.md
├── test-logs/     Test log (XLSX and CSV), one row per run
├── osi-files/     Saved OsdagBridge project (.osi) files per run
├── screenshots/   Evidence screenshots, named TCxx_Ry_description.png
├── issues/        Text of the GitHub issues raised (D1, D2)
├── report/        Final PDF report and LaTeX source
└── notes/         Installation notes, resume, other notes
```

## Links

- Demo video: **ADD VIDEO LINK**
- GitHub issues raised on [Nidhikhare12/OsdagBridge](https://github.com/Nidhikhare12/OsdagBridge):
  - D1: **ADD ISSUE LINK**
  - D2: **ADD ISSUE LINK**

## Environment

- OS: **ADD OS / VERSION / ARCHITECTURE**
- OsdagBridge build: **ADD BUILD / DOWNLOAD DATE** (downloaded from https://garvit000.github.io/OsdagBridge/)

## How to reproduce a run

1. Open the short-span steel girder bridge module in OsdagBridge.
2. Enter the inputs listed in the test log for the run (Input Values column).
3. Run the design and compare with the Expected Result column.
4. Unlock the module, change only the listed parameter and run again.

## Verdict criteria

- **Pass:** behaviour matched the expected result. For invalid inputs, the software rejected the input and produced no CAD.
- **Partial:** core run worked but part of the output was incomplete or inconsistent.
- **Fail:** behaviour contradicted the expected result.

## Limitations

- Numerical utilisation ratios were not logged, so no hand-calculation check is reported.
- Steel grade was E 350A for all steel components in all runs; custom steel properties are not covered.
- Skew angle was 0° in all runs.
