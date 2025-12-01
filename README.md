# 3D Atomic Structure Simulator

A real-time 3D visualization tool for exploring atomic lattice structures with spin states and energy calculations. Built with C++ and Raylib, this simulator provides an interactive environment for visualizing quantum spin systems in a cubic lattice configuration.

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![C++](https://img.shields.io/badge/C%2B%2B-17-brightgreen)
![License](https://img.shields.io/badge/license-MIT-green)

## Features

### Visualization Modes
- **Spin Coloring**: Visualize atoms colored by their spin state (up/down)
- **Wireframe Mode**: Display lattice connections between neighboring atoms
- **Energy Heat Map**: Color atoms based on their interaction energy levels

### Interactive Controls
- **3D Navigation**: First-person camera controls for exploring the structure
- **Atom Selection**: Click on individual atoms to view detailed properties
- **Auto-Rotation**: Automatic camera rotation for presentation mode
- **Dynamic Scaling**: Adjust atom sizes for better visibility

### Physics Simulation
- Ising model implementation with nearest-neighbor interactions
- Real-time energy calculations for each atom
- Configurable coupling constants
- Random spin initialization

## Prerequisites

Before building this project, ensure you have:

- **C++ Compiler**: GCC 7.0+ or Clang 5.0+ with C++17 support
- **Raylib**: Version 4.0 or higher
- **CMake**: Version 3.10 or higher (optional, for build system)

### Installing Raylib

#### Linux (Ubuntu/Debian)
```bash
sudo apt-get install libraylib-dev
```

#### macOS
```bash
brew install raylib
```

#### Windows
Download pre-compiled binaries from [Raylib releases](https://github.com/raysan5/raylib/releases) or build from source.

## Building the Project

### Using g++ directly
```bash
g++ -std=c++17 main.cpp -o atomic_simulator -lraylib -lm
```

### Using CMake
```bash
mkdir build
cd build
cmake ..
make
```

## Usage

### Running the Simulator
```bash
./atomic_simulator
```

### Keyboard Controls

| Key | Action |
|-----|--------|
| **W/A/S/D** | Move camera forward/left/backward/right |
| **Mouse** | Look around (first-person view) |
| **E / Q** | Move camera up/down |
| **R** | Reset camera to initial position |
| **H** | Toggle help panel |
| **P** | Pause/Resume simulation |
| **Left Alt + Mouse** | Show wireframe while held |

### Mouse Controls
- **Left Click**: Select an atom to view its properties
- **Mouse Movement**: Rotate camera view

### UI Buttons
- **Toggle Wireframe**: Switch between normal and wireframe display
- **Color by Spin**: Display atoms colored by spin state
- **Color by Energy**: Show energy heat map visualization
- **Toggle Auto-Rotate**: Enable/disable automatic camera rotation
- **Atoms +/-**: Increase or decrease atom display size

## Configuration

You can modify simulation parameters in the code:

```cpp
struct SimulationParams {
    int N = 10;                    // Lattice size (N×N×N)
    float distance = 2.0f;         // Distance between atoms
    float couplingConstant = 1.0f; // Interaction strength
};
```

### Adjustable Constants
- `MAX_STRUCTURE_SIZE`: Maximum lattice dimensions (default: 20)
- `MIN_ATOM_SIZE`: Minimum atom display radius (default: 0.3)
- `MAX_ATOM_SIZE`: Maximum atom display radius (default: 2.0)

## Understanding the Physics

### Ising Model
The simulator implements a 3D Ising model where:
- Each atom has a spin: ↑ (up) or ↓ (down)
- Atoms interact with their nearest neighbors in the cubic lattice
- Energy is calculated using: E = -J × Σ(Si × Sj)
  - J: coupling constant
  - Si, Sj: spin values of neighboring atoms

### Energy Calculations
- **Parallel spins** (↑↑ or ↓↓): Lower energy (favorable)
- **Antiparallel spins** (↑↓): Higher energy (unfavorable)
- Color gradient: Blue (low energy) → Red (high energy)

## Project Structure

```
.
├── main.cpp           # Main application source code
├── README.md          # This file
└── build/             # Build directory (generated)
```

## Customization

### Changing Color Schemes
Modify the color constants at the top of `main.cpp`:
```cpp
const Color ATOM_UP_COLOR = { 52, 152, 219, 255 };    // Blue
const Color ATOM_DOWN_COLOR = { 231, 76, 60, 255 };   // Red
```

### Adjusting Camera Settings
Change initial camera parameters:
```cpp
Camera3D camera = {
    {0, 10, 30},    // Position
    {10, 10, 10},   // Target
    {0, 1, 0},      // Up vector
    60.0f,          // Field of view
    CAMERA_PERSPECTIVE
};
```

## Performance Considerations

- Default 10×10×10 lattice contains 1,000 atoms
- Performance may degrade with structures larger than 20×20×20
- Wireframe mode is more computationally intensive
- Recommended maximum: 15×15×15 for smooth 60 FPS

## Troubleshooting

### Compilation Errors
- Ensure Raylib is properly installed and in your library path
- Check that you're using C++17 or later: `-std=c++17`

### Performance Issues
- Reduce lattice size (N parameter)
- Disable wireframe mode
- Reduce atom size multiplier

### Visual Glitches
- Update graphics drivers
- Try reducing window size
- Disable auto-rotate if camera movement is jerky

## Future Enhancements

Potential features for future versions:
- Temperature-based Monte Carlo simulation
- Magnetic field application
- Export visualization data
- Animation recording
- Custom lattice geometries
- Phase transition visualization

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

## License

This project is open source and available under the MIT License.

## Acknowledgments

- Built with [Raylib](https://www.raylib.com/) - A simple and easy-to-use library for game programming
- Inspired by classical Ising model simulations in statistical mechanics
