# Acoustic Localization Robot

## Overview
This project documents the design and build of a small tracked mobile robot intended to localize human voice / sound sources for search-and-rescue style scenarios. The system integrates a microphone array for acoustic direction finding, a drive platform (tank chassis + suspension + drivetrain), embedded motor control, and iterative testing to validate subsystem performance and end-to-end integration.

## Motivation
In real rescue environments, visibility is often poor (smoke, darkness, debris), and reaching a victim quickly can be the difference between life and death. This robot was built to explore whether a compact, rugged ground platform can use acoustic sensing to detect and point toward a sound source, enabling faster search and reducing risk to responders.

## System Architecture
The robot is organized as a set of tightly-coupled subsystems designed to support mobility, sensing, processing, and operator control. Each subsystem was developed and tested independently before full system integration.

### Mechanical Subsystem
- Tracked tank-style chassis for all-terrain mobility
- Christie-style suspension to maintain ground contact and reduce vibration
- Modular 3D-printed components allowing iterative redesign
- DC motors coupled to a geared drivetrain and sprockets

### Electrical & Power Subsystem
- Battery-powered DC system supplying motors and embedded electronics
- Motor drivers providing bidirectional speed and direction control
- Power distribution designed to isolate motor noise from sensitive sensors

### Sensing Subsystem
- Microphone array mounted on the robot body for acoustic localization
- Configurable microphone geometry tested for direction-finding performance
- ESP32-based camera module used for visual feedback and situational awareness

### Compute & Control Subsystem
- Arduino-based microcontroller handling:
  - Motor control (PWM, direction)
  - Microphone sampling and preprocessing
  - Coordination between sensing and actuation
- ESP32 camera operating as a separate processing node

### Data Flow
1. Microphones capture acoustic signals from the environment
2. Embedded code processes relative timing and amplitude differences
3. Direction estimate is computed and reported
4. Motor commands are generated for manual or assisted motion
5. Camera provides real-time visual feedback to the operator

### Mechanical Subsystem
- Tracked tank-style chassis for all-terrain mobility
- Christie-style suspension to maintain ground contact and reduce vibration
- Modular 3D-printed components allowing iterative redesign
- DC motors coupled to a geared drivetrain and sprockets

### Electrical & Power Subsystem
- Battery-powered DC system supplying motors and embedded electronics
- Motor drivers providing bidirectional speed and direction control
- Power distribution designed to isolate motor noise from sensitive sensors

### Sensing Subsystem
- Microphone array mounted on the robot body for acoustic localization
- Configurable microphone geometry tested for direction-finding performance
- ESP32-based camera module used for visual feedback and situational awareness

### Compute & Control Subsystem
- Arduino-based microcontroller handling:
  - Motor control (PWM, direction)
  - Microphone sampling and preprocessing
  - Coordination between sensing and actuation
- ESP32 camera operating as a separate processing node

### Data Flow
1. Microphones capture acoustic signals from the environment
2. Embedded code processes relative timing and amplitude differences
3. Direction estimate is computed and reported
4. Motor commands are generated for manual or assisted motion
5. Camera provides real-time visual feedback to the operator

## Hardware Design
The hardware design emphasized robustness, modularity, and ease of iteration. The robot was built around a compact tracked chassis to support uneven terrain while carrying sensing and compute hardware.

### Chassis & Mobility
- Tracked tank-style platform selected for stability and terrain adaptability
- 3D-printed chassis components enabled rapid iteration and fit adjustments
- Open internal volume allowed flexible placement of electronics and sensors

### Suspension & Drivetrain
- Christie-style suspension system used to maintain continuous track contact
- DC gear motors selected to provide sufficient torque for added payload
- Sprockets, road wheels, and track links assembled and tuned to reduce binding
- Mechanical resistance was minimized through iterative assembly and testing

### Sensors
- Multiple electret condenser microphones mounted on the robot body
- Microphone placement designed to test different array geometries
- ESP32 camera module mounted for forward-facing visual feedback

### Embedded Electronics
- Arduino-based microcontroller for real-time motor control and sensing
- Motor drivers interfaced via PWM and direction signals
- Power wiring routed to minimize electrical noise coupling into microphones

### Mechanical Iteration & Assembly
- Significant hands-on assembly including:
  - Press-fit inserts
  - Track link assembly
  - Suspension tuning
- Component tolerances and print quality required frequent inspection and adjustment

## Software Stack
The software stack was designed around embedded real-time control, incremental testing, and gradual subsystem integration.

### Embedded Control
- Arduino-based firmware written in C/C++ for:
  - Motor speed and direction control via PWM
  - Low-level timing and control logic
  - Coordinating sensing and actuation tasks
- Iterative tuning used to balance responsiveness, stability, and noise reduction

### Motor Control
- PWM-based motor control with adjustable frequency
- Direction and speed control implemented and tested incrementally
- PWM frequency adjustments used to reduce audible harmonics generated by motors

### Acoustic Processing
- Microphone signals sampled and processed on the microcontroller
- Relative timing and amplitude differences used to estimate sound direction
- Code evolved through repeated testing to improve directional accuracy

### Camera Integration
- ESP32 camera module programmed independently from the main controller
- Required manual firmware reset and reflash during development
- Provided visual feedback during testing and operation

### Development & Debugging
- Serial output used extensively for debugging and verification
- Subsystems validated independently before full integration

### Future Software Direction
- System architecture is compatible with migration to ROS2
- Microcontroller-based nodes could be bridged to higher-level ROS2 processing on a companion computer for advanced perception and navigation

## Acoustic Localization Approach
Microphone configuration, direction vs distance strategy, limitations.

## Testing & Results
What worked, what didn’t, key measurements.

## Challenges & Lessons Learned
- **3D printing is a schedule risk**: Print failures and tolerance/quality differences between printers impacted fit and forced reprints and redesign decisions. Plan buffer time and validate critical parts early. :contentReference[oaicite:2]{index=2}

- **Mechanical friction can look like an electrical problem**: Stiff drivetrain components created enough resistance that the motors struggled, which led to overcurrent warnings and “short-circuit-like” behavior on the supply. We had to mechanically free up the drivetrain before reliable testing. :contentReference[oaicite:3]{index=3}

- **PWM frequency matters (audible harmonics are real)**: Early motor control produced unpleasant audible harmonics/noise from the motors; increasing the effective PWM frequency reduced audibility, but control accuracy still required iterative tuning. :contentReference[oaicite:4]{index=4}

- **ESP32 camera bring-up is its own project**: Firmware upload issues were caused by the module’s behavior during reflashing; manually resetting/erasing was required before successful programming. Expect significant integration time for camera stacks. :contentReference[oaicite:5]{index=5}

- **Direction was easier than distance**: Our acoustic approach achieved near-perfect direction estimation but produced inaccurate distance estimates. This highlighted sensitivity to microphone geometry, timing, and environmental factors (reflections/noise). :contentReference[oaicite:6]{index=6}

- **Scope discipline beats “just add more sensors”**: We considered expanding from 3 microphones to 6 to improve accuracy, but time constraints made it infeasible. The better move was to stabilize and validate the existing architecture. :contentReference[oaicite:7]{index=7}

- **Morale is an engineering variable**: Getting the robot driving reliably was a major psychological inflection point for the team and improved execution velocity across remaining integration tasks. :contentReference[oaicite:8]{index=8}

## Future Improvements
What you would do next with more time/resources.

## Media
Photos, videos, diagrams.

## References
Papers, tutorials, resources used.

