# QSAM Acoustic Field Simulator

A compact Python simulation of an ultrasonic phased-array acoustic field and the optical targeting beams that intersect at a focal voxel.

## Overview

This project models a 16-element ultrasonic linear array operating at 40 kHz in air. The simulation computes a pressure field by summing contributions from each transducer as sinusoidal point sources and visualizes the resulting interference pattern.

The script also overlays two IR laser beams that intersect at the target position, visually representing the focal voxel or node to be excited.

## Features

- 16-element phased array geometry
- Acoustic field superposition model
- Beam steering toward a target point
- 2D visualization of pressure magnitude
- Optical target alignment overlay
- Adjustable target coordinates and array parameters

## Project Structure

```text
qsam-simulation/
├── README.md
├── requirements.txt
├── main.py
└── LICENSE
```

## Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/pranjalchaudhuri-dot/qsam-simulation.git
cd qsam-simulation
pip install -r requirements.txt
```

## Usage

Run the simulation:

```bash
python main.py
```

This displays the acoustic field heatmap with the laser intersection target.

## Configuration

Edit the parameters at the top of `main.py` to customize the simulation:

- `FREQ = 40000.0` — ultrasonic frequency in Hz
- `SPEED_OF_SOUND = 343.0` — sound speed in air at 20°C (m/s)
- `NUM_EMITTERS = 16` — number of array elements
- `PITCH = 0.01` — element spacing in meters (m)
- `RESOLUTION = 300` — simulation grid resolution (pixels per axis)
- `VOXEL_TARGET = (0.0, 0.10)` — focal point (x, y) in meters

## Example

To focus the acoustic field at the center (x=0) and a depth of 10 cm (y=0.10):

```python
VOXEL_TARGET = (0.0, 0.10)
plot_qsam_field(VOXEL_TARGET)
```

## Algorithm

### Phased Array Beam Steering

The simulator calculates the phase delay required for each transducer element to achieve constructive interference at the target point:

```
phase_delay[i] = k × distance(emitter[i], target)
```

where `k = 2π / λ` is the wavenumber.

### Acoustic Field Superposition

For each point in the 2D grid, the total acoustic pressure is computed as the sum of sinusoidal waves from all 16 emitters:

```
P(x, y) = Σ e^(i(k·r - φ[i]))
```

where:
- `r` = distance from emitter to grid point
- `φ[i]` = phase delay for emitter i

### Visualization

- **Heatmap** (inferno colormap): Acoustic pressure magnitude at each grid point
- **Cyan dots**: 16 ultrasonic transducers
- **Green dashed lines**: IR laser beams
- **White dot**: QSAM voxel (target excitation point)

## Physics Parameters

- **Frequency**: 40 kHz (typical for phased-array therapy and sonar)
- **Medium**: Air at 20°C (speed of sound ≈ 343 m/s)
- **Array**: Linear, 16 elements, 1 cm pitch (~15 cm total width)
- **Field region**: 20 cm × 20 cm (lateral × depth)

## Applications

- Acoustic ablation and surgical therapy
- Phased-array sonar simulation
- Educational visualization of constructive interference
- Precision medicine targeting

## License

MIT License — see `LICENSE` for details.

## Author

[Your Name/Pseudonym]  
October 2026
