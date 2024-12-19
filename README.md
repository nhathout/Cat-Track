# CatTrack

**Date:** October 4, 2024

## Overview
CatTrack is a behavior tracking device designed to monitor and classify feline activity using an accelerometer and temperature sensor, while providing real-time updates locally and through a web interface. This personal project demonstrates a compact system that collects movement data, temperature, and activity status, and then displays this information on an OLED display and web UI for analysis.

## Key Features

- **Movement Classification:**
  - Utilizes an accelerometer to measure and classify the cat’s activity (e.g., sleeping, walking, standing).
  - Aggregates multiple samples over a two-second window to ensure stable readings.
  - Computes pitch and roll from x, y, and z accelerations.

- **Continuous Reporting:**
  - Reports time, temperature, and classified activity to a laptop for visualization.
  - Data is displayed as strip charts on a web UI, allowing for easy interpretation of trends over time.
  
- **Local OLED Display:**
  - Shows cat’s name, current activity, and the elapsed time in that activity.
  - Features a button to cycle through different display modes (e.g., show name, show activity, show elapsed time).
  - Implements text scrolling if necessary and uses I²C communication to drive the display.

- **Temperature Measurement:**
  - Reads analog data from a thermistor-based temperature sensor.
  - Converts raw ADC readings to engineering units (°F) using the Steinhart-Hart equation.

## System Design

**Accelerometer Task:**
- Reads multiple acceleration samples within two seconds.
- Averages x, y, and z readings.
- Calculates pitch and roll, then classifies the cat’s activity.
- Synchronizes data with temperature and activity state before transmitting to the web interface.

**Button Task:**
- Detects button presses to switch between display modes.
- Enables toggling through cat name, activity, and elapsed time views on the OLED.

**Display Task:**
- Handles I²C communication to the OLED.
- Updates displayed information every cycle, showing relevant data (cat name, activity state, or time in activity).
- Manages scrolling text if the message exceeds the display size.

**Temperature Task:**
- Continuously reads from the ADC (A2 pin) for temperature measurements.
- Applies the Steinhart-Hart equation for accurate temperature conversion.
- Uses synchronization mechanisms (like semaphores) to ensure consistent console output and prevent race conditions.

## Results and Learnings

**Achievements:**
- Successfully classified cat activities based on motion patterns.
- Achieved stable, continuous reporting of time, temperature, and behavior to a web UI.
- OLED display effectively presented data in a user-friendly manner.

**Challenges:**
- Fine-tuning the activity classification thresholds required iterative testing.
- Integrating the display updates with sensor tasks needed careful timing and resource management.

**Potential Improvements:**
- Display the current real-world time on the OLED rather than just elapsed time.
- Include a contact number or additional information on the OLED display for real-world utility, such as helping a lost cat return home.
- Optimize interrupt-driven input (for the button) to reduce polling and improve responsiveness.

## Demonstrations

- [**Device Functionality Demo Video**](https://drive.google.com/file/d/1kXdl_pqsfS58n2JaBD2br86vPUoF4mpm/view?usp=sharing)
- [**Design Walkthrough Video**](https://drive.google.com/file/d/1MHmP07e8tH0pH1_1BzXr1exhsDJ_sImG/view?usp=sharing)

## Appendix
Circuit diagram:
![circuit-diagram](https://github.com/BU-EC444/Quest2-Team6-Bardwick-Hathout-Knutsen-Tran/blob/main/quest2/circuit-diagram1.png)

Images of circuit:
![circuit1](https://github.com/BU-EC444/Quest2-Team6-Bardwick-Hathout-Knutsen-Tran/blob/main/quest2/circuit-image1.png)
![circuit2](https://github.com/BU-EC444/Quest2-Team6-Bardwick-Hathout-Knutsen-Tran/blob/main/quest2/circuit-image2.png)

---

By integrating sensors, displays, and a web-based visualization platform, CatTrack provides a comprehensive system for monitoring feline behavior. This personal project underscores the potential for customizable pet monitoring solutions, offering insights into a cat’s daily activities and overall well-being.
