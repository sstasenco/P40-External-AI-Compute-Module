# Requirements

## Functional requirements

- Support two NVIDIA Tesla P40 GPUs in an external enclosure.
- Use Lenovo ThinkStation P900 as the initial host system.
- Provide a PCIe connection path from the host to an external PCIe switch board.
- Provide stable 12 V power for both GPUs.
- Provide cooling suitable for sustained AI/LLM inference workloads.
- Allow Linux to enumerate both GPUs reliably.
- Support CUDA/NVIDIA driver validation and basic multi-GPU testing.

## Non-functional requirements

- Prefer low-cost and available components for MVP.
- Avoid custom high-speed PCB design in Phase 1.
- Keep the design modular enough to replace adapters with a custom backplane later.
- Document risks, wiring, test results, and component assumptions.
- Make the design reproducible by another builder with similar hardware.

## MVP constraints

- Host: Lenovo ThinkStation P900.
- GPUs: 2x NVIDIA Tesla P40.
- Cooling: water blocks already planned/available.
- First connection approach: PCIe x16 to SlimSAS/SFF-8654 adapters and external PLX/PEX switch board.
- Final performance is less important than stable enumeration and repeatable operation during Phase 1.

## Open questions

- Exact lane bifurcation behavior of the P900 host slot.
- Compatibility of each adapter board with GPU-class PCIe traffic rather than only U.2/NVMe usage.
- Required cable lengths for stable PCIe Gen3 operation.
- Whether the PLX/PEX switch board handles PERST#, REFCLK, sideband signals, and endpoint reset as expected.
