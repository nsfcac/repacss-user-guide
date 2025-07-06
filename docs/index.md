# REPACSS User Guide Overview

The REmotely-managed Power Aware Computing Systems and Services (REPACSS) is a high-performance computing (HPC) data center and AI infrastructure prototype that demonstrates the feasibility of using variable energy for advanced computing tasks, with the goal of reducing costs and improving efficiency. REPACSS is designed to support intensive computational and data-driven research, powered by variable energy sources. The system consists of a combination of compute, GPU, and storage nodes, interconnected with high-speed networking to ensure efficient data transfer and processing. The facility is structured to accommodate diverse workloads, including large-scale simulations, AI training, and data analytics. This documentation serves as the official reference for all users seeking to utilize REPACSS systems in accordance with established operational standards, security policies, and best practices. 

---

## Documentation Overview

<!-- - [Getting Started at REPACSS](getting-started-at-REPACSS.md)  
  Detailed guidance on account creation, virtual private network (VPN) access, and system login procedures. -->

- [Absolute Beginner’s Guide](absolute-beginner-guide.md)  
  A high-level introduction to high-performance computing concepts and REPACSS usage for new users.

- [Scheduling Policies and Compute Accounting](running-jobs/scheduling.md)  
  Definitions of resource allocation models, charge factors, runtime limits, and job prioritization policies.

- [Sample SLURM Job Scripts](running-jobs/examples.md)  
  Verified examples to support the construction and submission of batch job scripts.

- [Core Job Submission Procedures](running-jobs/basics.md)  
  Step-by-step overview of SLURM commands, job queues, and execution workflows.

- [File Transfer Protocols and Utilities](understanding/repacss-system/file-system/file-transfer.md)  
  Guidance on secure and efficient data transfers via Globus.

- [UNIX File Access and Permissions](understanding/repacss-system/file-system/unix-permissions.md)  
  Overview of file ownership, group collaboration, and secure file access in a shared computing environment.

- [Sharing File Access with Others](understanding/repacss-system/file-system/ACL.md)  
  Guidance on how to share your files with others.

- [Multi-Factor Authentication (MFA) Procedures](connecting/mfa.md)  
  Official process for securing access to REPACSS resources using two-factor authentication.

---

## System Infrastructure and Technical Overview

- [System Architecture](understanding/repacss-system/architecture.md)  
  Technical description of the computational environment, including node types, CPUs, memory configurations, and interconnect topology.

- [Known Issues and Hardware Anomalies](understanding/repacss-system/known-issues.md)  
  Documented performance irregularities and hardware-specific limitations.

- [Software and Module Management](software/module-system.md)  
  Procedures for loading, managing, and deploying software modules within the REPACSS environment.

---

## Resource Scheduling and Job Execution

- [Batch and Interactive Job Submission](running-jobs/basics.md)  
- [Accessing Interactive Sessions](running-jobs/interactive.md)  
- [Monitoring Job Performance and Troubleshooting](running-jobs/monitoring.md)  
- [Operational Best Practices for Job Submission](running-jobs/best-practices.md)

---

## Optimization and Performance Engineering

<!-- - [Profiling and Analysis Tools](performance/profiling-tools.md)   -->
- [Compiler Flags](performance/compiler-flags.md)  
<!-- - [Scalability Testing and Benchmarking](performance/scaling-tests.md) -->

---

## Reference Materials

- [Technical Glossary](reference/glossary.md)  
- [Error Message Catalog](reference/common-errors.md)  
- [HPC Command Reference Sheet](reference/cheatsheet.md)

---

## <!--System Status and-->User Support

<!-- - [Live System Status](status.md)  
  View real-time information regarding system availability, node load, and queue performance. -->

- [Technical Support and Contact Information](support.md)  
  Resources for user assistance, including help desk contact methods and ticket submission.

---

## Contribution and Governance

This documentation is actively maintained by the REPACSS Systems Administration and Support Team. All technical content is subject to periodic review to ensure compliance with institutional standards and research computing best practices.  

Contributions, corrections, and feedback may be submitted via  
[GitHub Pull Request](https://github.com/nsfcac/repacss-user-guide), pending approval from the REPACSS documentation team.

---

