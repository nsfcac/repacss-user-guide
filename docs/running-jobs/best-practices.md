# 🛠️ Best Practices for REPACSS Users

This page outlines essential practices for making effective and considerate use of REPACSS resources. Following these practices helps maximize system performance, minimize job delays, and ensure fairness for all users.

---

## ✅ General Best Practices

* **Use `--time` Wisely**: Always request a realistic `--time` for your jobs. Overestimating leads to inefficient backfilling; underestimating can cause job termination.

* **Request Only What You Need**: Specify appropriate `--nodes`, `--ntasks`, and `--cpus-per-task`. Avoid overprovisioning to reduce idle resource waste.

* **Use Job Arrays**: For many similar short jobs, prefer `--array` to submitting hundreds of independent jobs. This reduces scheduler load.

* **Respect Shared Resources**: Avoid launching multiple simultaneous monitoring commands (e.g., `watch squeue`). Use longer intervals or alternatives like `sacct`.

* **Automate with Scripts**: Use submission and analysis scripts to avoid manual errors and streamline reproducibility.

* **Organize Job Files**: Keep your project directory clean by organizing outputs, logs, and scripts into appropriate folders.

---

## 🧪 Development vs. Production

* **Test First**: Use a short wall time and reduced node count to debug your application before scaling up.

* **Scale Gradually**: Once the small job completes successfully, increase the node count in stages.

* **Use Interactive Jobs for Debugging**: `salloc` with 1–2 nodes and `--time=01:00:00` is ideal for live testing.

* **Track Resource Usage**: Use `sacct`, `sstat`, and `jobstats` to analyze completed job efficiency.

---

## 🚦 Job Submission Etiquette

* **Avoid Resubmitting Frequently**: If a job is pending, do not cancel and resubmit repeatedly. This can reduce scheduling efficiency.

* **Use Holds Strategically**: Use `scontrol hold` to pause jobs instead of canceling and resubmitting.

* **Cancel Unused Jobs Promptly**: If you no longer need a job or see it stuck in pending unnecessarily, cancel it with `scancel`.

---

## 🔍 Monitoring and Diagnostics

* **Log into Compute Nodes**: Use `scontrol show job <jobid>` and SSH into compute nodes for diagnostics while jobs are running.

* **Monitor with Care**: Use `squeue`, `sqs`, or `sacct`. If using `watch`, do so at low frequency: `watch -n 60 squeue --me`.

* **Enable Email Alerts**: Add `--mail-type=begin,end,fail` and `--mail-user=<you@example.com>` to scripts for job status notifications.

---

## 🧼 Cleanup and Storage

* **Purge Temporary Files**: Remove scratch files, temporary logs, and unused intermediate outputs after job completion.

* **Archive Results**: Regularly move large output files to long-term storage or transfer them to your local system.

* **Limit Disk Footprint**: Keep your disk usage under control to prevent quota issues.

---

## 🧾 Documentation and Reproducibility

* **Document Parameters**: Log your job parameters (e.g., `SBATCH` settings, input files, module loads) to support reproducibility.

* **Version Your Code**: Use version control (e.g., Git) and commit job scripts alongside code changes.

* **Include README Files**: Explain directory structure, input expectations, and output interpretation in each major folder.

---

## 🙌 Collaboration and Support

* **Share Responsibly**: If collaborating, ensure shared scripts are documented, and avoid hardcoded paths.

* **Use the Ticketing System**: If unsure, submit a support ticket with relevant job IDs, error messages, and command history.

* **Stay Updated**: Watch for announcements from the system admins about downtime or usage changes.

---

For more help, visit the [Support page](../support.md).
