# Project Vision

## Goal

Build an external AI compute module based on two NVIDIA Tesla P40 GPUs, connected to a Lenovo ThinkStation P900 host through an external PCIe path.

The project should start with the most accessible working prototype and then evolve toward a cleaner custom backplane or PCIe switch board.

## Core idea

The first design should avoid a custom high-speed PCIe PCB. Instead, it should use available adapter boards, SlimSAS/SFF-8654 cabling, a PLX/PEX switch board, external power, and water-cooled Tesla P40 cards.

## Target use cases

- Local AI and LLM inference
- Experimentation with multi-GPU PCIe topology
- External GPU compute enclosure research
- Documentation of practical trade-offs for low-cost AI hardware

## Design philosophy

1. Build a working MVP first.
2. Prefer reversible, off-the-shelf parts during early phases.
3. Document every trade-off and failure.
4. Treat the custom backplane as v2, not as the first milestone.
5. Keep the project useful as both a build log and an engineering reference.
