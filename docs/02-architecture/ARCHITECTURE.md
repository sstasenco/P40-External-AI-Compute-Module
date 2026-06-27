# Architecture Overview

## Reference Design v1 - Low-cost MVP

```text
Lenovo ThinkStation P900
    |
    | PCIe x16 slot
    v
PCIe x16 to 2x SlimSAS SFF-8654 8i adapter
    |
    | SlimSAS / SFF-8654 cables
    v
External PCIe adapter / riser chain
    |
    v
PLX/PEX PCIe switch board
    |
    +--> Tesla P40 GPU #1
    |
    +--> Tesla P40 GPU #2
```

## Main subsystems

### 1. Host interface

The P900 provides the upstream PCIe connection. The first prototype should use a standard PCIe slot rather than modifying the workstation motherboard.

### 2. External PCIe transport

SlimSAS/SFF-8654 cabling is used as a practical external transport method for PCIe lanes. The MVP should assume Gen3 operation first, even if some adapter boards are advertised as Gen4.

### 3. PCIe switch

The external PLX/PEX switch board is responsible for exposing two GPU endpoints to the host through a single upstream path.

### 4. GPU module

The external enclosure contains two Tesla P40 cards, water blocks, PCIe mechanical support, power wiring, and cooling loop components.

### 5. Power subsystem

The GPU enclosure should provide independent 12 V power for both GPUs and auxiliary electronics. The host should not be expected to power the external GPUs through the PCIe slot path.

### 6. Cooling subsystem

Both Tesla P40 cards should be cooled by water blocks. The enclosure should include radiator, pump, reservoir, tubing, fittings, coolant, and airflow over VRM/backplate areas if required.

## Design direction

Reference Design v1 is a working lab prototype. Reference Design v2 may replace the adapter chain with a custom backplane. Reference Design v3 may integrate the PCIe switch, power distribution, management controller, and external connector into a custom board.
