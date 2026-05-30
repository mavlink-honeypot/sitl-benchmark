# ArduPilot SITL Parameters (v4.5.1)

These parameters were used for all baseline experiments in the paper.

## SITL Launch Command
```bash
sim_vehicle.py -v ArduCopter --console --map -L KSFO --out=tcpin:0.0.0.0:5760
```

## Key Parameters
- SERIAL0_PROTOCOL = 2 (MAVLink2)
- SERIAL0_BAUD = 921600
- LOG_BITMASK = 65535
- ARMING_CHECK = 1
- BRD_SAFETY_DEFLT = 0 (for SITL)
