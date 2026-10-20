# Functional Design Specification (FDS) - Liquid Filling Skid (Skid-101)

## 1. System Overview
This document defines the functional control sequences for the automated sterile syringe filling and stoppering machine. The system is controlled via a centralized Allen-Bradley ControlLogix PAC interfacing with distributed remote I/O blocks over an EtherNet/IP network.

## 2. Sequence of Operations (Filling Zone Loops)
The system executes a deterministic sequence to ensure sterile filling and prevent product loss:

*   **Permissive to Start:** Autoclave cycle validation bit must be high, and localized LAF (Laminar Air Flow) differential pressure must sit within 12 Pa to 18 Pa.
*   **Syringe Infeed:** A proximity sensor (ZSC-101) detects the presence of a nested syringe tub. The servo drive indexes the tub into the filling track.
*   **No Bottle, No Fill Interlock:** If the optical sensor (PE-102) fails to detect a syringe in the target pocket, the respective filling pump clutch is bypassed. This prevents product spraying onto the conveyor bed.
*   **Filling Cycle:** The rotary piston pumps or peristaltic dosing units stroke down. An analog weight transmitter (WT-103) verifies the target fill volume (Target: 1.0 mL, Tolerance: ±0.02 mL).
*   **Stoppering Cycle:** Nitrogen purge valves open to displace oxygen before a vacuum arm seats the elastomeric stopper into the syringe barrel.

## 3. Alarms & Fail-Safe Matrix

| Alarm ID | Tag Name | Condition | Hazard Mitigation | Fail-Safe Action |
| :--- | :--- | :--- | :--- | :--- |
| ALM-101 | PDT-104 | Filling Zone Low DP (<10 Pa) | Breach of sterile boundary | Immediate controlled stop of all conveyors; isolate fill needles. |
| ALM-102 | E-STOP-1 | Emergency Stop Engaged | Physical hazard to operator | De-energize all VFDs and servo coils via safety relays. |
| ALM-103 | WT-ERR | Weight Deviation Out of Spec | Under-dose / Over-dose batch | Automatically divert the failed syringe to the reject chute. |
