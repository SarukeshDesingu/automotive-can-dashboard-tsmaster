# Dashboard Scripts

## Overview

This section documents the C script and event-handling logic used in the **Automotive CAN Dashboard** project. The script reads system variables for ignition, speed, and brake values, processes the inputs, and updates the corresponding dashboard status variables.

The source code is included directly in this README for easy reference.

## Current Logic

The dashboard script implements the following functions:

- **Ignition Status:** Enables or disables the dashboard logic based on the ignition value.
- **Speed Validation:** Restricts the input speed to a range of 0 to 100.
- **Brake Validation:** Restricts the brake value to a range of 0 to 100.
- **Brake Status LED:** Turns the brake status indicator ON when the brake value is greater than zero.
- **Speed Calculation:** Reduces the speed by the brake value and prevents the resulting speed from becoming negative.
- **Dashboard Updates:** Updates the ignition, speed, and brake status system variables.

## Source Code

The following C script implements the dashboard logic using TSMaster system variable APIs.

```c
s32 Ignition = 0;
s32 Speed = 0;
s32 Brake = 0;

app.get_system_var_int32("Ignition", &Ignition);
app.get_system_var_int32("Speed", &Speed);
app.get_system_var_int32("Brake", &Brake);

if (Ignition == 1)
{
    /* Ignition ON */
    app.set_system_var_int32("Ignition_status", 1);

    /* Keep Speed within 0-100 */
    if (Speed < 0)
    {
        Speed = 0;
    }

    if (Speed > 100)
    {
        Speed = 100;
    }

    /* Keep Brake within 0-100 */
    if (Brake < 0)
    {
        Brake = 0;
    }

    if (Brake > 100)
    {
        Brake = 100;
    }

    /* Brake status LED */
    if (Brake > 0)
    {
        app.set_system_var_int32("Brake_status", 1);
    }
    else
    {
        app.set_system_var_int32("Brake_status", 0);
    }

    /* Reduce speed according to brake value */
    Speed = Speed - Brake;

    /* Speed cannot be negative */
    if (Speed < 0)
    {
        Speed = 0;
    }

    /* Display actual speed */
    app.set_system_var_int32("Speed_status", Speed);
}
else
{
    /* Ignition OFF */
    app.set_system_var_int32("Ignition_status", 0);

    /* System OFF */
    app.set_system_var_int32("Speed_status", 0);
    app.set_system_var_int32("Brake_status", 0);
}
```

## Code Explanation

### 1. System Variable Initialization

The variables `Ignition`, `Speed`, and `Brake` are initialized to zero. The script then reads their current values using the system variable retrieval API.

### 2. Ignition Control

When `Ignition == 1`, the script sets `Ignition_status` to `1` and executes the speed and brake processing logic. Otherwise, it sets the ignition status, speed status, and brake status to zero.

### 3. Speed and Brake Validation

Both speed and brake values are restricted to the range of 0 to 100. Values below zero are set to zero, while values above 100 are set to 100.

### 4. Brake Status Indication

The `Brake_status` variable is set to `1` when the brake value is greater than zero. If the brake value is zero, the brake status is set to `0`.

### 5. Speed Calculation

The brake value is subtracted from the validated speed value:

**Final Speed = Speed − Brake**

If the calculated speed becomes negative, it is set to zero. The resulting value is then written to `Speed_status`.

## System Variables

| System Variable | Purpose |
|---|---|
| `Ignition` | Input variable representing ignition state |
| `Speed` | Input variable representing speed |
| `Brake` | Input variable representing brake value |
| `Ignition_status` | Output variable indicating ignition state |
| `Speed_status` | Output variable displaying the calculated speed |
| `Brake_status` | Output variable controlling the brake status indicator |

## Configuration and Usage

1. Configure the required system variables in TSMaster.
2. Associate the script or event handler with the appropriate trigger.
3. Ensure the variable names in the script match the configured system variable names.
4. Run the dashboard application and change the ignition, speed, and brake inputs.
5. Verify that the status indicators and displayed speed update as expected.

## Notes

- The script uses TSMaster system variable APIs to read input values and update dashboard outputs.
- The speed and brake values are validated before the speed calculation.
- The calculated speed represents a simplified dashboard simulation in which the brake value is directly subtracted from the speed value.
- This calculation is intended for dashboard demonstration and does not represent a physical vehicle braking model.
- The script should be tested with the actual dashboard configuration to verify correct event triggering and variable updates.
