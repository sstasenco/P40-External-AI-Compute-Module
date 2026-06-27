# Performance Notes

## Initial expectation

The first goal is not maximum bandwidth. The first goal is stable enumeration and reliable dual-GPU operation.

Tesla P40 is a PCIe Gen3 GPU. Even if some adapter boards are advertised as PCIe Gen4, the MVP should be validated as a Gen3-class system first.

## Performance factors

- Upstream link width from P900 to switch board.
- Switch board lane allocation.
- Cable quality and length.
- Link training generation and width.
- Whether workloads require heavy host-to-GPU transfer or mostly run in GPU memory.

## AI/LLM implication

For many local inference workloads, PCIe bandwidth is less important than:

- GPU memory capacity.
- Model placement.
- Batch size.
- CPU RAM and storage speed.
- Stable driver operation.

A lower PCIe link speed may still be acceptable if models remain resident in GPU VRAM during inference.

## Measurements to collect

- `nvidia-smi topo -m`
- PCIe link width and speed from `lspci -vv`
- Host-to-device bandwidth using CUDA bandwidth tests
- Inference tokens/sec for selected models
- GPU utilization and power draw
- Temperature under sustained load

## MVP success definition

A successful MVP may run below ideal theoretical PCIe bandwidth if both GPUs remain stable and usable for real AI workloads.
