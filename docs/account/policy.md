# Account Usage Policies

!!! info "Purpose of This Document"
    This document outlines mandatory account usage policies for all users of the REPACSS system at Texas Tech University. Adherence to these policies ensures the security, integrity, and proper utilization of REPACSS high-performance computing (HPC) resources.

---

## Account Ownership, Password Requirements, and MFA Policy

Each user is issued a unique username secured with both a password and a required multi-factor authentication (MFA) by the Texas Tech University. The credentials are strictly confidential and must not be shared.

- Passwords must be strong, rotated regularly, and follow the guidelines outlined on the [Passwords tips and guidelines for secure passwords](https://askit.ttu.edu/sp?id=kb_article_view&sysparm_article=KB0027598) page.
- MFA credentials are tied to the individual user and must be securely stored. More info can be found on [Multifactor Authentication (MFA)](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed&table=sc_cat_item&searchTerm=MFA) by Texas Tech Central IT.
- Shared account usage is strictly prohibited. REPACSS enforces a one-user-per-account policy without exception.

!!! danger "Account Misuse Policy"
    If unauthorized access or account sharing is detected, all affected accounts will be disabled immediately. Reinstatement requires a written explanation and authorization from the Principal Investigator (PI) or project lead.

---

## Cluster Usage Rules

!!! warning "Job Submission Means Acceptance"
    **Every job submission constitutes your agreement to comply with this policy.** If you do not comply, your job submission privileges may be **temporarily suspended**, or your **account may be disabled**, at the discretion of the REPACSS administrative team.

### Login Node Usage

Login nodes are shared by every user and exist only for light activities such as editing files, compiling small programs, managing data, and preparing and submitting jobs.

- **Do not run heavy compute on login nodes.** This includes long-running or multi-threaded programs, model training or inference, large builds, and data processing.
- **Do not run AI agents, coding agents, or autonomous tools on login nodes** if they execute compute-intensive work, spawn many processes, or run for extended periods. This includes agent-driven test runs, builds, and local model inference.
- Do not run local LLM servers (for example Ollama) or Jupyter kernels on login nodes. Request a compute node instead.
- Do not use login nodes for bulk data transfers. Use [Globus](../understanding/repacss-system/file-system/file-transfer.md) instead.
- Processes that degrade login node performance may be terminated without notice.

### Compute Resources

- All computational work must run on compute nodes through Slurm, either as a batch job or an interactive session.
- Request only the resources you need, and release them when your work is finished.
- Do not bypass the scheduler, for example by connecting directly to compute nodes without an allocation or by running background processes that outlive your job.
- Do not use cluster resources for activities unrelated to your approved research project.

### Enforcement

| Violation                                          | Typical Action                                                       |
|----------------------------------------------------|----------------------------------------------------------------------|
| Heavy compute or AI agents on a login node         | Processes terminated; warning issued                                 |
| Repeated or severe login node misuse               | Job submission privileges temporarily suspended                      |
| Bypassing the scheduler or misusing resources      | Job submission privileges temporarily suspended; account review      |
| Continued or serious violations                    | Account disabled; reinstatement follows the Account Misuse Policy    |

---

## Security Incidents and Reporting

Users who suspect account compromise, unauthorized activity, or any security incident must report it immediately to the system administrators.

- Email: [repacss.support@ttu.edu](mailto:repacss.support@ttu.edu)
- Teams: [General Channel](https://teams.microsoft.com/l/channel/19%3AGUibrd_0s_qo4BQOAMlhkEVQ0gv1CMdSwiijRz_ey9c1%40thread.tacv2/General?groupId=8014973a-ed11-4aff-8a0c-09a4d34cd1fa&tenantId=178a51bf-8b20-49ff-b655-56245d5c173c)

When reporting, please include as much detail as possible (e.g., timestamps, logs, screenshots) to expedite investigation and remediation.

---

## Account Lifecycle Management

REPACSS accounts follow a lifecycle process aligned with institutional research allocations.

### Account Provisioning

- Access is granted upon official request and must be tied to a recognized TTU research project.
- New users undergo a vetting process by the REPACSS administrative team.
- Account setup includes MFA enrollment and initial password configuration.

### Account Maintenance

- Accounts remain active only while associated with an ongoing research allocation.
- Users may be prompted to acknowledge and re-accept updated policy or conduct agreements.

### Account Deactivation

Accounts are subject to deactivation under the following conditions:

| Condition                             | Action Taken                                           |
|---------------------------------------|--------------------------------------------------------|
| End of affiliations with Texas Tech   | Eraider account disabled by IT; for more info please see [eRaider account disabled](https://askit.ttu.edu/sp?id=kb_article_view&sysparm_article=KB0030934)|
| End of research project               | Login disabled; data access granted for 60 days        |
| User-initiated request                | Immediate deactivation                                 |
| User removed by project PI            | Immediate deactivation                                 |
| Expiration of project membership      | Immediate deactivation                                 |
| Refusal to accept policy updates      | Access suspended until acknowledgment is received      |
| Violation of system security policies | Immediate deactivation; subject to further review      |
| Violation of cluster usage rules      | Job submission suspended or account disabled           |

Upon deactivation:

- Login credentials and MFA tokens are invalidated.
- Data may be accessible through designated transfer endpoints for a limited duration, subject to administrative approval.

---

## Proper Acknowledgment of REPACSS Resources

!!! info "Citation Requirement"
    All publications, presentations, or research outputs that utilize REPACSS computing resources must include the official acknowledgment statement below.

### Acknowledgment Text

> *This research used resources of the REPACSS high-performance computing system at Texas Tech University, supported in part by the National Science Foundation under NSF Award No. 2404438 and Texas Tech’s High-Performance Computing Center (HPCC).*

Proper citation ensures continued support and funding for REPACSS and reflects the scientific value of computational infrastructure.

!!! tip "Not Sure If This Applies?"
    If your research made use of REPACSS for simulations, analysis, training, or testing, it qualifies for acknowledgment.

---

