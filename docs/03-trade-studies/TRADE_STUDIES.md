# Trade Studies

This section records design choices, alternatives, and reasons for selecting or rejecting options.

## Study 1 - Ready-made adapter chain vs custom PCB

### Option A: ready-made adapter chain

Components:

- P900 PCIe x16 slot
- PCIe x16 to 2x SlimSAS SFF-8654 8i adapter
- SlimSAS cables
- PCIe x16 female-to-female adapter/riser
- PLX/PEX switch board
- Tesla P40 GPUs

Pros:

- Lowest development effort.
- No custom high-speed PCB risk in Phase 1.
- Parts can be tested individually.
- Best fit for MVP.

Cons:

- More connectors and signal integrity risk.
- Mechanically messy.
- Documentation for generic adapter boards may be incomplete.
- Not a clean final product.

Decision: selected for Reference Design v1.

## Study 2 - SlimSAS/SFF-8654 vs OCuLink

### SlimSAS/SFF-8654

Pros:

- Common on server/storage adapter boards.
- Supports dense PCIe lane breakout.
- Available in many cable and board variants.

Cons:

- Many products are marketed for U.2/NVMe and may not be fully transparent for GPU use.
- Cable quality and length matter.

### OCuLink

Pros:

- Designed as an external PCIe-style connector family.
- Cleaner external module concept.

Cons:

- x16 OCuLink solutions are less common and may require multiple connectors.
- More custom design work may be needed.

Decision: SlimSAS/SFF-8654 for MVP; OCuLink remains a candidate for custom v2/v3 designs.

## Study 3 - PCIe switch board vs motherboard bifurcation

### PCIe switch board

Pros:

- Allows two GPUs behind one upstream connection.
- Does not rely on host bifurcation support.
- Better long-term direction for an external compute module.

Cons:

- PLX/PEX boards can be expensive and poorly documented.
- Requires attention to reset, reference clock, and power sequencing.

### Motherboard bifurcation only

Pros:

- Simpler if fully supported.
- Fewer active components.

Cons:

- Host BIOS must support the required split.
- Not all workstations expose useful bifurcation options.
- Does not solve clean external multi-GPU aggregation as well.

Decision: use PCIe switch board for the external dual-P40 module.

## Study 4 - Water cooling vs air cooling

### Water cooling

Pros:

- Makes Tesla P40 cards physically thinner.
- Better fit for compact external enclosure.
- Lower sustained temperatures under AI workloads.

Cons:

- Pump, radiator, reservoir, tubing, and leak risk.
- VRM/backside airflow may still be needed.

Decision: water cooling is selected because the project already assumes water blocks.
