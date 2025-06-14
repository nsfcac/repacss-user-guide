# REPACSS Architecture

This document provides a comprehensive overview of the REPACSS (Remotely-managed Power Aware Computing Systems and Services) high-performance computing (HPC) infrastructure at Texas Tech University. The system is designed to support computationally intensive and data-driven research and is powered by renewable energy sources. REPACSS supports a wide range of scientific workloads, including simulations, artificial intelligence (AI), and large-scale data analytics.

---

## Access Requirements

To utilize REPACSS resources, users must meet the following prerequisites:

* A valid TTU eRaider account (for current users)
* Access to the GlobalProtect VPN
* Basic familiarity with HPC concepts
* Competence with Linux command-line environments

---

## Compute Resources

REPACSS consists of a heterogeneous cluster of compute resources optimized for both CPU-intensive and GPU-accelerated workloads.

### CPU Compute Nodes

* **Total Nodes**: 110
* **Processor**: Dual AMD EPYC 9754
* **Cores per Node**: 256
* **Memory per Node**: 1.5 TB DDR5
* **Storage per Node**: 1.92 TB NVMe SSD

### GPU Compute Nodes

* **Total Nodes**: 8
* **Processor**: Dual Intel Xeon Gold 6448Y
* **Cores per Node**: 64
* **Memory per Node**: 512 GB
* **GPUs per Node**: 4 × NVIDIA H100 NVL (94 GB HBM per GPU)
* **Storage per Node**: 1.92 TB SSD

### Login Nodes

* **Total Nodes**: 3
* **Processor**: Dual AMD EPYC 9254
* **Cores per Node**: 48
* **Memory per Node**: 256 GB
* **Storage per Node**: 1.92 TB NVMe SSD

---

## Storage Infrastructure

REPACSS includes nine storage nodes that collectively offer approximately 2.94 PB of multi-tiered storage. These systems utilize both high-speed NVMe drives and large-capacity HDDs to accommodate various storage requirements.

### Storage Node Summary

* **Processors**: Intel Xeon Gold (varied models)
* **Cores per Node**: 8 to 32
* **Memory per Node**: 512 GB to 1 TB
* **Storage per Node**: 25.6 TB to 583.68 TB

### Storage Tiers

* **Home**: Persistent personal storage for user scripts and configuration files.
* **Scratch**: High-performance temporary storage space subject to periodic purging.
* **Archive**: Long-term storage for research outputs and finalized datasets.

---

## Network Architecture

The network backbone of REPACSS supports high-throughput and low-latency communication among compute and storage nodes.

* **Switching Infrastructure**: Dell PowerSwitch S5248-ON and S5232-ON
* **Storage Interconnect**: InfiniBand network
* **Features**:
    * Reliable and fast data movement
    * Efficient support for multi-node parallel processing (MPI)
    * Secure remote access capabilities

---

## System Specifications Summary

| Node Type     | Total Nodes | CPU Model                | CPUs/Node | Cores/Node | Memory/Node | Storage/Node   | GPUs/Node | GPU Model                   |
| ------------- | ----------- | ------------------------ | --------- | ---------- | ----------- | -------------- | --------- | --------------------------- |
| CPU Nodes     | 110         | AMD EPYC 9754            | 2         | 256        | 1.5 TB DDR5 | 1.92 TB NVMe   | -         | -                           |
| GPU Nodes     | 8           | Intel Xeon Gold 6448Y    | 2         | 64         | 512 GB      | 1.92 TB SSD    | 4         | NVIDIA H100 NVL (94 GB HBM) |
| Login Nodes   | 3           | AMD EPYC 9254            | 2         | 48         | 256 GB      | 1.92 TB NVMe   | -         | -                           |
| Storage Nodes | 9           | Intel Xeon Gold (varied) | 2         | 8–32       | 512 GB–1 TB | 25.6–583.68 TB | -         | -                           |

---

## Additional Resources

* [Running Jobs](../../running-jobs/basics.md)
* [Available Software](../../software/available-software.md)
* [GPU Job Submission](../../running-jobs/interactive.md)
* [Monitoring and Troubleshooting](../../running-jobs/monitoring.md)

---

*Last updated: June 2025*
