# File Format Description

These files are benchmark instances for the multi-vehicle residential waste collection problem (RWCP) with intermediate facilities and turn penalties. Each instance consists of a network file and a matching vehicle file.

The benchmark set contains synthetic grid instances and real-world instances. Homogeneous folders use vehicles with identical capacity and efficiency, while heterogeneous folders include vehicle-specific capacities and/or driver efficiency factors.

---

## Directory Structure

- `grid_homo/`: 15 synthetic grid instances and 15 matching vehicle files.
- `grid_hetero/`: 15 synthetic grid instances and 15 matching vehicle files.
- `real_homo/`: 10 real-world instances and 10 matching vehicle files.
- `real_hetero/`: 10 real-world instances and 10 matching vehicle files.

Network files use the instance name, such as `R-A-a.txt`. Vehicle files use the same name with `-vehicle`, such as `R-A-a-vehicle.txt`.

---

## Network File Structure

Each network `.txt` file consists of two parts.

### 1. Instance Specification (Header Section)

This section contains keyword-value pairs that define the overall characteristics of the instance.

Typical keywords include:

| Keyword | Description |
|---|---|
| `NAME` | Unique identifier of the instance |
| `NODES` | Number of nodes in the network |
| `REQ_EDGES` | Number of required undirected edges |
| `NOREQ_EDGES` | Number of non-required undirected edges |
| `REQ_ARCS` | Number of required directed arcs |
| `NOREQ_ARCS` | Number of non-required directed arcs |
| `DUMPING_COST` | Cost or time required at each disposal facility |
| `DUMPING_SITES` | Node IDs of disposal facilities |
| `TURN_PENALTY` | Turn costs for straight, right-turn, left-turn, and U-turn movements |

---

### 2. Network Element Lists (Body Section)

After the header section, the file lists required and non-required network elements.

Each section begins with a keyword row such as:

- `LIST_REQ_EDGES :`
- `LIST_NOREQ_EDGES :`
- `LIST_REQ_ARCS :`
- `LIST_NOREQ_ARCS :`

These rows are followed by the corresponding list of edges or arcs.

---

### Format of Each Arc/Edge Row

Each row is tab-delimited and follows this order:

| Field Name | Description |
|---|---|
| `source node ID` | Starting node of the arc/edge |
| `target node ID` | Ending node of the arc/edge |
| `service cost` | Cost incurred when servicing the arc/edge |
| `traveling cost` | Cost for traversing the arc/edge without service |
| `demand` | Waste demand on the arc/edge |
| `coordinate sequence` | Sequence of coordinates, written as `x1 y1,x2 y2,...` |
| `LINESTRING` | Geometry of the arc/edge in `LINESTRING(...)` format |

---

## Vehicle File Structure

Each `*-vehicle.txt` file is a tab-delimited table.

| Field Name | Description |
|---|---|
| `vehid` | Vehicle ID |
| `capacity` | Vehicle capacity |
| `max_duration` | Maximum route duration or working time |
| `efficiency` | Driver or vehicle efficiency factor |
| `depot_index` | Node ID of the depot used by the vehicle |

---

## Notes

- All network and vehicle files are tab-delimited.
- Node IDs are integers.
- Required arcs/edges represent street segments that must be serviced.
- Non-required arcs/edges may be traversed as traveling paths.
- Grid instances are synthetic networks; real-world instances are derived from road-network data.
- The coordinate sequence and `LINESTRING` fields describe the geometry of each arc/edge.
