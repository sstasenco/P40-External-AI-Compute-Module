# External Multi-GPU Architecture Options

## Objective

The goal of the project is to build a compact external AI accelerator based on multiple NVIDIA Tesla P40 GPUs connected to a single host computer.

The design should maximize PCIe bandwidth, minimize unnecessary latency, and remain practical enough to build in stages.

---

## Architecture 1: Direct PCIe Connection

```text
Host
 |
PCIe x16
 |
Tesla P40
```

### Advantages

- Lowest complexity
- Lowest latency
- Best baseline for testing one GPU
- Useful for validating drivers, cooling, and power

### Disadvantages

- Only one GPU
- No shared external enclosure concept
- No expansion path

### Recommended use

Use as an early test path before building the dual-GPU external module.

---

## Architecture 2: Adapter Chain MVP

```text
Lenovo ThinkStation P900
    |
PCIe x16 slot
    |
PCIe x16 to SlimSAS / SFF-8654 adapter
    |
SlimSAS / SFF-8654 cables
    |
External PCIe adapter / riser chain
    |
PLX / PEX PCIe switch board
    |
    +--> Tesla P40 #1
    |
    +--> Tesla P40 #2
```

### Advantages

- Uses mostly off-the-shelf parts
- Good MVP path
- Allows early validation of PCIe topology
- Avoids custom PCB design at the beginning

### Disadvantages

- More connectors and adapters
- More signal integrity risk
- Mechanically less clean
- Requires careful power sequencing and cable management

### Recommended use

This is the current baseline for Reference Design v1.

---

## Architecture 3: PCIe Switch Backplane

```text
Host
 |
External PCIe cable
 |
Custom backplane
 |
PCIe switch
 |
 +--> Tesla P40 #1
 +--> Tesla P40 #2
```

### Advantages

- Cleaner architecture
- Better mechanical design
- Better signal integrity control
- More predictable P2P behavior
- Centralized power and monitoring

### Disadvantages

- Requires custom PCB design
- Requires high-speed PCIe layout expertise
- Higher development cost

### Recommended use

Reference Design v2.

---

## Architecture 4: Integrated AI Compute Chassis

```text
Host
 |
External PCIe x16 / x8 cable
 |
Integrated controller + PCIe switch board
 |
 +--> GPU module 1
 +--> GPU module 2
 +--> optional GPU module 3
 +--> optional GPU module 4
```

### Advantages

- Scalable platform
- Cleanest final architecture
- Supports future GPUs
- Enables proper monitoring, cooling, and serviceability

### Disadvantages

- Highest complexity
- Requires full electrical, thermal, firmware, and mechanical design

### Recommended use

Long-term platform architecture after the MVP is validated.

---

## Recommended Project Path

1. Build the adapter-chain MVP using off-the-shelf PCIe/SlimSAS/SFF-8654 components.
2. Validate GPU enumeration, CUDA, P2P, thermals, and power stability.
3. Document all bottlenecks and failure modes.
4. Replace the adapter chain with a custom backplane.
5. Integrate power distribution, monitoring, and cooling control.
6. Expand toward a reusable external AI compute chassis.
