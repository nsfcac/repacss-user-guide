## System Architecture

### 🖥 Compute Resources

- **CPU Nodes** (110 nodes):
  - Dual AMD EPYC 9754 processors
  - 256 cores per node
  - 1.5TB DDR5 memory
  - 1.92TB NVMe local storage

- **GPU Nodes** (8 nodes):
  - Dual Intel Xeon Gold 6448Y processors
  - 64 cores per node
  - 512GB memory
  - 4× NVIDIA H100 NVL GPUs (94GB HBM each)
  - 1.92TB SSD storage

- **Login Nodes** (3 nodes):
  - Dual AMD EPYC 9254 processors
  - 48 cores per node
  - 256GB memory
  - 1.92TB NVMe storage

---

### 🗄 Storage Resources

- **Storage Nodes** (9 nodes):
  - Intel Xeon Gold processors (varying core counts: 32/24/8)
  - Memory configurations: 1024GB / 512GB
  - Storage per node: 25.6TB to 583.68TB
  - Total capacity: ~2.94PB
  - Combines high-speed NVMe drives with large-capacity HDDs

---

### 🌐 Network Infrastructure

- Dell PowerSwitch S5248-ON and S5232-ON switches
- High-bandwidth internal and external connectivity
- InfiniBand backbone for storage I/O performance

---

## Node Specifications

| Node Type     | Total Nodes | CPU Model                | CPUs/Node | Cores/Node | Memory/Node  | Storage/Node    | GPUs/Node | GPU Model              |
|---------------|-------------|--------------------------|-----------|------------|---------------|------------------|-----------|------------------------|
| Compute       | 110         | AMD EPYC 9754            | 2         | 256        | 1.5TB         | 1.92TB NVMe     | –         | –                      |
| GPU           | 8           | Intel Xeon Gold 6448Y    | 2         | 64         | 512GB         | 1.92TB SSD      | 4         | NVIDIA H100 NVL (94GB) |
| Login         | 3           | AMD EPYC 9254            | 2         | 48         | 256GB         | 1.92TB NVMe     | –         | –                      |
| Storage       | 9           | Intel Xeon Gold (varied) | 2         | 32/24/8    | 1024/512GB    | 25.6–583.68TB   | –         | –                      |

---

## Storage Tiers

REPACSS features a multi-tiered storage system with ~2.94PB total capacity. Users can access:

- **Home** directories – for personal files and configuration
- **Scratch** – high-speed temporary storage for active jobs
- **Archive** – for long-term data retention

---

## Related Resources

- [Getting Started](getting-started.md)
- [Running Jobs](running-jobs.md)
- [Available Software](software.md)
- [File Management](file-management.md)
- [REPACSS Official Specs](https://repacss.org/resources/)

---

## Next Steps

1. Review [Getting Started](getting-started.md) to connect and configure your environment
2. Follow [Running Jobs](running-jobs.md) to submit and monitor compute tasks
3. Explore [Software](software.md) installed on the system
4. Learn [File Management](file-management.md) best practices

---

*Last updated: June 2025*
