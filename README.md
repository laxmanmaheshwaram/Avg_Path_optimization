# 🤖 AGV Warehouse Path Optimization Simulator

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-success.svg)]()

A comprehensive pathfinding algorithm simulator for **Automated Guided Vehicles (AGVs)** in warehouse logistics. This project implements and compares multiple pathfinding algorithms (A*, Dijkstra, BFS) for AGV navigation with interactive visualization and performance metrics.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Algorithms Implemented](#algorithms-implemented)
- [Project Structure](#project-structure)
- [Results & Analysis](#results--analysis)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Overview

This project is part of research on **data-driven, automated in-plant logistics** utilizing AGVs/AMRs (Autonomous Mobile Robots). The simulator provides:

- **Multiple pathfinding algorithms** optimized for warehouse environments
- **Interactive visualization** of algorithm performance
- **Comprehensive metrics** for comparing efficiency
- **Flexible warehouse layouts** for testing different scenarios
- **Export capabilities** for further analysis

### Research Context

This work supports planning, implementation, and operational management of AGV/AMR systems in manufacturing environments, focusing on:
- Path optimization for single and multi-AGV systems
- Collision avoidance strategies
- Energy-efficient routing
- Real-time adaptation to dynamic warehouse layouts

##  Features

### Core Functionality
- **Three pathfinding algorithms**: A*, Dijkstra, BFS
- **Customizable warehouse layouts**: Default, Maze, Open configurations
- **Interactive grid editing**: Add/remove obstacles dynamically
- **Real-time visualization**: Watch algorithms explore the space
- **Performance metrics**: Path length, nodes explored, execution time, efficiency
- **Comparative analysis**: Side-by-side algorithm comparison
- **Export results**: JSON format for further analysis

### Advanced Features
- **Diagonal movement support** (optional)
- **Multiple heuristic functions**: Manhattan, Euclidean, Chebyshev
- **High-quality visualizations**: Publication-ready plots
- **Data persistence**: Save and load warehouse configurations

##  Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Quick Start

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/agv-path-optimization.git
cd agv-path-optimization
```

2. **Create virtual environment** (recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Run the simulator**
```bash
python agv_path_optimizer.py
```

##  Usage

### Basic Usage

```python
from agv_path_optimizer import WarehouseGrid, PathfindingAlgorithms, Visualizer

# Create warehouse
warehouse = WarehouseGrid(width=30, height=30)
warehouse.create_warehouse_layout("default")

# Set start and goal positions
start = (2, 2)
goal = (27, 27)

# Initialize pathfinding
pathfinder = PathfindingAlgorithms(warehouse)

# Run A* algorithm
result = pathfinder.a_star(start, goal)

# Visualize results
visualizer = Visualizer(warehouse)
visualizer.plot_path(result, save_path="path_result.png")
```

### Advanced Usage

```python
# Compare multiple algorithms
results = []

# A* with different heuristics
results.append(pathfinder.a_star(start, goal, heuristic_type="manhattan"))
results.append(pathfinder.a_star(start, goal, heuristic_type="euclidean"))

# Dijkstra
results.append(pathfinder.dijkstra(start, goal))

# BFS
results.append(pathfinder.bfs(start, goal))

# Compare and visualize
visualizer.compare_algorithms(results, save_path="comparison.png")

# Save results to JSON
save_results_to_json(results, "results.json")
```

### Custom Warehouse Layout

```python
# Create custom warehouse
warehouse = WarehouseGrid(width=40, height=40)

# Add obstacles manually
for i in range(10, 30):
    warehouse.add_obstacle(15, i)
    warehouse.add_obstacle(25, i)

# Or use predefined layouts
warehouse.create_warehouse_layout("maze")  # Options: "default", "maze", "open"
```

##  Algorithms Implemented

### 1. A* (A-Star)
**Description**: Informed search algorithm using heuristics to guide the search.

**Characteristics**:
- Optimal (finds shortest path)
- Complete (always finds solution if exists)
- Efficient (explores fewer nodes than Dijkstra)
- Time Complexity: O(b^d) where b is branching factor, d is depth
- Best for: Most warehouse scenarios

**Heuristic Options**:
- **Manhattan Distance**: Best for grid-based movement (4-directional)
- **Euclidean Distance**: Better for diagonal movement
- **Chebyshev Distance**: Optimized for 8-directional movement

### 2. Dijkstra's Algorithm
**Description**: Guaranteed shortest path algorithm without heuristics.

**Characteristics**:
- Optimal (guaranteed shortest path)
- Complete
- Less efficient than A* (explores more nodes)
- Time Complexity: O((V + E) log V)
- Best for: When you need guaranteed optimal path without heuristic assumptions

### 3. Breadth-First Search (BFS)
**Description**: Simple uninformed search exploring all neighbors level by level.

**Characteristics**:
- Optimal (for unweighted graphs)
- Complete
- Least efficient (explores many unnecessary nodes)
- Time Complexity: O(V + E)
- Best for: Simple scenarios, educational purposes

## Project Structure

```
agv-path-optimization/
│
├── agv_path_optimizer.py      # Main implementation
├── requirements.txt            # Python dependencies
├── setup.py                    # Package installation
├── README.md                   # This file
├── LICENSE                     # MIT License
├── .gitignore                  # Git ignore file
│
├── examples/                   # Example scripts
│   ├── basic_usage.py
│   ├── compare_algorithms.py
│   └── custom_warehouse.py
│
├── results/                    # Output directory
│   ├── plots/
│   └── data/
│
├── docs/                       # Documentation
│   ├── algorithms.md
│   ├── api_reference.md
│   └── tutorials.md
│
└── tests/                      # Unit tests
    ├── test_algorithms.py
    ├── test_warehouse.py
    └── test_visualization.py
```

## Results & Analysis

### Performance Comparison (30x30 Grid, Default Layout)

| Algorithm | Path Length | Nodes Explored | Time (ms) | Efficiency |
|-----------|-------------|----------------|-----------|------------|
| A*        | 51          | 282            | 1.55      | 18.1%      |
| Dijkstra  | 51          | 814            | 2.56      | 6.3%       |
| BFS       | 51          | 813            | 0.87      | 6.3%       |

**Key Insights**:
- A* explores **45% fewer nodes** than Dijkstra while guaranteeing optimality
- All algorithms find the same shortest path (52 cells)
- A* is fastest with best efficiency ratio


## Future Enhancements

### Planned Features
-  **Multi-AGV coordination**: Handle multiple robots simultaneously
-  **Dynamic obstacles**: Real-time obstacle avoidance
-  **Energy optimization**: Battery-aware path planning
-  **Time windows**: Delivery deadline constraints
-  **3D warehouse layouts**: Multi-floor navigation
-  **Machine learning integration**: Learn optimal paths from historical data
-  **Real-time replanning**: Adapt to changing conditions
-  **Web interface**: Browser-based interactive simulator

### Research Extensions
- Traffic flow optimization
- Predictive maintenance scheduling
- Load balancing across AGV fleet
- Integration with warehouse management systems (WMS)

##  Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### How to Contribute
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 style guide
- Add unit tests for new features
- Update documentation
- Include docstrings for all functions

##  License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

**Your Name**
- Email: laxman09maheshwaram@gmail.com
- LinkedIn: [Your LinkedIn](https://www.linkedin.com/in/maheshwaramlaxman/)
- GitHub: [@yourusername](https://github.com/laxmanmaheshwaram)


##  Acknowledgments

- Research supervisor and team members
- Manufacturing companies providing real-world insights
- Technology providers for sensor and AI integration expertise
- Open-source community for excellent libraries (NumPy, Matplotlib)

## References

1. Hart, P. E., Nilsson, N. J., & Raphael, B. (1968). A formal basis for the heuristic determination of minimum cost paths. IEEE transactions on Systems Science and Cybernetics.

2. Dijkstra, E. W. (1959). A note on two problems in connexion with graphs. Numerische mathematik.

3. Russell, S., & Norvig, P. (2020). Artificial Intelligence: A Modern Approach (4th ed.).

---

⭐ If you find this project helpful, please consider giving it a star!

**Last Updated**: January 2026
