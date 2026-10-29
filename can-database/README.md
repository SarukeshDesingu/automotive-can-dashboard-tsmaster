# CAN Database

## Overview

This folder contains the CAN database used by the Automotive CAN Dashboard project, if the database file is available for sharing.

## Configured Messages

### Front_Door_Status
- CAN ID: `0x101`
- Frame type: Standard data frame
- DLC: 8 bytes
- Signals:
  - `Front_Left_Door_Status`
  - `Front_Right_Door_Status`

### Rear_Door_Status
- CAN ID: `0x100`
- Signals:
  - `Rear_Right_Door_Status`
  - `Rear_Left_Door_Status`
  - `Boot_Door_Status`

## Files

Add the exported CAN database file here if permitted, and document its format and how it is used in TSMaster.

## Notes

The message and signal definitions should match the actual CANdb++ configuration. Verify the bit positions, lengths, byte order, and value definitions before using the database for communication testing.
