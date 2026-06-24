# U.M.E.R Engine — Empirical Benchmarks & Performance Validation DONE ON THE P100 unless explicitly stated otherwise

![Performance](https://img.shields.io/badge/Throughput-21%2C933%20MCell%2Fs-FF1744?style=flat-square)
![Validation](https://img.shields.io/badge/Validation-Empirical%20Data-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Published-success?style=flat-square)

> **Part of the U.M.E.R (Uniform Memory Encoded Representation) Compute Core**

---

### Academic Preprint & Citation
The benchmark data contained in this repository directly supports the performance claims detailed in our manuscript submitted to the **Journal of Supercomputing**:

* **Title:** *U.M.E.R: A Deterministic Sort Free Architecture for High Density Physical & Agentic Systems*
* **Author:** Muhammad Umer
* **Preprint DOI:** [https://doi.org/10.21203/rs.3.rs-9848255/v1](https://doi.org/10.21203/rs.3.rs-9848255/v1)

---

## Overview

This repository contains the bare-metal benchmarking suites used to validate the execution speed of the U.M.E.R. architecture against traditional N-body and spatial querying limits. 

By functioning as a Massively Parallel Search Engine, the U.M.E.R. architecture completely bypasses $O(\log N)$ hierarchical tree structures (such as Octrees or BVHs). Because the engine utilizes an $O(1)$ spatial hash paired with a deterministic prefix-sum scatter, it maps the entire search space directly into a flat memory array. This completely eliminates GPU branch divergence, allowing memory bandwidth to be saturated efficiently.

## Empirical Results

The core validation data is separated into dimensional scale constraints to accurately reflect hardware utilization.

### 1. The 1D Scale Benchmark
The primary focus of this repository is the definitive 1D performance test, located in `1d_benchmarks_final.ipynb`. 
* **Peak Throughput:** **21,933 MCell/s**
* **Significance:** At a 1D scale, the architecture achieves maximum theoretical L1/L2 cache residency. Without the overhead of multi-axis traversal, the raw $O(1)$ memory offset grabbing operates at peak efficiency, proving the foundational latency of the spatial hash.

### 2. The 3D Scale Benchmark (Contextual Reference)
As detailed in the full manuscript's hardware validation section, scaling the continuous topology to a full 3D spatial bound introduces additional memory strata complexity. 
* **Peak Throughput:** **18,102 MCell/s**
* **Hardware Profile:** Validated on AMD MI300X HPC architecture.
* **Significance:** Even when resolving full 3x3x3 neighborhood volumes in 3D space, the engine retains near-linear scaling without suffering the exponential performance decay typical of traditional tree-building algorithms.

## Repository Structure

* `1d_benchmarks_final.ipynb` — The finalized, clean execution environment for validating the 21,933 MCell/s 1D throughput. This is the primary file to run for replication of the core claim.
* `benchmark.ipynb` — Additional historical and comparative testing arrays validating edge-case behavior and varying particle densities.

## Running the Benchmarks

To replicate the empirical data, launch the Jupyter environment. Ensure your GPU is not currently bound by external display rendering tasks to guarantee accurate timing.

```bash
jupyter notebook 1d_benchmarks_final.ipynb
