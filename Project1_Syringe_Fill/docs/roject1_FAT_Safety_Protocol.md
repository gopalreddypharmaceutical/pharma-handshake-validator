# Factory Acceptance Testing (FAT) - Safety Interlock Dry-Run Protocol

**System ID:** FILL-SKID-101  
**Target Function:** Filling Zone Barrier Interlock Validation  
**Standard Reference:** GAMP 5 / 21 CFR Part 11 Data Integrity Constraints

### Test Procedure Loop 01: Enclosure Door Safety Interlock
*   **Objective:** Verify that opening the filling zone physical barrier enclosure instantly halts the filling needle assembly to prevent mechanical injury or sterility disruption.

| Step | Action Required | Expected Automation System Response | Pass/Fail | Verified By / Date |
| :--- | :--- | :--- | :--- | :--- |
| 1.0 | Bring the filling skid to active `RUNNING` state via the HMI terminal. | Conveyors run. Needles stroke continuously. HMI displays `System Status: In Production`. | | |
| 2.0 | Physically unlatch and open the access door to the filling needle enclosure (Limit Switch ZS-201). | Safety relay trips. Guard door open alarm is triggered on HMI screen. Needles stop instantly. | | |
| 3.0 | Attempt to press the `Start Cycle` button on the main control panel while the door remains open. | HMI prevents state transition. System blocks start permissive and remains in `Safe State`. | | |
| 4.0 | Close the guard door, clear the alarm text, and press `Safety Reset`. | System returns to `Idle` state. Start permissive becomes active. | | |

### Test Sign-Off
*   **Lead Automation Engineer Signature:** ___________________________
*   **Quality Assurance Auditor Signature:** ___________________________
