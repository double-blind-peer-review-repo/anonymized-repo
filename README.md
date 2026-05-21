# Multi-Vehicle Residential Waste Collection Problem

## Introduction

The multi-vehicle residential waste collection problem (RWCP) is an arc routing problem in which multiple vehicles service required street segments while satisfying capacity and working-time constraints, allowing repeated visits to disposal facilities.

This repository contains the benchmark instances and experimental results used in the study **"Equitable and Visually Attractive Arc Routing for Residential Waste Collection with Heterogeneous Fleets"**. The study considers workload balance, visual attractiveness, turn penalties, intermediate facilities, and heterogeneous fleets whose vehicles may differ in capacity and driver efficiency. The proposed method is a hierarchical graph-partitioning-based matheuristic (**H-GPM**) that assigns tasks to vehicles, partitions each vehicle workload into capacity-feasible trips, and routes each trip.

The file formats are described in the README file of each directory.

---

## Repository Structure and Guide

This repository is organized to separate benchmark instances from experimental results.

### benchmark_instances/

This folder contains the network and vehicle files used for the experiments. It consists of four subfolders:

- **[grid_homo/](benchmark_instances/grid_homo/)**: Synthetic grid instances with homogeneous vehicles.
- **[grid_hetero/](benchmark_instances/grid_hetero/)**: Synthetic grid instances with heterogeneous vehicles.
- **[real_homo/](benchmark_instances/real_homo/)**: Real-world instances with homogeneous vehicles.
- **[real_hetero/](benchmark_instances/real_hetero/)**: Real-world instances with heterogeneous vehicles.

Each instance has a network file and a matching vehicle file. Please refer to **[Benchmark Instances Format](benchmark_instances/README.md)** for the detailed instance format.

---

### experimental_results/

This folder contains curated result files generated from the computational experiments. It consists of five parts:

- **[grid_homo/](experimental_results/grid_homo/)**: Results for synthetic grid instances with homogeneous vehicles.
- **[grid_hetero/](experimental_results/grid_hetero/)**: Results for synthetic grid instances with heterogeneous vehicles.
- **[real_homo/](experimental_results/real_homo/)**: Results for real-world instances with homogeneous vehicles.
- **[real_hetero/](experimental_results/real_hetero/)**: Results for real-world instances with heterogeneous vehicles.
- **[route_cost_estimation/](experimental_results/route_cost_estimation/)**: Feature breakdown files used to evaluate the route-cost estimation procedure embedded in H-GPM.

The result folders are further grouped by algorithm, such as `H-GPM`, `MILP`, `Lum17+GPM`, `Chen25`, and `WJ19`.

> The route-cost estimation files have a different format from the route solution output files.
> For details, please refer to:
>
> - **[Experimental Results Format](experimental_results/README.md)**
> - **[Route Cost Estimation Format](experimental_results/route_cost_estimation/README.md)**

---

## Quick Navigation

- [Benchmark Instances Format](benchmark_instances/README.md)
- [Experimental Results Format](experimental_results/README.md)
- [Route Cost Estimation Format](experimental_results/route_cost_estimation/README.md)

