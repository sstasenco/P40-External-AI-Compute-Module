# Host connectivity options

## Preferred low-cost architecture

Host (ThinkStation P900)
-> PCIe x16 Gen4 SlimSAS adapter (2x SFF-8654 8i)
-> SlimSAS cable
-> PCIe x16 female-to-female adapter
-> PLX8796/PEX8796 switch board (6x SFF-8654)
-> 2x NVIDIA Tesla P40

Notes:
- Uses mostly off-the-shelf components.
- Avoids designing a custom PCIe switch PCB for the first prototype.
- Leaves room for a future custom backplane.
