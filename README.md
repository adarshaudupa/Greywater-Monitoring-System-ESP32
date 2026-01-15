# Greywater Monitoring System (ESP32)

**Status:** Functional prototype (August 2025) | Grade: 9/10

## What It Does
Real-time turbidity-based water recycling system for bathroom greywater.
- Measures water quality before/after filtration
- Controls pump flow based on turbidity thresholds
- Diverts clean water to reuse tank, discards contaminated water

## System Architecture
- **MCU:** ESP32
- **Sensors:** 2x turbidity sensors (pre/post filtration), flow sensor
- **Actuation:** 12V pump (intake), 6V pump (distribution), post-carbon filter
- **Power:** 12V 1.3Ah SLA battery

## Key Engineering Challenges

### 1. Filter Pressure Tolerance (CRITICAL LEARNING)
**Problem:** Initial design used standard sediment filter. 12V diaphragm pump output (~60 PSI) exceeded filter housing rating (40 PSI max). Housing cracked during sustained operation.

**Solution:** Switched to post-carbon filter (higher pressure rating), adjusted flow control logic to prevent pressure spikes.

**Takeaway:** Always validate component pressure/current/thermal ratings under **sustained** load, not just peak specs.

### 2. Turbidity Threshold Calibration
**Problem:** Raw NTU readings varied with ambient light and water temperature.

**Solution:** [Describe your calibration approach - even if manual]

## Planned Features (Not Implemented)
**Scope was reduced due to time/budget constraints. Listed here for transparency:**
- ~~Automated valve control~~ (had 5V relay, needed 12V for solenoid valves)
- ~~pH sensing~~ (sensor module failed during testing)
- ~~TDS measurement~~ (budget exhausted)
- ~~UV sterilization~~ (cost prohibitive)
- ~~Sediment pre-filtration~~ (see pressure tolerance issue above)
- ~~Overflow protection~~ (float switch available, integration deprioritized)

## What I Built vs. What Teammates Built
- **My role:** Hardware selection, system integration, sensor interfacing, power distribution
- **Teammates:** ESP32 firmware, sensor data processing, pump control logic

## If I Rebuilt This Today
1. **Pressure-rated components:** Select all mechanical components with 2x safety margin
2. **Modular valve control:** Use MOSFET-based solid-state relays (no moving parts, voltage-agnostic)
3. **Sensor fusion:** Combine turbidity + conductivity for better water quality assessment
4. **Fail-safe logic:** Add hardware watchdog to prevent pump runaway
