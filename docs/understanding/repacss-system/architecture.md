# REPACSS Architecture

Welcome to the architectural overview of REPACSS — the Research and Educational Platform for Advanced Computing Support Services at Texas Tech University. This document will guide you through the compute, storage, and networking resources available on the REPACSS cluster.

---

## 🧠 Compute Resources

REPACSS is a heterogeneous high-performance computing system optimized for both traditional CPU workloads and modern GPU-accelerated applications.

### CPU Compute Nodes

The majority of REPACSS's compute capacity comes from high-core-count AMD EPYC CPUs, suitable for large parallel jobs and memory-intensive simulations.

- 110 CPU nodes
- Dual AMD EPYC 9754 processors
- 256 total cores per node
- 1.5 TB DDR5 memory
- 1.92 TB local NVMe SSD

### GPU Compute Nodes

GPU resources are designed for machine learning, data analytics, and other massively parallel applications.

- 8 GPU nodes
- Dual Intel Xeon Gold 6448Y CPUs (64 cores)
- 512 GB RAM per node
- 4 × NVIDIA H100 NVL GPUs (94 GB HBM each)
- 1.92 TB local SSD

### Login Nodes

Users interact with the system through login nodes, where editing, compiling, and job submissions take place.

- 3 login nodes
- Dual AMD EPYC 9254 CPUs (48 cores)
- 256 GB RAM
- 1.92 TB NVMe SSD

---

## 💾 Storage Resources

REPACSS has nearly **3 PB** of storage capacity distributed across multiple tiers optimized for different use cases.

### Tiered Storage Overview

- **Home**: Persistent personal storage for source code and config files.
- **Scratch**: High-performance temporary storage for active simulations. Subject to purge policy.
- **Archive**: Long-term storage for research results and finalized datasets.

### Storage Node Hardware

| Node Type     | CPU Model         | Cores | RAM      | Local Storage     |
|---------------|------------------|-------|----------|-------------------|
| Storage-01    | Intel Xeon Gold 6238 | 44    | 512 GB   | 212.4 TB          |
| Storage-02    | Intel Xeon Gold 6226 | 24    | 512 GB   | 218.6 TB          |
| Storage-03    | Intel Xeon Gold 6346 | 32    | 1 TB     | 277.8 TB          |
| Storage-04    | Intel Xeon Gold 6346 | 32    | 1 TB     | 583.7 TB          |
| Storage-05    | Intel Xeon Gold 6338 | 32    | 1 TB     | 216.4 TB          |
| Storage-06    | Intel Xeon Gold 6338 | 32    | 1 TB     | 270.4 TB          |
| Storage-07    | Intel Xeon Gold 6338 | 32    | 1 TB     | 232.4 TB          |
| Storage-08    | Intel Xeon Gold 5317 | 8     | 512 GB   | 229.2 TB          |
| Storage-09    | Intel Xeon Gold 5317 | 8     | 512 GB   | 25.6 TB           |

---

## 🌐 Network Architecture

The REPACSS network architecture is designed to deliver high bandwidth and low latency for compute and storage operations.

- Core interconnect: Dell PowerSwitch S5248-ON and S5232-ON
- Storage network: Dedicated high-throughput fabric
- High-speed NICs support multi-node parallelism and MPI workloads

The network topology ensures:
- Efficient data movement between compute and storage
- Minimized I/O bottlenecks during job execution
- Reliable system access for remote users

---

## ⚙️ System Summary

| Component     | Count | Key Specs                                      |
|---------------|-------|-----------------------------------------------|
| CPU Nodes     | 110   | 256 cores, 1.5 TB RAM, NVMe SSD               |
| GPU Nodes     | 8     | 64 cores, 512 GB RAM, 4× NVIDIA H100 NVL      |
| Login Nodes   | 3     | 48 cores, 256 GB RAM, NVMe SSD                |
| Storage Nodes | 9     | 8–44 cores, 512 GB–1 TB RAM, up to 583 TB     |

---

## 🗃 Storage Best Practices

- Use `$HOME` for configs, scripts, and small files
- Use `$SCRATCH` for intermediate output and I/O-heavy workloads
- Archive finalized results in the long-term storage pool

!!! tip "Need more performance?"
    Running I/O intensive jobs? Always use `$SCRATCH` to avoid hitting I/O bottlenecks.

!!! warning "Don't forget to archive!"
    Scratch space is periodically purged. Move important data to long-term storage to avoid data loss.

---

## 🔗 Related Pages

- [Running Jobs](../../running-jobs/basics.md)
- [Available Software](../../software/available-software.md)
- [Using GPUs on REPACSS](../../running-jobs/interactive.md)
- [Monitoring and Troubleshooting](../../running-jobs/monitoring.md)

---

_Last updated: June 2025_
