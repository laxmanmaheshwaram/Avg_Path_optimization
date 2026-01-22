#  Quick Start Guide

Get up and running with the AGV Path Optimization Simulator in 5 minutes!

##  Installation

### Option 1: Quick Install
```bash
git clone https://github.com/yourusername/agv-path-optimization.git
cd agv-path-optimization
pip install -r requirements.txt
python agv_path_optimizer.py
```

### Option 2: Install as Package
```bash
git clone https://github.com/yourusername/agv-path-optimization.git
cd agv-path-optimization
pip install -e .
agv-optimize  # Run from anywhere
```

##  First Run

### Basic Example (5 lines of code)

```python
from agv_path_optimizer import WarehouseGrid, PathfindingAlgorithms, Visualizer

warehouse = WarehouseGrid(30, 30)
warehouse.create_warehouse_layout("default")
pathfinder = PathfindingAlgorithms(warehouse)
result = pathfinder.a_star((2, 2), (27, 27))

Visualizer(warehouse).plot_path(result)
```

**Output**: You'll see a visualization showing:
- Green star: Start position
- Red star: Goal position
- Yellow cells: Explored nodes
- Blue path: Optimal route found

##  Common Tasks

### 1. Compare Algorithms
```python
results = []
results.append(pathfinder.a_star((2, 2), (27, 27)))
results.append(pathfinder.dijkstra((2, 2), (27, 27)))
results.append(pathfinder.bfs((2, 2), (27, 27)))

Visualizer(warehouse).compare_algorithms(results)
```

### 2. Create Custom Warehouse
```python
warehouse = WarehouseGrid(40, 40)

# Add obstacles
for i in range(10, 30):
    warehouse.add_obstacle(15, i)

# Run pathfinding
result = pathfinder.a_star((5, 5), (35, 35))
```

### 3. Export Results
```python
from agv_path_optimizer import save_results_to_json

save_results_to_json([result], "my_results.json")
```

### 4. Try Different Heuristics
```python
# Manhattan (best for grid movement)
result1 = pathfinder.a_star((2,2), (27,27), heuristic_type="manhattan")

# Euclidean (for diagonal movement)
result2 = pathfinder.a_star((2,2), (27,27), heuristic_type="euclidean")

# Chebyshev (for 8-directional)
result3 = pathfinder.a_star((2,2), (27,27), heuristic_type="chebyshev")
```

##  Predefined Layouts

```python
# Simple warehouse with racks
warehouse.create_warehouse_layout("default")

# Complex maze
warehouse.create_warehouse_layout("maze")

# Open space (minimal obstacles)
warehouse.create_warehouse_layout("open")
```

##  Understanding Metrics

```python
result = pathfinder.a_star((2, 2), (27, 27))

print(f"Path Length: {result['path_length']}")        # Cells traveled
print(f"Nodes Explored: {result['nodes_explored']}")  # Search efficiency
print(f"Time: {result['execution_time']*1000:.2f}ms") # Speed
print(f"Success: {result['success']}")                # Path found?
```

**Interpreting Results**:
- **Lower path length** = shorter route
- **Fewer nodes explored** = more efficient algorithm
- **Faster execution time** = better performance
- **Higher efficiency ratio** (path_length/nodes_explored) = smarter search

##  Troubleshooting

### Problem: "No module named 'agv_path_optimizer'"
**Solution**: Make sure you're in the project directory and installed dependencies
```bash
cd agv-path-optimization
pip install -r requirements.txt
```

### Problem: Plots not showing
**Solution**: Add this to your script
```python
import matplotlib.pyplot as plt
plt.show()  # Add after visualizer.plot_path()
```

### Problem: Path not found
**Solution**: Check if start/goal are valid and not blocked
```python
# Verify positions are not obstacles
print(warehouse.is_obstacle(2, 2))  # Should be False
print(warehouse.is_obstacle(27, 27))  # Should be False
```

##  Next Steps

1. **Run examples**: `python examples/basic_usage.py`
2. **Read full docs**: Check `docs/` folder
3. **Experiment**: Try different warehouse sizes and layouts
4. **Contribute**: See `CONTRIBUTING.md` for guidelines

##  Pro Tips

1. **Start Small**: Begin with small grids (20x20) for faster experimentation
2. **Visualize Often**: Use `plot_path()` to understand algorithm behavior
3. **Compare Always**: Run multiple algorithms to see performance differences
4. **Save Results**: Export to JSON for later analysis
5. **Profile Code**: For large grids, use diagonal movement to reduce path length

##  Useful Commands

```bash
# Run main simulator
python agv_path_optimizer.py

# Run examples
python examples/basic_usage.py

# Run tests (if available)
pytest tests/

# Format code
black agv_path_optimizer.py

# Check code quality
flake8 agv_path_optimizer.py
```

##  Resources

- **Full Documentation**: [docs/README.md](docs/README.md)
- **API Reference**: [docs/api_reference.md](docs/api_reference.md)
- **Algorithm Details**: [docs/algorithms.md](docs/algorithms.md)
- **Tutorial Videos**: Coming soon!
- **Research Paper**: Link to your paper when published

## Common Questions

**Q: Which algorithm should I use?**  
A: For most cases, use A*. It's optimal and efficient.

**Q: Can I add diagonal movement?**  
A: Yes! Set `allow_diagonal=True` in algorithm calls.

**Q: How do I handle multiple AGVs?**  
A: This is a future feature. Currently focuses on single AGV optimization.

**Q: Can I use real warehouse data?**  
A: Yes! Import your layout and convert to grid format.

**Q: Is this production-ready?**  
A: This is a research/educational tool. For production, consider robustness, safety, and integration requirements.

---

**Need Help?** Open an issue on GitHub or contact: laxman09maheshwaram@gmail.com

Happy Pathfinding!
