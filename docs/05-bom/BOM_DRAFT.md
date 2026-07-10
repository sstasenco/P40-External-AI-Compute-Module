# Draft Bill of Materials

This BOM is a draft for Reference Design v1. Exact part numbers should be verified before purchase.

## Host side

| Item | Purpose | Status |
|---|---|---|
| Lenovo ThinkStation P900 | Host workstation | Existing |
| PCIe x16 slot | Upstream PCIe connection | Existing |
| PCIe x16 to 2x SlimSAS SFF-8654 8i adapter | Host-side lane breakout / cable interface | Candidate |
| SlimSAS/SFF-8654 cables | External PCIe cable path | Candidate |

## External PCIe path

| Item | Purpose | Status |
|---|---|---|
| PCIe x16 female-to-female adapter/riser | Adapter between cable path and switch board | Candidate |
| PLX8796 / PEX8796 or similar PCIe switch board | Fan-out from one upstream link to two GPU endpoints | Candidate |
| SFF-8654 cables | Link from switch board to GPU adapters/slots | Candidate |
| PCIe x16 risers or GPU slot adapters | Mechanical/electrical connection to GPUs | Candidate |

## GPUs

| Item | Purpose | Status |
|---|---|---|
| NVIDIA Tesla P40 #1 | AI compute GPU | Existing |
| NVIDIA Tesla P40 #2 | AI compute GPU | Existing |
| GTX 1080 Ti-compatible water blocks if mechanically compatible | GPU cooling | Existing/candidate |

## Power

| Item | Purpose | Status |
|---|---|---|
| External ATX/server PSU | 12 V supply for GPUs and pumps/fans | Candidate |
| PCIe GPU power cables | GPU auxiliary power | Candidate |
| Power distribution block or harness | Safe 12 V distribution | Candidate |
| Inline fuses or protection | Safety | Recommended |

## Cooling

| Item | Purpose | Status |
|---|---|---|
| Pump, D5/DDC or equivalent | Coolant circulation | Candidate |
| Radiator | Heat rejection | Candidate |
| Reservoir | Filling and bleeding | Candidate |
| Tubing and fittings | Cooling loop | Candidate |
| Fans | Radiator and VRM airflow | Candidate |
| Coolant temperature sensor | Monitoring | Recommended |
| Flow indicator/sensor | Pump/flow validation | Recommended |

## Mechanical

| Item | Purpose | Status |
|---|---|---|
| External enclosure | GPU module chassis | To design |
| GPU support brackets | Avoid connector stress | To design |
| Cable strain relief | Protect PCIe/SlimSAS connections | To design |
| PSU mounting | Safe power integration | To design |
