# Solar Power Monitoring System
A real-time monitoring solution for solar panel systems that measures voltage, current, temperature, and light intensity to optimize performance and reliability of renewable energy sources.

## Project Overview

This Solar Power Monitoring System provides real-time measurement and display of critical solar panel parameters. The system measures voltage and current for power calculation, along with environmental conditions including temperature and light intensity, enabling efficient operation monitoring of solar panels.

## Core Features

- Real-time Power Calculation: Voltage × Current = Power output
- Environmental Monitoring: Temperature and light intensity tracking
- LCD Display: Local real-time data visualization
- Serial Output: Data monitoring via serial connection
- Continuous Monitoring: 24/7 system operation

### Key Metrics Monitored
- Voltage (V): Solar panel output voltage
- Current (A): Current flow from panels
- Power (W): Real-time power generation
- Temperature (°C): Ambient and panel temperature
- Light Intensity (Lux): Solar irradiance levels
- Efficiency (%): Basic performance calculation

## Hardware Components

| Component | Model/Type | Quantity | Purpose |
|-----------|------------|----------|---------|
| **Microcontroller** | Arduino Uno | 1 | Main processing unit |
| **Voltage Sensor** | Voltage Divider Circuit | 1 | Measure panel voltage |
| **Current Sensor** | ACS712 (30A) | 1 | Measure current flow |
| **Temperature Sensor** | DS18B20 | 1 | Ambient & panel temperature |
| **Light Sensor** | LDR | 1 | Light intensity measurement |
| **LCD Display** | 16x2 LCD | 1 | Local data display |
| **Resistors** | 10kΩ, 1kΩ | Multiple | Voltage divider & pull-ups |
| **Breadboard/PCB** | - | 1 | Circuit assembly |
| **Connecting Wires** | Jumper wires | Multiple | Component connections |

## Circuit Connections

### Arduino Uno Pin Configuration

**Analog Pins:**
- `A0`: Voltage sensor input (via voltage divider)
- `A1`: Current sensor (ACS712) output
- `A4`: SDA (I2C for BH1750 light sensor)
- `A5`: SCL (I2C for BH1750 light sensor)

**Digital Pins:**
- `Pin 2`: Temperature sensor (DS18B20) data line
- `Pin 7`: LCD RS (Register Select)
- `Pin 8`: LCD Enable
- `Pin 9-12`: LCD Data pins (D4-D7)
- `Pin 13`: Status LED (optional)

**Power Connections:**
- `5V`: Power supply for sensors and LCD
- `GND`: Common ground for all components

## Getting Started

### 1. Hardware Assembly

1. Voltage Divider Setup: Create voltage divider circuit using resistors (25:1 ratio for 0-25V measurement)
2. Current Sensor Installation: Connect ACS712 in series with solar panel positive wire
3. Temperature Sensors: Install DS18B20 sensors with 4.7kΩ pull-up resistor
4. Light Sensor: Connect LDR via I2C (SDA/SCL pins)
5. LCD Display: Wire 16x2 LCD in 4-bit mode to digital pins
6. Power Supply: Connect 5V power supply to Arduino and sensors

### 2. Software Installation

bash
# Clone the repository
git clone https://github.com/yourusername/solar-power-monitoring.git
cd solar-power-monitoring

# Required Arduino Libraries:
# - OneWire (for DS18B20 temperature sensors)
# - DallasTemperature (for DS18B20)
# - LiquidCrystal (for LCD display)
# - BH1750 (for light sensor)


### 3. Calibration

1. Voltage Calibration: Adjust `VOLTAGE_CALIBRATION` constant based on your voltage divider
2. Current Calibration: Verify ACS712 zero point and sensitivity values
3. Temperature Verification: Compare sensor readings with known temperatures
4. System Testing: Verify all sensors provide reasonable readings

### 4. Operation

1. Upload Code: Flash Arduino with the monitoring firmware
2. Power On: Connect power and verify LCD displays data
3. Monitor Output: View real-time data on LCD and serial monitor
4. Check Readings: Ensure all sensor values are realistic

## Software Features

### Real-Time Display Modes

The LCD cycles through different display modes every 3 seconds:

1. Power & Voltage: Current power output and panel voltage
2. Current & Efficiency: Current flow and calculated efficiency
3. Temperature: Panel and ambient temperature readings
4. Light Intensity: Solar irradiance measurement

### Serial Monitor Output

Connect to Arduino via USB to view detailed sensor data:

=== Solar Monitor Reading ===
Voltage: 18.45V
Current: 3.21A
Power: 59.2W
Panel Temp: 45.2°C
Ambient Temp: 28.1°C
Light: 45230 Lux
Efficiency: 59.2%
=============================


### Key Functions

```cpp
// Core measurement functions
float readVoltage();           // Measure panel voltage
float readCurrent();           // Measure panel current  
float calculatePower();        // Compute power (V × I)
float readTemperature();       // Get temperature readings
float readLightIntensity();    // Measure light levels
void updateDisplay();          // Refresh LCD display
```

## System Configuration

### Calibration Constants

```cpp
// Adjust these values based on your hardware
#define VOLTAGE_CALIBRATION 25.0    // Voltage divider ratio
#define ACS712_SENSITIVITY 0.066    // Current sensor sensitivity
#define ACS712_ZERO_POINT 2.5       // Zero current voltage
#define PANEL_RATED_POWER 100.0     // Your panel's rated power
```

### Measurement Parameters

- Voltage Range: 0-25V (adjustable with voltage divider)
- Current Range: 0-30A (with ACS712-30A)
- Temperature Range: -55°C to +125°C
- Light Range: 1-65535 Lux
- Update Frequency: 1 reading per second

## Performance Calculations

### Power Calculation
```cpp
Power (W) = Voltage (V) × Current (A)
```

### Basic Efficiency
```cpp
Efficiency (%) = (Actual Power / Rated Power) × 100
```

### Temperature Impact
Basic temperature compensation can be applied:
```cpp
// Typical solar panels lose ~0.4% per °C above 25°C
Compensated Power = Measured Power × (1 + 0.004 × (25 - Panel Temp))
```

## Monitoring Applications

### Residential Use
- Performance Verification: Check if panels are working optimally
- Troubleshooting: Identify issues with individual panels
- Weather Impact: Observe how weather affects power generation

### Educational Projects
- Solar Energy Learning: Understand solar panel behavior
- Data Analysis: Study relationships between environmental factors and power output
- System Optimization: Test different panel orientations and configurations

### Research Applications
- Panel Comparison: Test different solar panel types
- Environmental Studies: Analyze temperature and light impact on efficiency
- System Design: Optimize solar installations

## ⚡ Circuit Design

### Voltage Measurement Circuit
```
Solar Panel (+) ----[10kΩ]----+----[1kΩ]---- GND
                              |
                              +---- Arduino A0
```

### Current Measurement
- ACS712 sensor in series with positive wire
- Output voltage proportional to current flow
- 2.5V = 0A, increases/decreases with current direction

### Temperature Sensors
- DS18B20 with 4.7kΩ pull-up resistor
- One-wire protocol for multiple sensors
- Waterproof versions available for outdoor use

## Troubleshooting

### Common Issues

**LCD Not Displaying:**
- Check power connections (5V, GND)
- Verify data pin connections (D4-D7)
- Adjust contrast potentiometer

**Incorrect Voltage Readings:**
- Calibrate voltage divider ratio
- Check resistor values
- Ensure stable power supply

**Current Sensor Issues:**
- Verify ACS712 orientation (current flow direction)
- Check zero-point calibration
- Ensure proper power supply to sensor

**Temperature Sensor Problems:**
- Confirm 4.7kΩ pull-up resistor
- Check sensor addressing (multiple sensors)
- Verify waterproof connections if used outdoors

## Expected Performance

### Typical Readings
- 100W Panel (ideal conditions): ~18V, ~5.5A, ~100W
- Efficiency: 85-95% under good conditions
- Temperature Impact: 3-5°C above ambient for panels
- Light Threshold: >10,000 Lux for meaningful power generation

### Environmental Factors
- Temperature: Higher temps reduce voltage and efficiency
- Light Intensity: Directly proportional to power output
- Shading: Dramatic power reduction with partial shading
- Panel Angle: Affects light capture throughout day

## 🔮 Future Enhancements (Potential Upgrades)

While the current system focuses on real-time monitoring, potential future additions could include:

- **Data Logging**: SD card storage for historical analysis
- **Wireless Connectivity**: WiFi/Bluetooth for remote monitoring
- **Alert System**: Notifications for performance issues
- **Web Dashboard**: Browser-based monitoring interface
- **Mobile App**: Smartphone integration
- **Advanced Analytics**: Trend analysis and performance optimization

### Contact
@roshnikumar749@gmail.com for any queries!
---
