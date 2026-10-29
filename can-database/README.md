# CAN Database

## Overview

This folder contains the CAN database file used by the **Automotive CAN Dashboard** project. The database defines CAN messages and signals used for communication between vehicle door status modules and the dashboard.

## Configured Messages

### 1. Front_Door_Status

- **CAN ID:** `0x101`
- **Frame Type:** Standard data frame
- **DLC:** 8 bytes
- **Signals:**
  - `Front_Left_Door_Status`
  - `Front_Right_Door_Status`

### 2. Rear_Door_Status

- **CAN ID:** `0x100`
- **Signals:**
  - `Rear_Right_Door_Status`
  - `Rear_Left_Door_Status`
  - `Boot_Door_Status`

## Files

The following CAN database file is included in this folder:

| File Name | Description |
|---|---|
| `CAN_exp6.dbc` | CAN database file containing message and signal definitions for the Automotive CAN Dashboard project. |

The `CAN_exp6.dbc` file can be imported into **TSMaster** to configure CAN communication, decode received CAN messages, and monitor vehicle door status signals during dashboard testing.

## Usage in TSMaster

1. Open TSMaster.
2. Import `CAN_exp6.dbc` into the CAN database configuration.
3. Verify the configured CAN message IDs and signal definitions.
4. Configure the CAN channel and start communication.
5. Monitor the front-door, rear-door, and boot-door status signals using the dashboard.

## Notes

- Ensure that the message and signal definitions match the actual CANdb++ configuration.
- Verify the CAN IDs, bit positions, signal lengths, byte order, scaling, and value definitions before testing.
- Confirm the signal encoding and decoding logic in TSMaster matches the dashboard implementation.
- The actual signal names and message properties should be verified against `CAN_exp6.dbc` before use in communication testing.
