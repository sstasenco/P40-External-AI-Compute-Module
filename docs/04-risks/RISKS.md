# Risk Register

## R1 - PCIe signal integrity

Risk: Multiple adapters, risers, and cables may degrade signal quality.

Impact: GPUs may not enumerate, may downtrain, or may become unstable under load.

Mitigation:

- Start at PCIe Gen3 or lower if needed.
- Use short, high-quality SlimSAS cables.
- Test each segment independently.
- Avoid unnecessary adapters in the final design.

## R2 - Adapter board compatibility

Risk: Some SFF-8654 adapter boards are intended for U.2/NVMe and may not correctly pass all signals needed for GPU-class PCIe use.

Impact: Link training, reset, or endpoint detection may fail.

Mitigation:

- Document exact boards used.
- Test with one GPU first.
- Verify PERST#, REFCLK, lane mapping, and power assumptions.

## R3 - Power sequencing

Risk: Host and external GPU enclosure may power up at different times.

Impact: PCIe enumeration failures or unstable reset behavior.

Mitigation:

- Power the external enclosure before or together with the host.
- Add controlled enable/reset logic in later prototypes.
- Document a repeatable boot sequence.

## R4 - GPU power delivery

Risk: Two Tesla P40 GPUs require significant 12 V current.

Impact: Connector heating, voltage drop, PSU shutdown, or instability.

Mitigation:

- Use a PSU with sufficient 12 V capacity.
- Use proper wire gauge and connectors.
- Measure voltage at GPU power inputs under load.

## R5 - Cooling loop reliability

Risk: Water cooling introduces leak and pump failure risk.

Impact: GPU damage or thermal shutdown.

Mitigation:

- Leak-test before powering electronics.
- Use flow and temperature monitoring.
- Add airflow over VRMs/backplates.

## R6 - Mechanical stress

Risk: Adapter chains and cables may mechanically stress PCIe connectors.

Impact: Intermittent contact or board damage.

Mitigation:

- Use brackets and strain relief.
- Avoid unsupported heavy adapters.
- Move toward a custom backplane after MVP validation.
