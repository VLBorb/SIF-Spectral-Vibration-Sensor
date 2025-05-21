# Class 1: Low-Budget SIF

## Target Applications
Designed for small-scale industrial applications such as HVAC systems, conveyor belts, small motors, and general basic machinery monitoring where cost is a primary constraint[cite: 358, 385].

## Hardware Configuration
* **Microprocessor:** RP2040 (Dual-core ARM Cortex-M0+, 133 MHz) [cite: 386]
* **ADC:** Built-in 12-bit ADC on RP2040 (up to 500 ksps) [cite: 386]
* **Piezoelectric Transducer:** Generic 40-80 kHz disk [cite: 387]
* **Battery:** Rechargeable Li-Po, ~50 mAh capacity [cite: 387]
* **Energy Harvesting Circuit:**
    * Bridge Rectifier: 4x 1N4148 diodes [cite: 388]
    * Storage Capacitor: ~10 µF [cite: 388]
    * Charge Management IC: TP4056 or similar [cite: 388]
    * Voltage Regulator: MCP1700 (3.3V LDO) or similar [cite: 388]
* **Connectivity:** ESP-01 (ESP8266-based Wi-Fi module) for MQTT [cite: 389]
* **Encapsulation:** Epoxy resin, targeting IP65 rating [cite: 389]
* **Indicator:** Single SMD LED for status/alerts [cite: 389]

## Functionality
* **SIF Framework:** Implements a simplified version, primarily FFT and basic fractal divergence (SASF² concepts, DASF² likely omitted for computational simplicity)[cite: 390].
* **Outputs:** Spectral Divergence Index (SDI), possibly Dominant Frequency Shift (DFS)[cite: 390].
* **Communication:** Periodic data transmission (e.g., every 5 minutes) and alerts via MQTT to a configured broker.
* **Power Management:** Utilizes RP2040's deep sleep modes. The ESP-01 is powered on only during transmission to conserve energy[cite: 391]. Designed for energy surplus in typical vibrational environments (e.g., harvest ~0.5 mWh/hour, consume ~0.055 mWh/hour)[cite: 391].
* **Calibration:** Via vibration pattern (e.g., 3 sharp taps)[cite: 384].

## Specific Inventive Aspects / Characteristics
* **Ultra-Low Cost:** Designed to enable mass deployment in applications where traditional predictive maintenance is too expensive[cite: 392].
* **Energy Autonomy:** Self-powered through vibrational energy harvesting, a novel feature for budget-class sensors[cite: 392].
* **Robustness for Basic Industrial Use:** "No moving parts" and epoxy encapsulation provide reliability in common vibrational environments[cite: 393].
* **Simplified Processing:** Focuses on core anomaly detection (SDI) to minimize computational and power overhead on the RP2040[cite: 390].
