# Project Structure

This repository is intended to grow from a simple build log into an engineering knowledge base for an external NVIDIA Tesla P40 AI compute module.

## Current documentation groups

- `docs/00-vision/` - project vision and purpose
- `docs/01-requirements/` - system requirements and constraints
- `docs/02-architecture/` - system architecture, external multi-GPU options, and memory sharing notes
- `docs/03-trade-studies/` - design alternatives and trade-offs
- `docs/04-risks/` - technical and project risks
- `docs/05-bom/` - draft bill of materials
- `docs/06-test-plan/` - validation and MVP test plan
- `docs/07-performance/` - performance notes and bandwidth estimates
- `docs/hardware/` - hardware-specific notes

## Newly added architecture documents

- `docs/02-architecture/EXTERNAL_MULTI_GPU_OPTIONS.md`
- `docs/02-architecture/MULTI_GPU_MEMORY.md`

## Proposed future documentation groups

### Hardware documentation

Recommended future files:

- `docs/hardware/PCIe_BACKPLANE.md`
- `docs/hardware/PCIe_SWITCH.md`
- `docs/hardware/POWER_DISTRIBUTION.md`
- `docs/hardware/COOLING.md`
- `docs/hardware/CHASSIS.md`
- `docs/hardware/CABLING.md`
- `docs/hardware/CONTROLLER_BOARD.md`
- `docs/hardware/MONITORING.md`

### Software documentation

Recommended future files:

- `docs/software/BIOS.md`
- `docs/software/LINUX.md`
- `docs/software/CUDA.md`
- `docs/software/NCCL.md`
- `docs/software/LLAMA_CPP.md`
- `docs/software/VLLM.md`
- `docs/software/EXLLAMAV2.md`

### Research documentation

Recommended future files:

- `docs/research/PCIe_MEMORY_SHARING.md`
- `docs/research/TENSOR_PARALLELISM.md`
- `docs/research/PCIe_SWITCHES.md`
- `docs/research/COOLING_CALCULATIONS.md`
- `docs/research/FUTURE_GPUS.md`

### Engineering asset folders

Recommended future top-level folders:

- `hardware/backplane/`
- `hardware/power-distribution/`
- `hardware/controller-board/`
- `hardware/front-panel/`
- `mechanical/cad/`
- `mechanical/step/`
- `mechanical/stl/`
- `mechanical/drawings/`
- `firmware/controller/`
- `software/setup/`
- `software/benchmarks/`
- `software/monitoring/`
- `images/`
- `references/`

## Documentation philosophy

The project should document both the final design and the reasoning behind each decision.

Important design decisions should include:

- what was selected
- what alternatives were considered
- why the selected option is acceptable
- known risks
- validation steps

## Current baseline

Reference Design v1 uses:

- Lenovo ThinkStation P900 host
- PCIe x16 to SlimSAS/SFF-8654 adapter path
- external PCIe adapter/riser chain
- PLX/PEX PCIe switch board
- two water-cooled NVIDIA Tesla P40 GPUs

## Long-term direction

The long-term direction is an external AI compute chassis with:

- custom PCIe backplane
- PCIe switch
- integrated 12 V power distribution
- liquid cooling
- monitoring controller
- clean cabling
- reproducible documentation
- software recipes for CUDA, NCCL, llama.cpp, ExLlamaV2, and vLLM
