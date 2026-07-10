# Multi-GPU Memory Sharing and Communication

## Summary

NVIDIA Tesla P40 GPUs do not support physical NVLink bridges. As a result, two or more P40 cards cannot create a hardware-level shared VRAM pool.

For this project, all multi-GPU memory sharing and synchronization must be handled through software over PCIe.

The practical options are:

1. CUDA Unified Memory
2. CUDA Peer-to-Peer access
3. Tensor parallelism in AI inference frameworks
4. NCCL-based GPU communication

This means the system can use the aggregate VRAM capacity of multiple P40 cards for large AI workloads, but it should be documented as distributed GPU memory, not true pooled memory.

---

## 1. CUDA Unified Memory

CUDA Unified Memory, also called Managed Memory, can be allocated with:

```cpp
cudaMallocManaged(...)
```

It creates a single virtual address space visible to the CPU and all CUDA-capable GPUs in the system.

### How it works

Memory pages migrate automatically to the CPU or GPU that accesses them.

If GPU #1 needs data currently resident near GPU #0, the CUDA runtime can migrate or map that data across the PCIe fabric.

### Advantages

- Simple programming model
- One pointer visible from CPU and GPUs
- No explicit application-managed copy path

### Limitations

- Page migration over PCIe has high latency
- Cross-GPU page movement can become a major bottleneck
- It is not equivalent to NVLink memory pooling
- Best for correctness and simplicity, not maximum multi-GPU inference performance

---

## 2. CUDA Peer-to-Peer Access

CUDA Peer-to-Peer, or P2P, allows one GPU to directly access memory on another GPU without staging the transfer through system RAM.

Typical CUDA flow:

```cpp
cudaDeviceCanAccessPeer(&canAccessPeer, gpu0, gpu1);
cudaSetDevice(gpu0);
cudaDeviceEnablePeerAccess(gpu1, 0);
```

### How it works

When peer access is available, GPU #0 can read from or write to GPU #1 memory through the PCIe topology.

### Requirements

- Both GPUs must support CUDA peer access
- The motherboard/PCIe topology must allow peer traffic
- The cards should ideally be under the same CPU root complex or the same PCIe switch
- BIOS must support large PCIe memory mapping

### Important topology note

For the P40 external module, a PCIe switch board is strongly preferred because it keeps both GPUs inside the same PCIe hierarchy and improves the chance of stable P2P communication.

---

## 3. Tensor Parallelism for AI and LLM Inference

For large language models, the preferred approach is not CUDA Unified Memory. The better solution is to split model weights and computation across GPUs using tensor parallelism or layer splitting.

Useful frameworks:

- `llama.cpp`
- `ExLlamaV2`
- `vLLM`
- Hugging Face Text Generation Inference
- custom PyTorch/CUDA workloads using NCCL

### Effective VRAM capacity

| GPU count | Physical VRAM | Practical meaning |
|---:|---:|---|
| 1 x P40 | 24 GB | Single-GPU model hosting |
| 2 x P40 | 48 GB | Distributed model storage |
| 3 x P40 | 72 GB | Larger sharded models |
| 4 x P40 | 96 GB | Larger multi-GPU inference node |

This is not one continuous VRAM pool. It is distributed model placement controlled by software.

---

## 4. NCCL Communication

NVIDIA NCCL provides optimized collective communication between GPUs.

Common operations include:

- broadcast
- all-reduce
- reduce-scatter
- all-gather
- point-to-point communication

On Tesla P40, NCCL traffic runs over PCIe because NVLink is not available.

---

## 5. BIOS and Platform Requirements

The host platform should be configured with the following settings.

### Above 4G Decoding

Required.

This allows the firmware to map large PCIe memory regions for multiple GPUs.

Without it, systems may show:

- missing GPUs
- BAR mapping failures
- unstable driver initialization
- unavailable P2P access

### Resizable BAR / Large BAR

Recommended when supported and stable.

Support depends on motherboard firmware, chipset, and GPU behavior. It should be tested rather than assumed.

### PCIe speed and width

Recommended target:

- PCIe Gen3 x16 per GPU where possible
- PCIe Gen3 x8 as an acceptable compromise
- avoid PCIe x4 for serious LLM inference

### CPU socket topology

For dual-socket systems such as the Lenovo ThinkStation P900, both GPUs should ideally be routed through the same CPU socket or through the same PCIe switch.

Cross-socket traffic can add latency and reduce bandwidth.

---

## 6. Performance Implications

Tesla P40 multi-GPU communication is limited by PCIe bandwidth.

Approximate PCIe Gen3 bandwidth:

| Link | One-direction theoretical bandwidth |
|---|---:|
| Gen3 x4 | ~3.9 GB/s |
| Gen3 x8 | ~7.9 GB/s |
| Gen3 x16 | ~15.8 GB/s |

This is far below modern NVLink bandwidth.

Therefore, workloads should be designed to:

- minimize cross-GPU transfers
- keep tensors local whenever possible
- use tensor parallelism carefully
- avoid excessive Unified Memory page migration
- benchmark real model behavior on the final topology

---

## Project Takeaway

Tesla P40 GPUs cannot physically pool VRAM. The project should treat multi-GPU memory as software-managed distributed memory over PCIe.

The preferred software strategy for large LLM inference is tensor parallelism or explicit layer/model splitting, not transparent Unified Memory.

The preferred hardware strategy is a PCIe switch-based external module that keeps all GPUs under one predictable PCIe hierarchy.
