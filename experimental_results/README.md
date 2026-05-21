# File Format Description

These files contain the solution output for benchmark instances of the multi-vehicle RWCP. Each file records the result of a single run using a particular algorithm, fleet setting, and instance.

All curated result files are stored as CSV files. If the original file contained algorithm-parameter rows before the result header, those rows were removed so that the curated file begins directly with the result summary header.

---

## Directory Structure

The result files are grouped by instance type and fleet setting:

- `grid_homo/`: Synthetic grid instances with homogeneous vehicles.
- `grid_hetero/`: Synthetic grid instances with heterogeneous vehicles.
- `real_homo/`: Real-world instances with homogeneous vehicles.
- `real_hetero/`: Real-world instances with heterogeneous vehicles.

Each directory is further divided by algorithm. The algorithm names include:

| Algorithm Folder | Description |
|---|---|
| `H-GPM` | Hierarchical graph-partitioning-based matheuristic proposed in the study |
| `MILP` | Mixed-integer linear programming formulation used for grid-instance comparison |
| `Lum17+GPM` | Baseline based on the method of Lum et al. combined with the single-vehicle GPM routing component |
| `Chen25` | Baseline based on Chen et al. |
| `WJ19` | Baseline based on Willemse and Joubert |

Output filenames follow this convention:

```text
<instance>_output_<algorithm>.csv
```

For example, `R-A-a_output_HGPM.csv` is the H-GPM result for instance `R-A-a`.

---

## File Structure

Each route solution file consists of two parts.

### 1. Summary Section (Header)

The first two rows provide the column names and values for overall solution performance.

Typical fields include:

| Field Name | Description |
|---|---|
| `Problem Type` | Problem or experiment type identifier |
| `Solution Method` / `Multi Vehicle Solution Method` | Algorithm used to construct the multi-vehicle solution |
| `Clustering Method` / `Multi Vehicle Clustering Method` | Clustering method used in the solution process |
| `Single Vehicle Solution Method` | Routing method used for trip-level or single-vehicle subproblems |
| `Number of Vehicles` | Number of vehicles used in the solution |
| `Max Route Time` | Maximum route time among vehicles, including turn penalties |
| `Max Route Time wo Turns` | Maximum route time among vehicles, excluding turn penalties |
| `Total Route Time` | Sum of route times over all vehicles |
| `Total Route Time wo Turns` | Sum of route times excluding turn penalties |
| `Avg Route Time` | Average route time over vehicles |
| `Std Dev Route Time` | Standard deviation of route time over vehicles |
| `Min Route Time` | Minimum route time among vehicles |
| `Range Route Time` | Difference between maximum and minimum route time |
| `Shortest Path Time(Sec)` | Computational time for shortest-path preprocessing |
| `Balanced GP Time(Sec)` | Computational time for vehicle-level balanced graph partitioning |
| `Capacitated GP Time(Sec)` | Computational time for trip-level capacitated graph partitioning |
| `Computational Time(Sec)` | Total computational time |
| `VA(NHO)` | Visual attractiveness: normalized hull overlap |
| `VA(ATD)` | Visual attractiveness: average task distance |
| `VA(CCI)` | Visual attractiveness: connected component index |
| `VA(DMT)` | Visual attractiveness: distance from median to tasks |
| `VA(ROI)` | Visual attractiveness: route overlapping index |
| `VA(AOI)` | Visual attractiveness: arc overlapping index |
| `Optimal` | Whether optimality was proven, if applicable |
| `Lower Bound` | Lower bound from the MILP solver, if applicable |
| `MIP Gap` | MIP optimality gap, if applicable |

---

### 2. Route Log Section (Body)

After the summary rows, the route log section begins with its own header row. Each following row corresponds to a route segment visited by a vehicle.

| Field Name | Description |
|---|---|
| `Vehicle No` | Vehicle index in the solution |
| `Load No` | Index of the trip or load for the vehicle |
| `Sequence No` | Visiting order within the trip/load |
| `Arc` | Arc/edge identifier |
| `From Node` | Starting node of the segment |
| `To Node` | Ending node of the segment |
| `Is Edge` | 1 if the segment is an undirected edge; 0 otherwise |
| `Required` | 1 if the segment requires service; 0 otherwise |
| `Demand` | Waste demand collected on the segment |
| `Traveling Cost` | Traversal cost without service |
| `Service Cost` | Service cost for the segment |
| `Driver's Service Cost` | Service cost adjusted by driver/vehicle efficiency |
| `Served` | 1 if the required segment is serviced in this row |
| `Dumped` | 1 if dumping occurs at the start of the segment; otherwise 0 |
| `Turn Type` | Turn type from the previous segment (`Straight`, `Left`, `Right`, `U`, or `None`) |
| `Turn Cost` | Turn penalty applied before traversing the segment |
| `Depart Time` | Departure time from the starting node |
| `Arrival Time` | Arrival time at the ending node |
| `Visit No` | Visit index for the segment |
| `Shape` | Segment geometry in `LINESTRING(...)` format |

---

## Notes

- All result files are CSV files.
- The route log section has its own header row after the summary section.
- The route-cost estimation files use a different format; see [Route Cost Estimation Format](route_cost_estimation/README.md).
