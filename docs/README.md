# Documentation Index

## Core documents

- [Vision](00-vision/VISION.md)
- [Requirements](01-requirements/REQUIREMENTS.md)
- [Architecture](02-architecture/ARCHITECTURE.md)
- [External Multi-GPU Architecture Options](02-architecture/EXTERNAL_MULTI_GPU_OPTIONS.md)
- [Multi-GPU Memory Sharing and Communication](02-architecture/MULTI_GPU_MEMORY.md)
- [Trade Studies](03-trade-studies/TRADE_STUDIES.md)
- [Risks](04-risks/RISKS.md)
- [BOM Draft](05-bom/BOM_DRAFT.md)
- [Test Plan](06-test-plan/TEST_PLAN.md)
- [Performance Notes](07-performance/PERFORMANCE_NOTES.md)
- [Roadmap](ROADMAP.md)

## Hardware-specific notes

- [Host to Dual P40 Options](hardware/HOST_TO_DUAL_P40_OPTIONS.md)
- [Project Structure](PROJECT_STRUCTURE.md)

## Suggested future documentation groups

- PCIe backplane design
- PCIe switch selection
- Power distribution
- Liquid cooling system
- External chassis and mechanical layout
- BIOS/Linux/CUDA/NCCL setup
- llama.cpp, ExLlamaV2, vLLM configuration
- Benchmarking and validation

## Current reference design

The current baseline is Reference Design v1: P900 host, PCIe x16 to SlimSAS/SFF-8654 adapter path, external PLX/PEX switch board, and two water-cooled Tesla P40 GPUs.

The key architectural assumption is that Tesla P40 cards do not support NVLink. Multi-GPU workloads must therefore use PCIe-based software approaches such as CUDA P2P, CUDA Unified Memory, NCCL, tensor parallelism, or explicit model/layer splitting.
