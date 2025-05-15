# System Overview

## REPACSS Facility Overview

The REPACSS is a high-performance computing (HPC) infrastructure designed to support intensive computational and data-driven research, powered by renewable energy. The system consists of compute, GPU, and storage nodes, interconnected with high-speed networking to ensure efficient data transfer and processing. The facility supports diverse workloads, including large-scale simulations, AI training, and data analytics.

## User Access

### Current Status
- **TTU Users Only**
  - Access via TTU eRaider accounts
  - Project-based allocations
  - TTU-specific support channels

### Future Integration
- **ACCESS Integration (Coming Soon)**
  - ACCESS user access
  - National allocation system
  - ACCESS support integration

## System Components

- **Compute Nodes:** 110 AMD-based nodes, each with dual AMD EPYC 9754 processors (256 cores, 1.5TB DDR5 memory per node, 1.92TB NVMe storage).
- **GPU Nodes:** 8 nodes, each with dual Intel Xeon Gold 6448Y processors (64 cores, 512GB memory), 4 NVIDIA H100 NVL GPUs (94GB HBM per GPU), and 1.92TB SSD storage.
- **Login Nodes:** 3 nodes, each with dual AMD EPYC 9254 processors (48 cores, 256GB memory, 1.92TB NVMe storage).
- **Storage Nodes:** 9 nodes, Intel Xeon Gold CPUs, 32/24/8 cores, 1024GB/512GB memory, 25.6TB–583.68TB storage per node, total ~2.94PB, high-speed NVMe and large-capacity HDDs.
- **Networking & Infrastructure:** Dell PowerSwitch S5248-ON and S5232-ON switches, high-speed interconnectivity, 2U rack-mounted chassis, redundant power supplies.

## System Specifications

| Node Type     | Total Nodes | CPU Model                | CPUs/Node | Cores/Node | Memory/Node  | Storage/Node    | GPUs/Node | GPU Model              |
| ------------- | ----------- | ------------------------ | --------- | ---------- | ------------ | --------------- | --------- | ---------------------- |
| CPU Nodes     | 110         | AMD EPYC 9754            | 2         | 256        | 1.5TB        | 1.92TB NVMe     | -         | -                     |
| GPU Nodes     | 8           | Intel Xeon Gold 6448Y    | 2         | 64         | 512GB        | 1.92TB SSD      | 4         | NVIDIA H100 NVL (94GB) |
| Login Nodes   | 3           | AMD EPYC 9254            | 2         | 48         | 256GB        | 1.92TB NVMe     | -         | -                     |
| Storage Nodes | 9           | Intel Xeon Gold (varied) | 2         | 32/24/8    | 1024/512GB   | 25.6–583.68TB   | -         | -                     |

## Storage Systems
- Multi-tiered storage, ~2.94PB total
- High-speed NVMe and large-capacity HDDs
- Home, scratch, and archive spaces

## Networking
- Dell PowerSwitch S5248-ON and S5232-ON
- High-speed internal and external connectivity
- InfiniBand for storage

## Related Resources
- [Getting Started](getting-started.md)
- [Running Jobs](running-jobs.md)
- [Software](software.md)
- [File Management](file-management.md)

---

*Source: [REPACSS System Specifications](https://repacss.org/resources/)*