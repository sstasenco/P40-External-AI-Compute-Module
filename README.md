# P40 External AI Compute Module

External dual NVIDIA Tesla P40 compute module project for local AI and LLM workloads.

## Current direction

The project starts with the most accessible MVP design:

```text
Lenovo ThinkStation P900
    -> PCIe x16 to SlimSAS/SFF-8654 adapter
    -> SlimSAS cabling
    -> external PCIe adapter/riser path
    -> PLX/PEX PCIe switch board
    -> 2x water-cooled NVIDIA Tesla P40
```

The long-term goal is to evolve this into a cleaner external AI compute enclosure with a custom backplane, robust power distribution, cooling, monitoring, and documentation.

## Documentation

Start here:

- [Documentation Index](docs/README.md)
- [Project Roadmap](docs/ROADMAP.md)
- [Architecture Overview](docs/02-architecture/ARCHITECTURE.md)
- [Trade Studies](docs/03-trade-studies/TRADE_STUDIES.md)
- [MVP Test Plan](docs/06-test-plan/TEST_PLAN.md)

## Project principles

- Build a working prototype first.
- Use off-the-shelf adapters before designing custom PCIe hardware.
- Document every trade-off and risk.
- Treat the repository as both a build log and an engineering knowledge base.
