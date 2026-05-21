# File Format Description

These files contain vehicle-level route-cost comparison summaries used to evaluate the route-cost estimation procedure embedded in H-GPM. Unlike the route solution output files, each file is a single CSV table whose rows compare the estimated final route cost with the actual route cost of each vehicle.

For grid instances, the estimates are curated from the sequential route-cost estimation results. For real-world instances, the estimates are curated from the subtrip-parallel route-cost estimation results. Actual route costs are extracted from the corresponding H-GPM route output files.

For homogeneous instances, `ActualRouteCost` is the route cost excluding turn penalties. For heterogeneous instances with `-ht` in the instance name, `ActualRouteCost` is the route cost including turn penalties.

---

## File Naming

Filenames follow this convention:

```text
<instance>_feature_breakdown.csv
```

For example, `R-A-a_feature_breakdown.csv` contains the route-cost comparison summary for instance `R-A-a`.

---

## File Structure

Each file contains one CSV table. Each row corresponds to one vehicle generated during route-cost estimation.

### Instance and Vehicle Fields

| Field Name | Description |
|---|---|
| `Instance` | Instance name |
| `VehicleIndex` | Zero-based vehicle index |
| `VehicleID` | Vehicle ID from the vehicle file |
| `VehicleCapacity` | Capacity of the vehicle |
| `VehicleMaxDuration` | Maximum route duration or working time |
| `VehicleEfficiency` | Driver or vehicle efficiency factor |
| `ClusterDemand` | Total demand assigned to the cluster |
| `TaskCount` | Number of tasks assigned to the cluster |

### Route Cost Comparison Fields

| Field Name | Description |
|---|---|
| `EstimatedRouteCost` | Estimated final route cost from the route-cost estimation procedure |
| `ActualRouteCost` | Actual vehicle route cost extracted from the H-GPM route output file |
| `DiffRouteCost` | `EstimatedRouteCost - ActualRouteCost` |
| `AbsolutePercentageError` | Absolute percentage error, in percent |

---

## Notes

- All files are CSV files.
- Route-cost estimation files are not route logs; they summarize final route-cost estimation accuracy by vehicle.
- `DiffRouteCost` is computed as estimated value minus actual value.
