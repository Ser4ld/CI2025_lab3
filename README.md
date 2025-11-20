# CI2025 Lab 3

This project implements and compares three fundamental shortest path algorithms:
- **Dijkstra's Algorithm** - Efficient greedy approach for non-negative weights
- **A* Search** - Heuristic-guided variant of Dijkstra using Euclidean distance
- **Bellman-Ford Algorithm** - Handles negative weights and detects negative cycles

## Implemented Algorithms

### Dijkstra's Algorithm
- **Complexity**: O((V + E) log V) with priority queue
- **Use case**: Graphs with non-negative edge weights
- **Implementation**: All-pairs shortest paths using single-source runs

### A* (A-star) Search
- **Complexity**: O(E) best case, O(b^d) worst case
- **Heuristic**: Admissible Euclidean distance between nodes
- **Use case**: Point-to-point pathfinding with spatial coordinates
- **Implementation**: All-pairs computation for comprehensive benchmarking

### Bellman-Ford Algorithm
- **Complexity**: O(V × E)
- **Use case**: Graphs with negative edge weights
- **Feature**: Detects negative cycles
- **Implementation**: Edge relaxation over V-1 iterations

## Test Configurations

The benchmark suite evaluates algorithm performance across multiple dimensions:

### Graph Sizes
```
10, 20, 50, 100, 200, 500, 1000 nodes
```

### Density Levels
- `0.2` - Sparse graphs (20% edge connectivity)
- `0.5` - Medium density
- `0.8` - Dense graphs
- `1.0` - Complete graphs (all edges present)

### Noise Levels
- `0.0` - Pure Euclidean distances
- `0.1` - 10% perturbation
- `0.5` - 50% perturbation
- `0.8` - 80% perturbation

### Edge Weights
- `False` - Non-negative weights only (Dijkstra + A*)
- `True` - Allows negative weights (Bellman-Ford)


## Usage

```python
# Generate a random problem
problem_matrix, node_coords = create_problem(
    size=50,
    density=0.8,
    noise_level=0.1,
    negative_values=False,
    seed=42
)

# Run benchmark on a specific configuration
run_problem(
    size=50,
    density=0.8,
    noise_level=0.1,
    negative_values=False,
    save_results=True
)
```

## Output

Results are saved as CSV files with the naming convention:
```
ResultsCSV/metrics_size{size}_density{density}_noise{noise}_neg{negative}.csv
```

Each CSV contains:
- Source and target node pairs
- Computed distances for each algorithm
- Complete paths found
- Execution times (logged to console)


## Notes

- The framework automatically selects appropriate algorithms based on edge weights
- Negative edges trigger Bellman-Ford exclusively
- Non-negative graphs run both Dijkstra and A* for comparison
- All coordinates are normalized to [0,1] × [0,1] space
- Edge weights are scaled by 1000 and rounded for numerical stability
