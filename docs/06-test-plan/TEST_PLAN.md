# MVP Test Plan

## Test goal

Validate that the P900 can reliably enumerate and use two external Tesla P40 GPUs through the proposed SlimSAS + PCIe switch path.

## Stage 0 - Bench safety

- Inspect all adapters and cables.
- Verify PSU output voltage before connecting GPUs.
- Leak-test water cooling loop without powering GPUs.
- Confirm pump and fans run reliably.

## Stage 1 - Single GPU local baseline

- Install one Tesla P40 directly in the P900 if physically possible.
- Install NVIDIA driver and CUDA tools.
- Run `nvidia-smi`.
- Record baseline temperature, power, PCIe link width, and PCIe generation.

## Stage 2 - External path without switch, if possible

- Test one GPU through the shortest external adapter path.
- Confirm enumeration.
- Compare PCIe link training with baseline.
- Run a light CUDA workload.

## Stage 3 - Switch board with one GPU

- Connect host to PLX/PEX switch board.
- Attach one Tesla P40.
- Confirm that the switch and GPU appear in `lspci`.
- Confirm NVIDIA driver detects the GPU.

## Stage 4 - Switch board with two GPUs

- Attach both Tesla P40 GPUs.
- Confirm both GPUs appear in `lspci` and `nvidia-smi`.
- Record PCIe topology with `lspci -tv`.
- Run independent workloads on both GPUs.

## Stage 5 - Stability test

- Run sustained inference or CUDA stress workload.
- Monitor GPU temperature, coolant temperature, PSU voltage, and system logs.
- Check for PCIe AER errors, driver resets, or GPU dropouts.

## Commands to record

```bash
lspci -tv
lspci -vv | grep -A 20 -i nvidia
nvidia-smi
nvidia-smi topo -m
nvidia-smi dmon
journalctl -k | grep -iE 'pcie|aer|nvrm|xid'
```

## Pass criteria for MVP

- Both Tesla P40 GPUs enumerate reliably.
- Both GPUs are visible in `nvidia-smi`.
- Both GPUs can run workloads simultaneously.
- No repeatable PCIe errors under moderate load.
- Cooling remains stable under sustained test load.
