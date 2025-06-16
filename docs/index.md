# REPACSS Technical Documentation

The Remotely-managed Power Aware Computing Systems and Services (REPACSS) is a high-performance computing (HPC) and data infrastructure initiative established to support the research mission of Texas Tech University (TTU). REPACSS provides scalable computational resources, secure data storage, and user support to facilitate advanced scientific and academic research. This documentation serves as the official reference for all users seeking to utilize REPACSS systems in accordance with established operational standards, security policies, and best practices.

---

## Official Documentation Index

- [Getting Started at REPACSS](getting-started-at-REPACSS.md)  
  Detailed guidance on account creation, virtual private network (VPN) access, and system login procedures.

- [Absolute Beginner’s Guide](absolute-beginner-guide.md)  
  A high-level introduction to high-performance computing concepts and REPACSS usage for new users.

- [Scheduling Policies and Compute Accounting](running-jobs/scheduling.md)  
  Definitions of resource allocation models, charge factors, runtime limits, and job prioritization policies.

- [Sample SLURM Job Scripts](running-jobs/examples.md)  
  Verified examples to support the construction and submission of batch job scripts.

- [Core Job Submission Procedures](running-jobs/basics.md)  
  Step-by-step overview of SLURM commands, job queues, and execution workflows.

- [File Transfer Protocols and Utilities](file-transfer.md)  
  Guidance on secure and efficient data transfers via Globus, `rsync`, and `scp`.

- [UNIX File Access and Permissions](unix-permissions.md)  
  Overview of file ownership, group collaboration, and secure file access in a shared computing environment.

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

- [Profiling and Analysis Tools](performance/profiling-tools.md)  
- [Compiler Optimization Strategies](performance/compiler-flags.md)  
- [Scalability Testing and Benchmarking](performance/scaling-tests.md)

---

## Reference Materials

- [Technical Glossary](reference/glossary.md)  
- [Error Message Catalog](reference/common-errors.md)  
- [Printable HPC Command Reference Sheet](reference/cheatsheet.md)

---

## System Status and User Support

- [Live System Status](status.md)  
  View real-time information regarding system availability, node load, and queue performance.

- [Technical Support and Contact Information](support.md)  
  Resources for user assistance, including help desk contact methods and ticket submission.

---

## Contribution and Governance

This documentation is actively maintained by the REPACSS Systems Administration and Support Team. All technical content is subject to periodic review to ensure compliance with institutional standards and research computing best practices.  

Contributions, corrections, and feedback may be submitted via  
[GitHub Pull Request](https://github.com/nsfcac/repacss-user-guide), pending approval from the REPACSS documentation team.

---

_Last official revision: June 2025_
